# [[../../appunti-completi#gestione-dei-moduli-module-management|Gestione dei Moduli (Module Management)]]

## 🎯 Concetto

I **moduli** sono l'evoluzione moderna dei namespace. Invece di una singola variabile globale, ogni file è un modulo con **scope privato** per default. Gli identificatori vengono **esplicitamente importati** dove servono, eliminando completamente l'inquinamento dello scope globale.

**Principio Chiave**: Nessun identificatore globale, import/export espliciti, vera privacy.

## 💻 Pattern di Moduli

### CommonJS (Node.js Classico)

```javascript
// === libreria.js ===
function funzione1() {
  /* privata */
}
function funzione2() {
  /* privata */
}

// Esporta solo ciò che serve
module.exports = {
  funzione1,
  funzione2,
};

// === app.js ===
const libreria = require("./libreria");
libreria.funzione1(); // Import esplicito in scope locale
```

### ES6 Modules (Standard Moderno)

```javascript
// === libreria.js ===
export function funzione1() {
  /* ... */
}
export function funzione2() {
  /* ... */
}

// O export default
export default { funzione1, funzione2 };

// === app.js ===
import { funzione1, funzione2 } from "./libreria.js";
funzione1(); // Scope locale, zero pollution globale

// O import namespace
import * as lib from "./libreria.js";
lib.funzione1();
```

## 💡 Scope Privati Automatici

```javascript
// === math-utils.js ===
// TUTTO è privato per default
const PI = 3.14159; // Privato
let cache = {}; // Privato

function arrotonda(num) {
  // Privato (non esportato)
  return Math.round(num * 100) / 100;
}

// Solo funzioni esportate sono accessibili
export function calcolaArea(raggio) {
  return arrotonda(PI * raggio * raggio);
}

// === app.js ===
import { calcolaArea } from "./math-utils.js";
calcolaArea(5); // ✅ OK
// PI // ❌ ReferenceError - veramente privato!
// arrotonda(3.14) // ❌ ReferenceError - veramente privato!
```

## 🔄 Namespace vs Moduli

### Namespace (Vecchio)

```javascript
var App = {
  _privateHelper: function () {
    /* ... */
  }, // Convenzione, ma accessibile
  publicMethod: function () {
    /* ... */
  },
};

App._privateHelper(); // ⚠️ Funziona (nessuna vera privacy)
```

### Moduli (Moderno)

```javascript
// === utils.js ===
function privateHelper() {
  /* veramente privato */
}
export function publicMethod() {
  privateHelper();
}

// === app.js ===
import { publicMethod } from "./utils.js";
publicMethod(); // ✅ OK
// privateHelper(); // ❌ ReferenceError (vera privacy!)
```

## 🎯 Import con Alias (Prevenzione Collisioni)

```javascript
// === math.js ===
export function add(a, b) {
  return a + b;
}

// === app.js ===
// Due librerie con stessa funzione 'add'
import { add as mathAdd } from "./math.js";
import { add as stringAdd } from "./string-utils.js";

mathAdd(2, 3); // 5
stringAdd("hello", "world"); // 'helloworld'
// NO conflitti!
```

## ⚡ Vantaggi dei Moduli

1. **Vera Privacy**: Non solo convenzioni, incapsulamento reale
2. **Zero Global Pollution**: Nessun identificatore globale
3. **Dipendenze Esplicite**: Import chiaro di ciò che serve
4. **Prevenzione Collisioni**: Automatica tramite scope separati
5. **Tree Shaking**: Bundler rimuovono codice non usato
6. **Code Splitting**: Caricamento lazy di moduli
7. **Manutenibilità**: Dipendenze chiare e tracciabili

## 📦 Dependency Managers

```javascript
// package.json
{
  "dependencies": {
    "lodash": "^4.17.21",
    "axios": "^1.0.0"
  }
}

// app.js
import _ from 'lodash';
import axios from 'axios';

// Librerie in scope locale, NO globali!
const raddoppiati = _.map([1, 2, 3], n => n * 2);
```

## 🏗️ Struttura Applicazione Modulare

```javascript
// config.js → api-client.js → user-service.js → app.js
// Ogni modulo importa solo ciò che serve
// Scope privati a ogni livello
// Nessuna variabile globale in tutta l'app
```

## ⚠️ Scope Lessicale, Non Magia

I moduli **non violano** le regole dello scope lessicale. Semplicemente:

- Ogni file è una funzione che crea uno scope privato
- `export` rende accessibili identificatori specifici
- `import` li porta in uno scope locale (non globale)
- Il resto rimane privato per sempre

## 🔗 Concetti Correlati

- [[scope-namespaces|Namespace Globali]] - Pattern precedente
- [[hiding-in-scope|Hiding in Scope]] - Principio generale
- [[lexical-scope-base|Scope Lessicale]] - Meccanismo sottostante
- [[../../appunti-completi#gestione-dei-moduli-module-management|Module Management Completo]]

## 📚 Risorse

- MDN: JavaScript Modules
- ES6 Modules Specification
- CommonJS vs ES Modules

## 📌 Tag

#javascript #modules #scope #es6 #commonjs #import-export #encapsulation #dependency-management #tree-shaking
