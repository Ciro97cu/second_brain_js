# [[../../appunti-completi#gestione-dei-moduli-module-management|Module Management: Concetto e Scope Privati]]

I **moduli** rappresentano l'evoluzione moderna dei namespace in JavaScript. Invece di fare affidamento su una o più variabili globali, ogni file viene trattato come un modulo indipendente con uno **scope privato** per default. 

Gli identificatori necessari vengono **esplicitamente importati** solo dove servono, eliminando alla radice il problema dell'inquinamento dello scope globale.

Il principio fondamentale è l'assenza di identificatori globali, l'uso di import ed export espliciti e una vera privacy dei dati all'interno del modulo.

## Scope Privati Automatici

All'interno di un modulo, tutto ciò che non viene esplicitamente esportato rimane privato e inaccessibile dall'esterno.

```javascript
// === math-utils.js ===
// Tutto è privato per default
const PI = 3.14159; // Variante privata
let cache = {}; // Variabile privata

function arrotonda(num) {
  // Funzione non esportata, quindi privata
  return Math.round(num * 100) / 100;
}

// Solo le funzioni esportate diventano accessibili all'esterno
export function calcolaArea(raggio) {
  return arrotonda(PI * raggio * raggio);
}
```

Quando il modulo viene importato, solo le parti pubbliche sono visibili:

```javascript
// === app.js ===
import { calcolaArea } from "./math-utils.js";

calcolaArea(5); // ✅ OK
// PI // ❌ ReferenceError - la variabile è veramente privata
// arrotonda(3.14) // ❌ ReferenceError - la funzione è privata
```

## Pattern di Moduli

Esistono due pattern principali per la gestione dei moduli: CommonJS (classico di Node.js) e ES6 Modules (lo standard moderno).

### ES6 Modules (Standard Moderno)

Il sistema ES6 utilizza le keyword `export` e `import`.

```javascript
// === libreria.js ===
export function funzione1() {
  /* ... */
}
export function funzione2() {
  /* ... */
}

// Esportazione di default
export default { funzione1, funzione2 };

// === app.js ===
import { funzione1, funzione2 } from "./libreria.js";
funzione1(); // Eseguita nello scope locale del modulo, zero inquinamento globale

// Oppure importando l'intero namespace
import * as lib from "./libreria.js";
lib.funzione1();
```

### CommonJS (Node.js Classico)

Il sistema CommonJS utilizza `module.exports` e `require()`.

```javascript
// === libreria.js ===
function funzione1() {
  /* privata o da esportare */
}
function funzione2() {
  /* ... */
}

// Esporta esplicitamente ciò che deve essere pubblico
module.exports = {
  funzione1,
  funzione2,
};

// === app.js ===
const libreria = require("./libreria");
libreria.funzione1(); // Viene utilizzata nello scope locale
```
