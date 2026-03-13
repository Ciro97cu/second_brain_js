# [[../../appunti-completi#variazioni-del-pattern-iife|IIFE: Pattern UMD]]

## 🌐 Universal Module Definition (UMD)

Il pattern UMD (Universal Module Definition) si avvale dell'IIFE per creare moduli in grado di funzionare universalmente su diversi ambienti di esecuzione (es. browser, Node.js, e strumenti di caricamento AMD).

### Struttura Base

La IIFE accetta due parametri: l'oggetto globale (`global`) e una funzione `factory` che racchiude il codice del modulo. In questo modo si iniettano direttamente le funzionalità desiderate.

```javascript
// La funzione factory passata come argomento viene eseguita all'interno della IIFE
(function (global, factory) {
  factory(global); // Esecuzione della factory con iniezione delle dipendenze
})(window, function IIFEModulo(global) {
  // Implementazione del modulo
  var mioModulo = {
    versione: "1.0.0",
    init: function () {
      /* inizializzazione del modulo */
    },
  };

  // Esposizione globale
  global.mioModulo = mioModulo;
});
```

### Implementazione Completa (Multi-Ambiente)

Il pattern UMD completo rileva l'ambiente di esecuzione a runtime e adotta il sistema di esportazione del modulo più appropriato fra AMD, CommonJS e moduli Browser base (Global Variable).

```javascript
(function (root, factory) {
  // Rilevamento dinamico dell'ambiente e del sistema di moduli

  if (typeof define === "function" && define.amd) {
    // Ambiente AMD (es. RequireJS)
    define(["jquery"], factory);
  } else if (typeof module === "object" && module.exports) {
    // Ambiente CommonJS (es. Node.js)
    module.exports = factory(require("jquery"));
  } else {
    // Ambiente Browser tramite variabili globali
    root.MioModulo = factory(root.jQuery);
  }
})(typeof self !== "undefined" ? self : this, function ($) {
  // Il codice del modulo, progettato per funzionare in ogni ambiente supportato
  function MioModulo() {
    /* implementazione */
  }
  return MioModulo;
});
```

L'uso principale di questo pattern si riscontra nello sviluppo di librerie pubbliche (storicamente come jQuery o simili) che necessitano di funzionare interscambiabilmente all'interno di normali tag script del browser, moduli CommonJS di Node.js e moduli caricati in modo asincrono (AMD). Si nota in tempi recenti che il target UMD viene comunque pre-generato da compiler moderni e non risulta più una necessità scriverselo a mano.

## 📌 Tag

#javascript #iife #umd #modules #compatibility
