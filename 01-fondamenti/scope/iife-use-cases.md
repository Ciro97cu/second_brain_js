# [[../../appunti-completi#variazioni-del-pattern-iife|IIFE: Casi d'Uso Comuni]]

## 📋 Scenari Applicativi Tipici

Le IIFE sono state sfruttate estensivamente in JS e offrono una modalità robusta per nascondere informazioni all'interno dello scope locale, facilitando diversi pattern architetturali e operativi all'interno delle applicazioni.

### Strutturazione e Inizializzazione

Le IIFE sono ideali per racchiudere logiche di configurazione, incapsulando calcoli in un singolo passaggio o computazione complessa ed esponendo solo il risultato finale richiesto al di fuori, senza così inquinare lo scope globale.

```javascript
var config = (function () {
  var env = "production";
  var apiKeys = { dev: "dev123", prod: "prod456" };

  function getKey() {
    return apiKeys[env];
  }

  // Ritorna le impostazioni pubbliche finali (Closure)
  return {
    apiUrl: "https://api.com",
    apiKey: getKey(),
    timeout: 5000,
  };
})();

// Verrà esposto esclusivamente l'oggetto 'config', le variabili e le funzioni interne restano private e al riparo dall'esterno.
```

### Configurazione di Eventi Standalone

Utili per eseguire il setup di listener temporanei per gli eventi e isolando specificatamente tutte le variabili temporanee.

```javascript
(function configuraEventi() {
  document.getElementById("form").addEventListener("submit", function (e) {
    e.preventDefault();
    // gestione dell'evento submit
  });
})();
```

### Module Pattern

Essendo alla base del Module Pattern per intero, permettono l'implementazione dell'incapsulamento e dell'accesso privilegiato dei dati prima dell'avvento dei moduli ES6 nativi e Classi private.

```javascript
var Logger = (function () {
  var prefix = "[LOG]"; // Variabile mantenuta interamente privata grazie alla closure stabilita dalla IIFE

  return {
    log: function (msg) {
      console.log(prefix, msg);
    },
    setPrefix: function (p) {
      prefix = p; // Metodo che consente l'aggiornamento controllato di un dato privato
    },
  };
})();
```

## ⚖️ Vantaggi a Confronto

| Pattern Costruttivo          | Vantaggio Principale Ricavato                                                                  |
| ---------------------------- | ---------------------------------------------------------------------------------------------- |
| `(function(){})();`          | Definizione IIFE di base; syntax standard e chiaro internazionalmente                          |
| `(function NOME(){})();`     | IIFE con nominazione; migliora significativamente il debugging base e gli stack trace generati |
| `(function(w){...})(window)` | IIFE con argomenti; ottimizza lo scope lookup per riferimenti globali pesanti                  |

## 📌 Tag

#javascript #iife #use-cases #module-pattern #encapsulation
