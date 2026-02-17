# Strict Mode ("Modalità Stretta")

**Tipo**: Best Practice

**Appunti Completi**: [[../../appunti-completi#29-strict-mode]]

Introdotta in **ECMAScript 5 (ES5)**, la **strict mode** attiva regole più restrittive per il codice JavaScript. L'obiettivo è rendere il codice più **sicuro**, **robusto** e meno incline a errori, trasformando "errori silenziosi" in errori espliciti.

## Perché Usare Strict Mode

✅ **Sicurezza** → Previene pratiche rischiose (variabili globali accidentali)
✅ **Ottimizzazione** → Codice più facile da ottimizzare
✅ **Futuro** → Direzione evolutiva del linguaggio

## Come Attivare lo Strict Mode

Inserisci `"use strict";` all'inizio di un **file** (globale) o di una **funzione** (locale).

### A Livello di File

```javascript
"use strict";

// Tutto il file è in strict mode
let nome = "Mario";
x = 10; // ❌ ReferenceError: x is not defined
```

### A Livello di Funzione

```javascript
function modalitaStretta() {
  "use strict";
  y = 5; // ❌ ReferenceError
}

function modalitaNormale() {
  z = 10; // ✅ Crea globale (sconsigliato)
}
```

## Principali Regole Introdotte

### 1. Impedisce Variabili Globali Accidentali

```javascript
"use strict";

function test() {
  messaggio = "Ciao"; // ❌ ReferenceError
  let messaggio2 = "Ciao"; // ✅ OK
}
```

### 2. Parametri Duplicati Vietati

```javascript
"use strict";

function somma(a, a, c) {
  // ❌ SyntaxError
  return a + a + c;
}
```

### 3. Proprietà Read-Only Non Modificabili

```javascript
"use strict";

let obj = {};
Object.defineProperty(obj, "x", { value: 42, writable: false });
obj.x = 9; // ❌ TypeError (silenzioso in non-strict)
```

### 4. Elimina `this` Globale in Funzioni

```javascript
"use strict";

function mostraThis() {
  console.log(this); // undefined (non window!)
}

mostraThis();
```

### 5. Parole Riservate per il Futuro

```javascript
"use strict";

let implements = 5; // ❌ SyntaxError
let interface = {}; // ❌ SyntaxError
// Riservate: implements, interface, let, package, private, protected, public, static, yield
```

## Strict Mode nei Moduli ES6

**I moduli ES6 sono automaticamente in strict mode**, non serve dichiararlo:

```javascript
// file: modulo.js
// Già in strict mode automaticamente

export function test() {
  x = 10; // ❌ ReferenceError
}
```

## Riepilogo

Lo **strict mode** è una **best practice** essenziale:

- Usa `"use strict";` all'inizio di file o funzioni
- Sempre attivo nei **moduli ES6**
- Trasforma errori silenziosi in errori espliciti
- Rende il codice più sicuro e manutenibile

## Collegamenti

- [[../funzioni/this]] - This è undefined in strict mode
- [[../variabili/dichiarazione]] - Variabili devono essere dichiarate
- [[statement]] - Regole sintattiche più rigide
