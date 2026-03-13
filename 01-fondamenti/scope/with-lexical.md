# [[../../appunti-completi#barare-con-lo-scope-lessicale-cheating-lexical|Scope Lessicale: Costrutto with]]

## 🎯 Concetto

Il costrutto `with` è un meccanismo **deprecato** in JavaScript che crea temporaneamente un nuovo scope lessicale basato sulle proprietà di un oggetto. Benchè ideato per semplificare l'accesso ripetuto alle proprietà di un oggetto, tale costrutto nasconde comportamenti anomali e problematiche di sicurezza ed è vietato in strict mode.

## 🔀 Sintassi Base

L'utilizzo di `with` appare vantaggioso per modificare più proprietà dello stesso oggetto senza ripeterne il nome:

```javascript
var obj = { a: 1, b: 2, c: 3 };

// Senza with
obj.a = 2;
obj.b = 3;

// Con with (deprecato)
with (obj) {
  a = 3;
  b = 4;
}
console.log(obj); // { a: 3, b: 4, c: 3 }
```

## ⚠️ Il Pericolo: Variabili Globali Accidentali

Il comportamento più critico di `with` si manifesta quando si cerca di assegnare un valore a una proprietà non esistente nell'oggetto fornito.

```javascript
function foo(obj) {
  with (obj) {
    a = 2; // Quale scope viene modificato?
  }
}

var o1 = { a: 3 };
var o2 = { b: 3 };

foo(o1);
console.log(o1.a); // 2 - proprietà modificata correttamente

foo(o2);
console.log(o2.a); // undefined - o2 non possiede la proprietà 'a'
console.log(a);    // 2 - ⚠️ CREAZIONE DI VARIABILE GLOBALE ACCIDENTALE!
```

Se la proprietà richiesta (es. `a`) non viene trovata nell'oggetto, la risoluzione (scope lookup) sale nello scope lessicale esterno. Nel caso di una riassegnazione, se non viene trovata in nessuno degli scope superiori, viene generata una variabile globale (in non-strict mode) invece di aggiungerla all'oggetto o sollevare un errore.

## ⛔ Strict Mode

Data la pericolosità e l'imprevedibilità del costrutto, lo strict mode vieta esplicitamente l'uso di `with`:

```javascript
"use strict";

var obj = { a: 1 };
// with (obj) { // ❌ SyntaxError: Strict mode code may not include a with statement
//   a = 2;
// }
```

## ⛔ Svantaggi e Pericoli

1. **Variabili Globali Accidentali**: Modifica imprevista dello scope globale, generando hard-to-find bugs.
2. **Performance Devastante**: L'engine JavaScript non è in grado di ottimizzare staticamente il codice.
3. **Leggibilità**: Diviene impossibile determinare a quale scope appartenga una variabile semplicemente leggendo il codice.

## 📚 Risorse

- MDN Web Docs: with statement (deprecated)
- "You Don't Know JS" - Scope & Closures

## 📌 Tag

#javascript #scope #with #deprecated #global-leak #strict-mode #lexical-scope