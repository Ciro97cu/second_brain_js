# [[../../appunti-completi#38-funzioni-functions|IIFE (Immediately Invoked Function Expressions)]]

Una **IIFE** (pronunciata "iffy") è un'Espressione di Funzione Invocata Immediatamente: una funzione dichiarata ed eseguita subito dopo la creazione.

## Sintassi

```javascript
// IIFE base
(function () {
  console.log("Eseguita immediatamente!");
})();

// Struttura: (espressione di funzione)(chiamata)
//            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^  ^^

// IIFE con nome (per debug)
(function iife() {
  console.log("IIFE con nome");
})();

// Sintassi alternativa
(function () {
  console.log("Sintassi alternativa");
})();
```

## Scopo Principale: Scope Privato

Le variabili dentro una IIFE sono **private** e non inquinano lo scope globale.

```javascript
// ❌ Senza IIFE - variabile globale
var contatore = 0;

// ✅ Con IIFE - scope privato
(function () {
  var contatore = 0; // privato
  function incrementa() {
    contatore++;
    console.log(contatore);
  }
  incrementa(); // 1
})();

// console.log(contatore);  // ❌ ReferenceError
```

Pattern fondamentale prima di `let`/`const` per evitare variabili globali accidentali con `var`.

## Pattern Module

```javascript
let modulo = (function () {
  // Variabili private
  let contatore = 0;
  let segreto = "password";

  // API pubblica
  return {
    incrementa: function () {
      contatore++;
    },
    getValue: function () {
      return contatore;
    },
  };
})();

modulo.incrementa();
console.log(modulo.getValue()); // 1
console.log(modulo.segreto); // undefined (privato)
```

## IIFE con Parametri e Return

```javascript
// Con parametri
(function (nome, eta) {
  console.log(nome, eta);
})("Mario", 30);

// Con return per inizializzazione
const risultato = (function () {
  let moltiplicatore = 5;
  let valoreBase = 10;
  return moltiplicatore * valoreBase;
})();

console.log(risultato); // 50
// moltiplicatore e valoreBase non esistono più

// Configurazione complessa
const config = (function () {
  let ambiente = "produzione";
  let apiUrl =
    ambiente === "sviluppo"
      ? "http://localhost:3000"
      : "https://api.production.com";

  return {
    ambiente,
    apiUrl,
    version: "1.0.0",
  };
})();
```

## IIFE e Closure: Una Precisazione

È doveroso fare una precisazione riguardo al pattern IIFE. Spesso si cita l'IIFE come esempio di Closure, ma secondo una definizione rigorosa, non è esattamente così.

```javascript
var a = 2;

(function IIFE() {
  console.log(a); // 2
})();
```

Sebbene questo codice funzioni, **non è un'osservazione diretta della Closure**. Perché? Perché la funzione IIFE non viene eseguita al di fuori del suo Lexical Scope. Viene invocata esattamente nello stesso scope in cui è stata dichiarata. La variabile `a` viene trovata tramite le normali regole di lookup del Lexical Scope, non tramite Closure.

Anche se l'IIFE in sé non è un esempio di Closure osservata (è come un albero che cade nella foresta senza nessuno che lo senta), essa **crea uno scope**, ed è uno degli strumenti più comuni per **creare scope su cui altre funzioni potranno poi effettuare una Closure**.

## Collegamenti

- [[funzioni]] - Concetti base delle funzioni
- [[../sintassi/blocchi]] - IIFE crea scope di blocco funzione
- [[../variabili/variabili]] - Differenza var vs let/const con IIFE
- [[../scope/scope]] - IIFE per scope privato
