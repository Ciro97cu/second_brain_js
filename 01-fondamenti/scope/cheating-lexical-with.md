# Barare con lo Scope Lessicale: with [[../../appunti-completi#barare-con-lo-scope-lessicale-cheating-lexical|📚]]

## 🎯 Concetto

`with` è un costrutto JavaScript **deprecato** che crea uno scope temporaneo da un oggetto. Apparentemente semplifica l'accesso ripetuto alle proprietà di un oggetto, ma in realtà introduce comportamenti pericolosi e imprevedibili.

**Perché è considerato "barare"**: `with` modifica la catena dello scope a runtime, trasformando un oggetto in uno scope lessicale temporaneo. Questo viola il principio che lo scope è determinato **author-time**.

## 💻 Sintassi e Comportamento

### with Base

```javascript
var obj = {
  a: 1,
  b: 2,
  c: 3,
};

// Senza with - ripetitivo
obj.a = 2;
obj.b = 3;
obj.c = 4;

// Con with - apparentemente più pulito
with (obj) {
  a = 3;
  b = 4;
  c = 5;
}
```

Sembra pratico, ma nasconde pericoli enormi.

### Il Pericolo: Creazione di Variabili Globali

```javascript
function foo(obj) {
  with (obj) {
    a = 2; // Cosa succede qui?
  }
}

var o1 = { a: 3 };
var o2 = { b: 3 };

foo(o1);
console.log(o1.a); // 2 - proprietà modificata

foo(o2);
console.log(o2.a); // undefined
console.log(a); // 2 - VARIABILE GLOBALE ACCIDENTALE!
```

**Problema**: Se l'oggetto non ha la proprietà `a`, `with` crea una variabile globale invece di dare errore!

### Come with Modifica lo Scope

```javascript
var obj = { a: 1 };

with (obj) {
  // Lo scope lookup parte da "obj"
  // 1. Cerca "a" in obj (TROVATO: obj.a)
  // 2. Se non trovato, cerca nello scope esterno
  console.log(a); // 1

  // "b" non è in obj, va nello scope globale
  console.log(b); // ReferenceError (se non esiste globalmente)
  b = 2; // Crea variabile GLOBALE!
}
```

### with in Strict Mode

```javascript
"use strict";

var obj = { a: 1 };
with (obj) {
  // SyntaxError: Strict mode code may not include a with statement
  // ...
}
```

**Strict mode vieta completamente `with`**.

## ⚠️ Pericoli

1. **Variabili Globali Accidentali**: L'esempio più pericoloso
2. **Performance Devastante**: L'engine non può ottimizzare codice con `with` (vedi sotto)
3. **Leggibilità**: Impossibile capire a quale scope appartiene una variabile
4. **Debugging**: Comportamento imprevedibile

## 🚀 Impatto sulle Performance

Sia `eval()` che `with` **distruggono le ottimizzazioni** dell'engine JavaScript:

```javascript
// L'engine NON PUÒ ottimizzare questo codice
function foo(obj) {
  with (obj) {
    a = b; // Quale scope? obj? globale? locale?
  }
}
```

**Perché**: L'engine deve assumere che lo scope possa cambiare a runtime, quindi:

- Non può fare **scope lookup statico**
- Non può fare **inline caching**
- Non può applicare ottimizzazioni lexical scope-based

**Regola**: Se anche una sola funzione usa `eval()` o `with`, **l'intero scope gerarchico superiore** non può essere ottimizzato.

## ✅ Alternative Moderne

```javascript
var obj = { a: 1, b: 2, c: 3 };

// ❌ con with (deprecato)
with (obj) {
  console.log(a, b, c);
}

// ✅ Destructuring (ES6+)
const { a, b, c } = obj;
console.log(a, b, c);

// ✅ Accesso esplicito
obj.a = 2;
obj.b = 3;
obj.c = 4;
```

Il destructuring è più esplicito, sicuro e ottimizzabile.

## 🔗 Concetti Correlati

- [[cheating-lexical-eval|eval() e cheating]] - Altro meccanismo deprecato
- [[lexical-scope-base|Scope Lessicale]] - Il principio violato
- [[scope-vs-properties|Scope vs Proprietà]] - Differenza fondamentale
- [[../../appunti-completi#barare-con-lo-scope-lessicale-cheating-lexical|Barare con Scope Lessicale Completo]]

## 📚 Risorse

- MDN: with statement (deprecated)
- "You Don't Know JS" - Scope & Closures, Chapter 2

## 📌 Tag

#javascript #scope #with #deprecated #performance #global-leak #strict-mode #lexical-scope
