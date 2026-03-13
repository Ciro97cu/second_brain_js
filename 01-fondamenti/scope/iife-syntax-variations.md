# [[../../appunti-completi#variazioni-del-pattern-iife|IIFE: Variazioni Sintattiche]]

## 🔧 Posizione delle Parentesi

Esistono due stili sintattici principali per definire e invocare una IIFE, che risultano funzionalmente identici:

```javascript
// STILE 1: Parentesi di invocazione ALL'ESTERNO (più comune)
(function () {
  console.log("Stile 1");
})();

// STILE 2: Parentesi di invocazione ALL'INTERNO (meno comune ma valido)
(function () {
  console.log("Stile 2");
}());
```

Entrambi gli stili garantiscono l'immediata esecuzione della funzione.

### Altre Sintassi Valide

L'uso di operatori unari è un modo alternativo per forzare il JavaScript parser a trattare la funzione come un'espressione invece che come una dichiarazione, eliminando la necessità delle parentesi di raggruppamento esterne:

```javascript
// Operatori unari forzano l'espressione
!(function () {
  console.log("Esecuzione con l'operatore !");
})();

+(function () {
  console.log("Esecuzione con l'operatore +");
})();

~(function () {
  console.log("Esecuzione con l'operatore ~");
})();
```

Sebbene queste sintassi siano valide e talvolta utilizzate per risparmiare uno o più byte nel codice minificato, lo stile standard con le parentesi di raggruppamento è generalmente preferito per la sua maggiore chiarezza e leggibilità.

## 📌 Tag

#javascript #iife #syntax #design-patterns #expressions
