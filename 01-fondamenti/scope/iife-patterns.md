# [[../../appunti-completi#variazioni-del-pattern-iife|Pattern IIFE (Immediately Invoked Function Expression)]]

## 🎯 Concetto

Le **IIFE** (Immediately Invoked Function Expressions) sono funzioni che si eseguono immediatamente dopo essere state definite. Esistono diverse variazioni sintattiche e pattern di utilizzo, tutte basate sullo stesso principio: creare uno scope privato ed eseguirlo subito.

**Pattern Base**: `(function() { /* codice */ })();`

## 💻 Forma Anonima vs Nominata

### Anonima (Comune)

```javascript
// IIFE anonima
(function () {
  var messaggio = "IIFE anonima";
  console.log(messaggio);
})();

// Stack trace: <anonymous>
```

### Nominata (Best Practice)

```javascript
// IIFE nominata
(function IIFE() {
  var messaggio = "IIFE nominata";
  console.log(messaggio);
})();

// Stack trace: IIFE ← Utile per debugging!
```

**Vantaggio**: Nome visibile negli stack trace senza inquinare lo scope esterno.

## 🔧 Posizione delle Parentesi

Due stili funzionalmente identici:

```javascript
// STILE 1: Parentesi invocazione FUORI (più comune)
(function () {
  console.log("Stile 1");
})();

// STILE 2: Parentesi invocazione DENTRO (meno comune)
(function () {
  console.log("Stile 2");
})();

// Entrambi funzionano identicamente
```

### Altre Sintassi Valide

```javascript
// Operatori unari forzano espressione
!(function () {
  console.log("Con !");
})();
+(function () {
  console.log("Con +");
})();
~(function () {
  console.log("Con ~");
})();

// Meno comuni, stile standard preferito
```

## 📥 Passaggio di Argomenti

### Oggetto Globale

```javascript
(function (global) {
  // 'global' riceve 'window'
  console.log(global === window); // true

  global.miaVar = "valore"; // Esplicito
  console.log(global.document.title);
})(window);
```

**Vantaggi**:

- Accesso esplicito allo scope globale
- Riduce scope lookup (micro-ottimizzazione)
- Chiaro quando si modifica il globale

### Librerie Esterne

```javascript
(function ($, _) {
  // '$' è jQuery, '_' è Lodash
  $(".element").hide();

  var array = [1, 2, 3];
  var doubled = _.map(array, (n) => n * 2);
})(jQuery, Lodash);

// Se non definiti, errore immediato alla chiamata
```

### Pattern di Protezione

```javascript
(function (window, document, undefined) {
  // Parametri locali = lookup più veloce

  var app = {
    init: function () {
      console.log("App inizializzata");
    },
  };

  window.app = app; // Espone al globale
})(window, document);
```

## 🛡️ Garantire `undefined`

Protegge da sovrascrittura di `undefined` (vecchi browser):

```javascript
(function (window, document, undefined) {
  // 'undefined' qui è GARANTITO undefined
  // perché NON passiamo terzo argomento

  var x;
  if (x === undefined) {
    console.log("x è undefined"); // Sicuro
  }
})(window, document); // Solo 2 argomenti
```

**Pattern**: Parametro `undefined` senza argomento corrispondente.

### ES6+ Alternative

```javascript
// ES6+ ha parametri default nativi
(function (config = {}) {
  var debug = config.debug ?? false; // Nullish coalescing
  var timeout = config.timeout ?? 5000;
})();

// Non serve più 'undefined' come parametro
```

## 🌐 Pattern UMD (Universal Module Definition)

### Base

```javascript
// Funzione passata come argomento
(function (global, factory) {
  factory(global); // Esegue factory con dipendenze
})(window, function IIFEModulo(global) {
  // Codice del modulo
  var mioModulo = {
    versione: "1.0.0",
    init: function () {
      /* ... */
    },
  };

  global.mioModulo = mioModulo;
});
```

### UMD Completo (Multi-Ambiente)

```javascript
(function (root, factory) {
  // Rileva ambiente e usa sistema moduli appropriato

  if (typeof define === "function" && define.amd) {
    // AMD (RequireJS)
    define(["jquery"], factory);
  } else if (typeof module === "object" && module.exports) {
    // CommonJS (Node.js)
    module.exports = factory(require("jquery"));
  } else {
    // Browser globals
    root.MioModulo = factory(root.jQuery);
  }
})(typeof self !== "undefined" ? self : this, function ($) {
  // Codice che funziona ovunque
  function MioModulo() {
    /* ... */
  }
  return MioModulo;
});
```

**Uso**: Librerie che devono funzionare in browser, Node.js e AMD loaders.

## 📋 Casi d'Uso Comuni

### Inizializzazione

```javascript
var config = (function () {
  var env = "production";
  var apiKeys = { dev: "dev123", prod: "prod456" };

  function getKey() {
    return apiKeys[env];
  }

  return {
    apiUrl: "https://api.com",
    apiKey: getKey(),
    timeout: 5000,
  };
})();

// Solo 'config' esposto, dettagli privati
```

### Event Setup

```javascript
(function configuraEventi() {
  document.getElementById("form").addEventListener("submit", function (e) {
    e.preventDefault();
    // ...
  });
})();
```

### Module Pattern

```javascript
var Logger = (function () {
  var prefix = "[LOG]"; // Privato

  return {
    log: function (msg) {
      console.log(prefix, msg);
    },
    setPrefix: function (p) {
      prefix = p;
    },
  };
})();
```

## ⚖️ Confronto Stili

| Pattern                                   | Uso            | Vantaggi                      |
| ----------------------------------------- | -------------- | ----------------------------- |
| `(function(){}())`                        | IIFE base      | Standard, chiaro              |
| `(function IIFE(){})()`                   | IIFE nominata  | Debugging migliore            |
| `(function(w){...})(window)`              | Con argomenti  | Scope lookup ottimizzato      |
| `(function(w,d,u){...})(window,document)` | Con undefined  | Protezione retrocompatibilità |
| UMD                                       | Multi-ambiente | Funziona ovunque              |

## 📉 Pattern in Declino

Con **ES6 modules** e **bundler moderni** (Webpack, Vite):

- IIFE meno necessarie (moduli hanno scope privato nativo)
- UMD meno usato (bundler gestiscono compatibilità)
- Pattern resta utile per script standalone e compatibilità legacy

## 🔗 Concetti Correlati

- [[function-as-scope|Funzioni come Scope]] - Base delle IIFE
- [[anonymous-vs-named|Funzioni Anonime vs Nominate]] - Naming best practices
- [[module-management|Module Management]] - Evoluzione moderna
- [[hiding-in-scope|Hiding in Scope]] - Principio generale
- [[../../appunti-completi#variazioni-del-pattern-iife|Pattern IIFE Completo]]

## 📚 Risorse

- "You Don't Know JS" - Scope & Closures
- JavaScript Design Patterns
- UMD Pattern (Universal Module Definition)

## 📌 Tag

#javascript #iife #design-patterns #scope #modules #umd #closures #encapsulation
