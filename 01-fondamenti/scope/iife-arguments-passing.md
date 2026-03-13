# [[../../appunti-completi#variazioni-del-pattern-iife|IIFE: Passaggio di Argomenti]]

## 📥 Passaggio di Parametri

Le IIFE permettono il passaggio di argomenti al momento dell'invocazione, consendo di legare valori esterni a variabili locali all'interno dello scope della funzione, rendendo il codice più efficiente.

### Oggetto Globale

```javascript
(function (global) {
  // 'global' riceve il riferimento a 'window'
  console.log(global === window); // true

  global.miaVar = "valore"; // Inserimento esplicito nel contesto globale
  console.log(global.document.title);
})(window);
```

**Vantaggi**:

- Fornisce un accesso esplicito allo scope globale dall'interno della IIFE.
- Permette una micro-ottimizzazione riducendo le operazioni di scope lookup, dato che il parametro `global` è risolto localmente.
- Rende evidente quando il codice sta apportando modifiche al contesto globale.

### Librerie Esterne

È pratica comune passare librerie globali come parametri alla IIFE per garantire l'accesso locale, mascherando o mappando i nomi interni.

```javascript
(function ($, _) {
  // '$' corrisponde a jQuery, '_' corrisponde a Lodash
  $(".element").hide();

  var array = [1, 2, 3];
  var doubled = _.map(array, (n) => n * 2);
})(jQuery, Lodash);
```

Se le librerie non sono definite al momento dell'invocazione, si verifica un errore "loud" immediatamente, facilitando il principio fail-fast.

## 🛡️ Garantire `undefined` (Pattern Classico)

In ambienti JavaScript (pre-ES5), la variabile globale `undefined` poteva essere riscritta. Il pattern IIFE offre un meccanismo di protezione:

```javascript
(function (window, document, undefined) {
  // Il parametro 'undefined' all'interno di questo scope è garantito essere il vero valore undefined,
  // poiché nessun terzo argomento viene fornito durante l'invocazione.

  var x;
  if (x === undefined) {
    console.log("Il valore di x è garantitamente undefined");
  }
})(window, document); // Invocazione con soli 2 argomenti
```

Questo uso, per quanto classico, è per lo più obsoleto oggi, ma risulta informativo se ci si confronta con vecchi progetti legacy.

### Alternative ES6+

Con l'introduzione dei parametri di default in ES6, questa tecnica si rivela meno propensa a errori e offre opzioni più flessibili e robuste per la configurazione:

```javascript
(function (config = {}) {
  var debug = config.debug ?? false; // Utilizzo del Nullish coalescing operator
  var timeout = config.timeout ?? 5000;
})();
```

## 📌 Tag

#javascript #iife #arguments #scope #undefined
