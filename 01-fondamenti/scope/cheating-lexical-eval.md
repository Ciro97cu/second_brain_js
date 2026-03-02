# Barare con lo Scope Lessicale: eval() [[../../appunti-completi#barare-con-lo-scope-lessicale-cheating-lexical|📚]]

## 🎯 Concetto

`eval()` è una funzione JavaScript che permette di eseguire codice arbitrario **a runtime**, modificando dinamicamente lo scope lessicale. Questo "imbroglio" permette al codice di alterare lo scope dopo che è stato definito, violando il principio fondamentale dello scope lessicale determinato **author-time**.

**Perché è considerato "barare"**: Lo scope lessicale è normalmente immutabile e determinato dalla posizione del codice nel file sorgente. `eval()` rompe questa regola permettendo modifiche runtime.

## 💻 Sintassi e Comportamento

### eval() Base

```javascript
function foo(str, a) {
  eval(str); // modifica lo scope a runtime!
  console.log(a, b);
}

var b = 2;
foo("var b = 3;", 1); // 1, 3 - eval ha creato b nello scope di foo!
```

`eval()` esegue la stringa come se fosse codice scritto in quella posizione.

### eval() in Strict Mode

In **strict mode**, `eval()` ha il proprio scope lessicale isolato:

```javascript
function foo(str) {
  "use strict";
  eval(str);
  console.log(a); // ReferenceError: a is not defined
}

foo("var a = 2");
```

La dichiarazione dentro `eval()` non "inquina" lo scope circostante.

### Funzioni Simili a eval()

Queste funzioni accettano stringhe di codice ed eseguono runtime evaluation:

```javascript
// setTimeout / setInterval
setTimeout("console.log('Hello')", 1000); // SCONSIGLIATO

// new Function()
var add = new Function("a", "b", "return a + b"); // SCONSIGLIATO
console.log(add(2, 3)); // 5
```

**Nota**: Usare sempre callback function anziché stringhe di codice.

## ⚠️ Pericoli

1. **Sicurezza**: Eseguire stringhe arbitrarie apre a injection attacks
2. **Debugging**: Codice dinamico è difficile da debuggare
3. **Performance**: L'engine non può ottimizzare codice che può essere modificato a runtime
4. **Manutenibilità**: Comportamento imprevedibile, difficile da testare

```javascript
// PERICOLOSO - Input utente
var userInput = getUserInput(); // Potrebbe contenere codice malevolo
eval(userInput); // MAI FARE QUESTO!
```

## ✅ Alternative Moderne

Invece di `eval()`, usa:

```javascript
// ❌ Vecchio approccio
eval("console.log('Hello')");

// ✅ Approccio moderno
const code = () => console.log("Hello");
code();

// ❌ Per accesso a proprietà dinamiche
var obj = { a: 1, b: 2 };
eval("console.log(obj." + prop + ")");

// ✅ Bracket notation
console.log(obj[prop]);
```

## 🔗 Concetti Correlati

- [[lexical-scope-base|Scope Lessicale]] - Il principio che eval() viola
- [[scope-window|Variabili Globali e window]] - Scope globale
- [[cheating-lexical-with|with statement]] - Altro meccanismo deprecato
- [[../../appunti-completi#scope-lessicale-lexical-scope|Scope Lessicale Completo]]

## 📚 Risorse

- MDN: eval() is evil
- "You Don't Know JS" - Scope & Closures

## 📌 Tag

#javascript #scope #eval #deprecated #security #performance #lexical-scope
