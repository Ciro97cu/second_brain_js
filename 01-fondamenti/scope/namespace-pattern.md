# [[../../appunti-completi#namespace-globali-global-namespaces|Namespace Pattern]]

Un **namespace** è un contenitore (solitamente un oggetto) che raggruppa le funzionalità di una libreria o di un modulo sotto un unico nome globale. Questo approccio previene l'inquinamento dello scope globale e riduce il rischio di conflitti tra identificatori.

Il pattern prevede l'utilizzo di una singola variabile globale per applicazione o libreria, definendo tutte le funzionalità come proprietà e metodi di tale oggetto.

## Problema: Inquinamento dello Scope Globale

La definizione di variabili e funzioni direttamente nello scope globale può portare a conflitti, specialmente quando si utilizzano più librerie.

```javascript
// Libreria 1
function helper() {
  /* ... */
}
var version = "1.0";

// Libreria 2 (Sovrascrive gli identificatori precedenti)
function helper() {
  /* ... */
}
var version = "2.0";
```

## Soluzione: Oggetto Namespace

L'utilizzo di un oggetto come namespace risolve il problema dei conflitti.

```javascript
// Definizione del namespace per la prima libreria
var MyLibrary = {
  version: "1.0",
  helper: function () {
    console.log("Helper di MyLibrary");
  },
};

// Definizione del namespace per la seconda libreria
var AnotherLibrary = {
  version: "2.0",
  helper: function () {
    console.log("Helper di AnotherLibrary");
  },
};

// Nessun conflitto
MyLibrary.helper(); // "Helper di MyLibrary"
AnotherLibrary.helper(); // "Helper di AnotherLibrary"
```

## Esempi nel Mondo Reale

Molte librerie JavaScript popolari utilizzano il pattern del namespace per esporre le proprie API:

```javascript
// jQuery espone le funzionalità sull'oggetto 'jQuery' o '$'
jQuery.ajax({
  /* ... */
});

// Lodash utilizza l'oggetto '_'
_.map(array, fn);

// React espone le proprie API sull'oggetto 'React'
React.createElement("div", null, "Hello");
```

## Vantaggi

1. **Prevenzione dei conflitti**: L'occupazione di un solo nome nello scope globale minimizza il rischio di collisioni.
2. **Organizzazione**: Le funzionalità vengono raggruppate in modo logico e strutturato.
3. **Chiarezza dell'API**: L'accesso ai metodi tramite il namespace (es. `Libreria.metodo()`) rende il codice più esplicito sulla provenienza della funzionalità.
