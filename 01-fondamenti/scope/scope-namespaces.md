# [[../../appunti-completi#namespace-globali-global-namespaces|Namespace Globali (Global Namespaces)]]

## 🎯 Concetto

Un **namespace** è un contenitore (solitamente un oggetto) che raggruppa tutte le funzionalità di una libreria sotto un unico nome globale. Questo evita di "inquinare" lo scope globale con decine di identificatori e previene conflitti tra librerie diverse.

**Pattern**: Una sola variabile globale per libreria, tutte le funzionalità come proprietà.

## 💻 Problema e Soluzione

### Cattiva Pratica: Inquinamento Globale

```javascript
// ❌ Libreria 1
function utilityFunction() {
  /* ... */
}
function helper() {
  /* ... */
}
function doSomething() {
  /* ... */
}
var version = "1.0";

// ❌ Libreria 2 (CONFLITTO!)
function utilityFunction() {
  /* ... */
} // Sovrascrive!
function helper() {
  /* ... */
} // Sovrascrive!
```

### Buona Pratica: Namespace

```javascript
// ✅ Libreria 1
var MyReallyCoolLibrary = {
  awesome: "stuff",
  doSomething: function () {
    console.log("Doing something cool!");
  },
  doAnotherThing: function () {
    console.log("Doing another thing!");
  },
};

// ✅ Libreria 2
var AnotherLibrary = {
  awesome: "different stuff", // NO conflitto!
  doSomething: function () {
    // NO conflitto!
    console.log("Doing something else!");
  },
};

// Uso senza conflitti
MyReallyCoolLibrary.doSomething(); // "Doing something cool!"
AnotherLibrary.doSomething(); // "Doing something else!"
```

## 💡 Pattern Avanzati

### Sub-Namespaces

```javascript
var MiaApp = {
  version: "2.0.1",

  // Sub-namespace per organizzazione
  utils: {
    formatta: function (str) {
      return str.toUpperCase();
    },
    valida: function (email) {
      return email.includes("@");
    },
  },

  ui: {
    mostraMessaggio: function (msg) {
      console.log("[UI]", msg);
    },
  },

  init: function () {
    this.ui.mostraMessaggio("App inizializzata v" + this.version);
  },
};

MiaApp.init(); // "[UI] App inizializzata v2.0.1"
```

### Module Pattern con Namespace

```javascript
var CalcolatriceAvanzata = (function () {
  // *** PRIVATO ***
  let risultato = 0;
  let precisione = 2;

  function arrotonda(num) {
    return (
      Math.round(num * Math.pow(10, precisione)) / Math.pow(10, precisione)
    );
  }

  // *** PUBBLICO (API esposta) ***
  return {
    somma: function (a, b) {
      risultato = arrotonda(a + b);
      return risultato;
    },
    moltiplica: function (a, b) {
      risultato = arrotonda(a * b);
      return risultato;
    },
    getRisultato: function () {
      return risultato;
    },
    setPrecisione: function (p) {
      precisione = p;
    },
  };
})();

// Uso: unico nome globale, API chiara
CalcolatriceAvanzata.somma(10.555, 20.333); // 30.89
// arrotonda() non accessibile - privato!
```

## 🌍 Esempi nel Mondo Reale

### Librerie Famose

```javascript
// jQuery usa '$' e 'jQuery'
jQuery.ajax({
  /* ... */
});
$.each(array, function () {
  /* ... */
});

// Lodash usa '_'
_.map(array, fn);
_.filter(array, predicate);

// React usa 'React'
React.createElement("div", null, "Hello");
React.Component;
```

Ogni libreria occupa **un solo nome** nello scope globale, evitando conflitti.

## ⚠️ Vantaggi

1. **Zero Conflitti**: Nomi unici per libreria
2. **Organizzazione**: Funzionalità raggruppate logicamente
3. **API Chiara**: `Libreria.metodo()` è esplicito e leggibile
4. **Compatibilità**: Più librerie possono coesistere senza problemi

## ✅ Best Practices

- **Nome Unico**: Usa nomi descrittivi e sufficientemente unici
- **Singola Esposizione**: Una sola variabile globale per progetto/libreria
- **Sub-Namespaces**: Organizza funzionalità correlate in sotto-oggetti
- **Module Pattern**: Combina con IIFE per dettagli privati

## 🔗 Concetti Correlati

- [[hiding-in-scope|Hiding in Scope]] - Principio generale
- [[scope-window|Variabili Globali e window]] - Scope globale
- [[../../appunti-completi#namespace-globali-global-namespaces|Namespace Completo]]

## 📚 Risorse

- Module Pattern (JavaScript Design Patterns)
- "You Don't Know JS" - Scope & Closures

## 📌 Tag

#javascript #scope #namespace #design-patterns #global-scope #module-pattern #libraries
