# [[../../appunti-completi#il-processo-di-ricerca-look-up-nello-scope-lessicale|Look-up nelle Bolle di Scope]]

Il **processo di look-up** cerca le variabili partendo dalla bolla più interna e risalendo verso le bolle esterne.

## 🎯 Concetto Chiave

L'Engine cerca le variabili con una **ricerca a risalita**: inizia dalla bolla corrente e sale di livello in livello finché trova la variabile o raggiunge lo scope globale.

### Ricerca Multi-Livello

```javascript
function foo(a) {
  let b = a * 2;

  function bar(c) {
    // Engine cerca 'a':
    // 1. Bolla bar → ❌ Non trovato
    // 2. Bolla foo → ✅ Trovato! (a = 2)

    // Engine cerca 'b':
    // 1. Bolla bar → ❌ Non trovato
    // 2. Bolla foo → ✅ Trovato! (b = 4)

    // Engine cerca 'c':
    // 1. Bolla bar → ✅ Trovato! (c = 12)

    console.log(a, b, c); // 2 4 12
  }

  bar(b * 3);
}

foo(2);
```

La ricerca si **ferma alla prima corrispondenza**.

## 💻 Esempio Pratico Complesso

```javascript
let tassa = 0.22; // Bolla 1: Globale

function calcolaPrezzoFinale(prezzoBase) {
  // Bolla 2
  let margine = 0.3;

  function applicaTassa() {
    // Bolla 3

    // Look-up per 'prezzoBase':
    // Bolla 3 → ❌ | Bolla 2 → ✅ Trovato!
    let prezzoConMargine = prezzoBase * (1 + margine);

    // Look-up per 'tassa':
    // Bolla 3 → ❌ | Bolla 2 → ❌ | Bolla 1 → ✅ Trovato!
    let prezzoFinale = prezzoConMargine * (1 + tassa);

    return prezzoFinale;
  }

  return applicaTassa();
}

console.log(calcolaPrezzoFinale(100)); // 158.6
```

## ⚠️ Shadowing: Prima Corrispondenza

Quando una bolla interna ha un identificatore con lo stesso nome di una bolla esterna, la ricerca si **ferma alla prima corrispondenza**.

```javascript
function foo(a) {
  let b = a * 2;

  function bar(c) {
    let a = 100; // ⚠️ Shadows il parametro 'a' di foo

    // Look-up per 'a':
    // 1. Bolla bar → ✅ Trovato: a = 100
    // (Non arriva mai alla bolla foo dove a = 2)

    console.log(a, b, c); // 100 4 12 (non 2 4 12)
  }

  bar(b * 3);
}

foo(2);
```

### Shadowing Multi-Livello

```javascript
let x = "Globale";

function livello1() {
  let x = "Livello 1"; // Shadows globale

  function livello2() {
    let x = "Livello 2"; // Shadows livello1 e globale

    // Look-up per 'x':
    // 1. Bolla livello2 → ✅ Trovato: "Livello 2"
    console.log(x); // "Livello 2"
  }

  livello2();
  console.log(x); // "Livello 1" (usa il SUO x)
}

livello1();
console.log(x); // "Globale" (usa il SUO x)
```

## 🔍 Look-up Passo-Passo

```javascript
// Visualizza il processo di ricerca
let config = { api: "v1" }; // Bolla: Globale

function init() {
  let versione = "2.0"; // Bolla: init

  function start() {
    let debug = true; // Bolla: start

    // Look-up per 'debug':
    // start → ✅ Trovato subito!
    console.log("Debug:", debug);

    // Look-up per 'versione':
    // start → ❌ | init → ✅ Trovato!
    console.log("Versione:", versione);

    // Look-up per 'config':
    // start → ❌ | init → ❌ | Globale → ✅ Trovato!
    console.log("API:", config.api);

    // Look-up per 'inesistente':
    // start → ❌ | init → ❌ | Globale → ❌
    // console.log(inesistente); // ❌ ReferenceError
  }

  start();
}

init();
```

## ✅ Best Practices

**Comprendi l'ordine di ricerca**: Sempre dall'interno verso l'esterno.

```javascript
// ✅ Chiaro: sa dove cercare
function calcola(x) {
  let fattore = 2;

  function moltiplica() {
    return x * fattore; // Chiaro che vengono da scope esterni
  }

  return moltiplica();
}
```

**Evita shadowing non intenzionale**: Usa nomi diversi.

```javascript
// ❌ Shadowing confuso
function outer() {
  let count = 10;

  function inner() {
    let count = 5; // Shadows (confuso!)
    console.log(count); // Quale count?
  }
}

// ✅ Nomi distinti
function outer() {
  let totalCount = 10;

  function inner() {
    let localCount = 5; // Chiaro!
    console.log(totalCount, localCount);
  }
}
```

**Minimizza i livelli di look-up**: Per performance e chiarezza.

```javascript
// ❌ Look-up profondo
function a() {
  let x = 10;
  function b() {
    function c() {
      function d() {
        console.log(x); // Look-up attraverso 4 livelli
      }
    }
  }
}

// ✅ Più diretto
function a() {
  let x = 10;
  function b() {
    console.log(x); // Look-up attraverso 2 livelli
  }
}
```

## 🔗 Collegamenti

- [[scope-bubbles]] - Visualizzazione bolle scope
- [[lexical-scope-base]] - Scope lessicale base
- [[scope-chain]] - Catena degli scope
- [[scope-errors]] - ReferenceError quando fallisce

## 📌 Note Aggiuntive

- La ricerca procede sempre dall'**interno verso l'esterno**
- Si ferma alla **prima corrispondenza** (shadowing)
- Se non trova nulla, genera **ReferenceError**
- Il look-up è determinato **lessicalmente** (dalla posizione nel codice)
