# [[../../appunti-completi#barare-con-lo-scope-lessicale-cheating-lexical|Scope Lessicale: eval()]]

## 🎯 Concetto

Lo scope lessicale è normalmente **immutabile** e determinato dalla posizione del codice nel file sorgente (**author-time**). JavaScript offre meccanismi deprecati che permettono di "barare" modificando lo scope a **runtime**, come `eval()`.
Tale funzione esegue codice arbitrario a runtime, modificando dinamicamente lo scope lessicale. È una pratica fortemente sconsigliata.

## 💻 Esecuzione Dinamica di Codice

### Sintassi Base

La funzione `eval()` esegue la stringa passata come se fosse codice scritto in quella determinata posizione, creando o modificando variabili nello scope corrente:

```javascript
function foo(str, a) {
  eval(str); // modifica lo scope a runtime!
  console.log(a, b);
}

var b = 2;
foo("var b = 3;", 1); // 1, 3 - eval ha creato b nello scope di foo!
```

### eval() in Strict Mode

In **strict mode**, `eval()` possiede il proprio scope lessicale **isolato**:

```javascript
function foo(str) {
  "use strict";
  eval(str);
  // La dichiarazione dentro eval non "inquina" lo scope circostante
  console.log(a); // ReferenceError: a is not defined
}

foo("var a = 2");
```

### Funzioni Simili

Altre funzioni o costrutti accettano stringhe di codice ed eseguono la valutazione a runtime, presentando problematiche simili:

```javascript
// setTimeout / setInterval con stringhe (DEPRECATO)
setTimeout("console.log('Hello')", 1000); // ❌ SCONSIGLIATO

// Costruttore Function (leggermente più sicuro, ma da evitare)
var add = new Function("a", "b", "return a + b"); // ❌ SCONSIGLIATO
console.log(add(2, 3)); // 5
```

È considerato fondamentale utilizzare sempre callback function anziché stringhe di codice.

## ⚠️ Pericoli dell'Utilizzo

L'impiego di `eval()` comporta svantaggi significativi:

1. **Sicurezza**: Rischio di injection attacks se si esegue input utente senza validazione.
2. **Debugging**: Il codice generato dinamicamente risulta difficile da tracciare e analizzare.
3. **Performance**: L'engine JavaScript non è in grado di ottimizzare il codice (poiché lo scope è imprevedibile).
4. **Manutenibilità**: Il comportamento del programma diviene imprevedibile.

```javascript
// PERICOLOSO - Esecuzione di input non verificato
var userInput = getUserInput(); // Potrebbe contenere codice malevolo
eval(userInput); // ❌ PRATICA DA EVITARE ASSOLUTAMENTE
```

## 📚 Risorse

- MDN Web Docs: eval()
- "You Don't Know JS" - Scope & Closures

## 📌 Tag

#javascript #scope #eval #deprecated #security #lexical-scope #dynamic-execution