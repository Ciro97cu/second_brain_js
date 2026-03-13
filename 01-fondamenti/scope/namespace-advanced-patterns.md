# [[../../appunti-completi#namespace-globali-global-namespaces|Namespace Pattern Avanzati]]

Il pattern del namespace può essere esteso per supportare architetture più complesse, organizzando ulteriormente il codice e integrandolo con altri pattern come il Module Pattern.

## Sub-Namespaces

Per applicazioni di grandi dimensioni, un singolo livello di namespace potrebbe non essere sufficiente. In questi casi, è possibile nidificare oggetti all'interno del namespace principale per creare **sub-namespaces**, organizzando logicamente le funzionalità in moduli separati.

```javascript
var App = {
  version: "2.0.1",

  // Sub-namespace per le utility
  utils: {
    formatta: function (str) {
      return str.toUpperCase();
    },
    valida: function (email) {
      return email.includes("@");
    }
  },

  // Sub-namespace per l'interfaccia utente
  ui: {
    mostraMessaggio: function (msg) {
      console.log("[UI]", msg);
    }
  },

  init: function () {
    this.ui.mostraMessaggio("App inizializzata v" + this.version);
  }
};

App.init(); // "[UI] App inizializzata v2.0.1"
App.utils.formatta("test"); // "TEST"
```

## Integrazione con il Module Pattern

Il namespace di base espone tutte le sue proprietà pubblicamente. Per supportare l'incapsulamento e nascondere dettagli implementativi privati, il pattern del namespace viene spesso combinato con il [[module-pattern|Module Pattern]] utilizzando una [[iife-concept|IIFE]].

```javascript
var CalcolatriceAvanzata = (function () {
  // Stato e metodi privati
  var risultato = 0;
  var precisione = 2;

  function arrotonda(num) {
    return Math.round(num * Math.pow(10, precisione)) / Math.pow(10, precisione);
  }

  // API Pubblica esposta nel namespace
  return {
    somma: function (a, b) {
      risultato = arrotonda(a + b);
      return risultato;
    },
    getRisultato: function () {
      return risultato;
    }
  };
})();

CalcolatriceAvanzata.somma(10.555, 20.333); // Ritorna la somma arrotondata
// CalcolatriceAvanzata.arrotonda non è accessibile
```

Questa combinazione garantisce un unico punto di accesso globale, esponendo solo le interfacce necessarie e mantenendo lo stato interno inaccessibile dall'esterno.
