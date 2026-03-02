# [[../../appunti-completi#variabili-globali-e-loggetto-window|Oggetto Globale: window]]

Le variabili globali dichiarate con `var` diventano **proprietà dell'oggetto globale** (`window` in browser).

## 🎯 Concetto Chiave

L'oggetto **globale** (`window` in browser, `global` in Node.js) è un oggetto speciale che contiene le variabili globali dichiarate con `var`.

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

## 💻 Bypass dello Shadowing

Puoi "bypassare" lo shadowing di variabili **globali** dichiarate con `var` usando `window`.

```javascript
var varGlobale = "Sono globale";

function test() {
  var varGlobale = "Sono locale"; // Shadows

  console.log(varGlobale); // "Sono locale" (scope locale)
  console.log(window.varGlobale); // "Sono globale" (bypass shadowing)
}

test();
```

⚠️ **Limitazione**: Funziona **solo** per variabili globali con `var`, non per `let`/`const`.

### Non Funziona con let/const

```javascript
let globaleLet = "let globale";

function test() {
  let globaleLet = "let locale"; // Shadows

  console.log(globaleLet); // "let locale"
  console.log(window.globaleLet); // undefined (NON funziona)
  // Non c'è modo di accedere alla 'globaleLet' originale
}

test();
```

## ⚠️ Non Funziona per Variabili Non Globali

```javascript
function esterna() {
  var x = 10;

  function interna() {
    var x = 20; // Shadows

    console.log(x); // 20
    console.log(window.x); // undefined (x non è globale)
    // console.log(esterna.x); // ❌ Non esiste

    // La x di 'esterna' è INACCESSIBILE qui dentro
  }

  interna();
}

esterna();
```

## 🌐 Oggetto Globale in Ambienti Diversi

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

```javascript
// globalThis è disponibile ovunque
var x = 10;

console.log(globalThis.x); // 10 (browser)
console.log(globalThis.x); // 10 (Node.js)
console.log(globalThis.x); // 10 (Web Worker)
```

## 🚫 Inquinamento dello Scope Globale

```javascript
// ❌ var inquina window
var config = { api: "..." };
console.log(window.config); // { api: "..." }

function test() {
  // Potenziale conflitto con window.config
  console.log(config); // Ambiguo
}

// ✅ let/const NON inquinano window
let config2 = { api: "..." };
console.log(window.config2); // undefined (nessun inquinamento)
```

### Rischio di Conflitti

```javascript
// ❌ PERICOLOSO: Sovrascrivere API native
var alert = function () {
  console.log("Custom alert");
};

// Ora window.alert è sovrascritto!
alert("test"); // Custom alert (non l'alert nativo)
```

## ✅ Best Practices

**Usa let/const invece di var**: Evita inquinamento di window.

```javascript
// ❌ EVITA
var globale = 10;
console.log(window.globale); // 10 (inquinamento)

// ✅ PREFERISCI
let globale = 10;
console.log(window.globale); // undefined (nessun inquinamento)
```

**Non usare window per bypassare shadowing**: Cattiva pratica.

```javascript
// ❌ EVITA (confuso e fragile)
var x = 10;
function test() {
  var x = 20;
  console.log(window.x); // 10 (perché??)
}

// ✅ PREFERISCI nomi diversi
let globaleX = 10;
function test() {
  let localeX = 20;
  console.log(globaleX); // 10 (chiaro!)
}
```

**Usa globalThis per codice portabile**: Funziona ovunque.

```javascript
// ✅ Portabile tra browser e Node.js
globalThis.myGlobal = "valore";

// Funziona in browser, Node.js, Web Workers, etc.
console.log(globalThis.myGlobal);
```

**Minimizza le variabili globali**: Usa moduli o IIFE.

```javascript
// ❌ EVITA variabili globali
var config = {};
var utils = {};

// ✅ PREFERISCI moduli o namespace
const App = {
  config: {},
  utils: {},
};

// O usa moduli ES6
// export const config = {};
// export const utils = {};
```

## 🔗 Collegamenti

- [[scope-vs-properties]] - Differenza scope vs proprietà
- [[lexical-scope-base]] - Scope lessicale base
- [[scope-errors]] - Variabili globali accidentali
- [[../variabili/variabili]] - var vs let vs const

## 📚 Risorse Esterne

- [MDN: window](https://developer.mozilla.org/en-US/docs/Web/API/Window) - Oggetto globale window
- [MDN: globalThis](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/globalThis) - Standard universale

## 📌 Note Aggiuntive

- Solo `var` globale crea proprietà di `window`
- `let`/`const` globali NON sono in `window`
- `globalThis` è lo standard universale (ES2020+)
- Evita inquinamento di `window` con variabili globali
- Il bypass dello shadowing con `window` è una cattiva pratica
