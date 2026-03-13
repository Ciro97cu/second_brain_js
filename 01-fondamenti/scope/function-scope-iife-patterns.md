# [[../../appunti-completi#funzioni-come-scope|Funzione come Scope: Pattern IIFE e Incapsulamento]]

## 🎯 Pattern IIFE (Immediately Invoked Function Expression)

L'impiego di una espressione di funzione invocata immediatamente (IIFE) rappresenta una tecnica fondamentale per creare scope isolati istantaneamente, escludendo qualsiasi rischio di inquinamento dello scope esterno.

```javascript
var a = 2;

(function IIFE() {
  var a = 3; // Variabile isolata nello scope della funzione
  var b = 4;

  function helper() {
    return a + b;
  }

  console.log(helper()); // 7
})(); // Le parentesi finali forzano l'esecuzione immediata della funzione

console.log(a); // 2 (Il valore esterno originario NON è inquinato)
// console.log(b); // ReferenceError (variabile b strettamente privata)
// console.log(IIFE); // ReferenceError (nome IIFE mantenuto privato)
```

## 💼 Caso d'Uso Pratico: Inizializzazione Complessa

Le IIFE sono spesso utilizzate per eseguire complessi blocchi di setup dell'applicazione, garantendo che le variabili temporanee necessarie alla configurazione svaniscano al termine dell'esecuzione, senza influire sull'ambiente al di fuori dell'espressione.

```javascript
var config = (function () {
  // Configurazione temporanea e incapsulata
  var env = "production";
  var apiKeys = { dev: "dev123", prod: "prod456" };

  function getKey() {
    return apiKeys[env];
  }

  // Viene restituito esclusivamente l'oggetto pubblico finale
  return {
    apiUrl: "https://api.com/api",
    apiKey: getKey(),
    timeout: 5000,
  };
})();

// È esposto unicamente il riferimento 'config'
config.apiUrl; // Accessibile ed utilizzabile
// env; // ReferenceError (mantiene la privacy delle variabili di setup)
```

## ⚖️ Analisi dei Vantaggi: Function Scope

La scelta di sfruttare le funzioni, ed in particolare espressioni come le IIFE, apporta benefici notevoli dal punto di vista dell'architettura dello stato:

| Caratteristica | Dichiarazione di Funzione | Espressione/IIFE |
| ---------------------------- | ------------- | ----------- |
| Nome visibile esternamente   | ✅ Sì         | ❌ No       |
| Esecuzione automatica        | ❌ No         | ✅ Sì       |
| Inquinamento scope globale   | ⚠️ Possibile  | ❌ Mai      |
| Privacy dei dati implementati| ⚠️ Parziale   | ✅ Totale   |

Le problematiche tipicamente risolte includono l'eliminazione di collisioni accidentali tra nomi identici (shadowing e sovrascritture impreviste) e il rispetto dei principi dell'information hiding.

## 🔗 Risorse e Riferimenti

- "You Don't Know JS" - Scope & Closures
- [[module-pattern|Il Pattern Modulo]] - Evoluzione orientata allo sviluppo web
- [[function-scope-concept|Concetto di Scope via Funzioni]]

## 📌 Tag

#javascript #iife #encapsulation #modules #patterns
