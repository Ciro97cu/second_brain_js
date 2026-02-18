# [[../appunti-completi#11-che-cosè-javascript|Che cos'è Javascript]]

JavaScript (JS) è un linguaggio di programmazione versatile, comunemente usato per creare interattività nelle pagine web. Permette di manipolare dinamicamente i contenuti, animare elementi, gestire eventi (come il click di un pulsante) e comunicare con un server per aggiornare parti della pagina senza doverla ricaricare completamente.

## Esecuzione: Non solo Interpretazione

Sebbene sia spesso descritto come un linguaggio interpretato (interpreted), la sua esecuzione è più complessa. I moderni motori JavaScript (JavaScript engines) — come V8 (in Chrome) o SpiderMonkey (in Firefox) — non si limitano a interpretare il codice riga per riga. Eseguono invece una compilazione Just-In-Time (JIT), traducendo il codice sorgente (source code) in codice macchina ottimizzato poco prima dell'esecuzione, garantendo così prestazioni molto più elevate.

## Tipizzazione Debole e Dinamica

JavaScript è un linguaggio a tipizzazione debole e dinamica (weakly and dynamically typed). Questo significa che non è necessario dichiarare il tipo di dato di una variabile (es. numero, testo, ecc.) quando la si crea. Una stessa variabile può contenere tipi di dati diversi nel corso del programma. Il linguaggio gestisce inoltre conversioni di tipo automatiche, un processo chiamato coercizione di tipo (type coercion). Questa flessibilità può accelerare lo sviluppo, ma richiede attenzione per evitare errori e comportamenti inattesi.

## Esempio

```javascript
// Manipolazione del DOM
document.getElementById("titolo").textContent = "Benvenuto!";

// Gestione eventi
document.getElementById("mioBottone").addEventListener("click", function () {
  alert("Hai cliccato!");
});

// Tipizzazione dinamica
let valore = 42; // number
valore = "Ciao"; // ora è string

// Type coercion
let risultato = "5" + 3; // "53"
let somma = "5" - 3; // 2
```

## Collegamenti

- [[esecuzione]] - Come JavaScript viene eseguito
- [[ecmascript]] - Lo standard che definisce JavaScript

## Riferimenti

- [MDN - What is JavaScript](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/What_is_JavaScript)
- [V8 JavaScript Engine](https://v8.dev/)
