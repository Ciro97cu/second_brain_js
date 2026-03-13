# [[../../appunti-completi#variabili-globali-e-loggetto-window|Oggetto Globale: window e globalThis]]

Le variabili globali dichiarate con `var` diventano **proprietà dell'oggetto globale** (`window` nei browser).

## 🎯 Concetto Chiave

L'oggetto **globale** (`window` nei browser, `global` in Node.js) è un oggetto speciale che contiene le variabili globali dichiarate con `var`.

### var vs let/const

```javascript
var globalVar = "Globale con var";
let globalLet = "Globale con let";
const globalConst = "Globale con const";

console.log(window.globalVar); // "Globale con var" (✅ è in window)
console.log(window.globalLet); // undefined (❌ NON è in window)
console.log(window.globalConst); // undefined (❌ NON è in window)
```

**Differenza fondamentale**:

- `var` globale → **proprietà di window**
- `let`/`const` globale → **NON proprietà di window**

## 🌐 Oggetto Globale in Ambienti Diversi

L'accesso all'oggetto globale varia a seconda dell'ambiente di esecuzione:

```javascript
// BROWSER
console.log(window); // ✅ Oggetto globale nel browser
console.log(this === window); // true (nello scope globale)

// NODE.JS
// console.log(global); // ✅ Oggetto globale in Node.js

// UNIVERSALE (ES2020+)
console.log(globalThis); // ✅ Funziona ovunque
```

### globalThis: Standard Universale

Dallo standard ES2020, `globalThis` fornisce un modo standard per accedere all'ambiente globale trasversalmente a diversi ambienti JS.

```javascript
// globalThis è disponibile ovunque
var x = 10;

console.log(globalThis.x); // 10 (browser)
console.log(globalThis.x); // 10 (Node.js)
console.log(globalThis.x); // 10 (Web Worker)
```

## 📌 Note Aggiuntive

- Solo `var` globale crea proprietà di `window`.
- `let`/`const` globali non sono presenti in `window`.
- `globalThis` è lo standard universale raccomandato (ES2020+) per riferirsi all'oggetto globale.
