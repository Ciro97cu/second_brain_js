# [[../../appunti-completi#scope-lessicale-lexical-scope|Scope Lessicale (Lexical Scope)]]

Lo **scope lessicale** determina l'accesso alle variabili in base a **dove il codice è scritto** (author-time), non dove viene eseguito (run-time).

## 🎯 Concetto Chiave

JavaScript usa lo **scope lessicale**: lo scope di una funzione è determinato dalla sua **posizione nel codice sorgente**, non da dove o come viene invocata. Questa struttura è definita durante la fase di **lexing** (compilazione) e rimane immutabile.

### Author-Time vs Run-Time

```javascript
// Scope determinato da DOVE è SCRITTA la funzione
let messaggio = "Globale";

function mostraMessaggio() {
  // Questa funzione è SCRITTA nello scope globale
  console.log(messaggio);
}

function test() {
  let messaggio = "Locale";
  mostraMessaggio(); // "Globale" (non "Locale")
}

test();
// mostraMessaggio() cerca 'messaggio' dove è STATA DEFINITA (globale),
// NON dove viene CHIAMATA (test)
```

## 💻 Le Bolle di Scope

Ogni blocco di codice crea una **"bolla di scope"** che può contenere altre bolle più piccole.

```javascript
// BOLLE ANNIDATE
function foo(a) {
  // Bolla 2: contiene a, b, bar
  let b = a * 2;

  function bar(c) {
    // Bolla 3: contiene c
    console.log(a, b, c); // Accede a tutte e 3 le bolle
  }

  bar(b * 3);
}

foo(2); // Bolla 1: contiene foo
```

**Regola fondamentale**: Una bolla è sempre **interamente contenuta** in un'altra, mai parzialmente.

### Il Processo di Look-up

L'Engine cerca le variabili partendo dalla **bolla più interna** e risalendo verso l'esterno:

```javascript
function foo(a) {
  let b = a * 2;

  function bar(c) {
    // Cerca 'a': Bolla bar → ❌ | Bolla foo → ✅ Trovato!
    // Cerca 'b': Bolla bar → ❌ | Bolla foo → ✅ Trovato!
    // Cerca 'c': Bolla bar → ✅ Trovato!
    console.log(a, b, c); // 2 4 12
  }

  bar(b * 3);
}

foo(2);
```

La ricerca si **ferma alla prima corrispondenza**.

## 🔍 Lexical vs Dynamic Scope

JavaScript usa **solo** lexical scope (la maggior parte dei linguaggi moderni).

```javascript
let valore = "globale";

function mostraValore() {
  console.log(valore);
}

function test() {
  let valore = "locale";
  mostraValore(); // Cosa stampa?
}

test();
// LEXICAL SCOPE (JavaScript): "globale"
// → mostraValore() è DEFINITA nello scope globale

// DYNAMIC SCOPE (ipotetico): "locale"
// → mostraValore() è CHIAMATA da test()
```

## ⚠️ Distinzioni Importanti

### Scope Lessicale vs Proprietà Oggetti

La ricerca dello scope si applica **solo al primo identificatore**.

```javascript
let obj = {
  livello1: {
    valore: 42,
  },
};

function test() {
  // SCOPE LESSICALE: cerca 'obj' (trova nello scope esterno)
  // PROPRIETÀ OGGETTO: accede a 'livello1' e 'valore'
  console.log(obj.livello1.valore); // 42
}

test();
```

**Differenza chiave**:

- Variabile non trovata → **ReferenceError** (scope lessicale)
- Proprietà non trovata → **undefined** (accesso oggetto)

```javascript
let obj = { x: 10 };

// console.log(variabileNonEsiste);  // ❌ ReferenceError (scope)
console.log(obj.proprietaNonEsiste); // undefined (proprietà)
```

### Variabili Globali e `window`

Le variabili globali dichiarate con `var` sono proprietà di `window` (in browser).

```javascript
var globalVar = "Globale";

function test() {
  var globalVar = "Locale"; // Shadows

  console.log(globalVar); // "Locale"
  console.log(window.globalVar); // "Globale" (bypass shadowing)
}

test();
```

⚠️ Questo **non funziona** per variabili non globali o per `let`/`const`.

## ✅ Best Practices

**Comprendi la struttura lessicale**: Visualizza le "bolle" annidate quando leggi il codice.

```javascript
// Chiara gerarchia di scope
function esterna() {
  let x = 10; // Scope esterna

  function interna() {
    // Scope interna, può accedere a 'x'
    console.log(x);
  }

  return interna;
}
```

**Evita di modificare lo scope a runtime**: Non usare `eval()` o `with` (deprecati e pericolosi).

```javascript
// ❌ EVITA (modifica scope a runtime)
eval("var x = 10"); // Crea 'x' dinamicamente

// ✅ PREFERISCI (scope statico)
let x = 10; // Dichiarazione esplicita lessicale
```

**Sfrutta le closures**: Lo scope lessicale è la base delle closures.

```javascript
function creaContatore() {
  let count = 0; // Scope lessicale di creaContatore

  return function () {
    // 'incrementa' ricorda il SUO scope lessicale
    count++;
    return count;
  };
}

let contatore = creaContatore();
console.log(contatore()); // 1
console.log(contatore()); // 2
```

**Distingui scope da proprietà**: Ricorda che `obj.prop` usa regole diverse da `variabile`.

```javascript
let config = { host: "localhost" };

function usa() {
  // 'config' → scope lessicale
  // 'host' → proprietà oggetto
  console.log(config.host);
}
```

## 🔗 Collegamenti

- [[scope-chain]] - Catena degli scope annidata
- [[nested-scope]] - Scope annidati in pratica
- [[scope]] - Concetti base scope
- [[../funzioni/closures]] - Closures e scope lessicale

## 📚 Risorse Esterne

- [MDN: Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) - Scope lessicale nelle closures
- [YDKJS: Scope](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch1.md) - Approfondimento scope lessicale

## 📌 Note Aggiuntive

- Lo **scope lessicale** è anche chiamato **static scope** (statico, determinato alla compilazione)
- Il 99.9% dei linguaggi moderni usa lexical scope (C, Java, Python, JavaScript, ecc.)
- **Dynamic scope** è usato solo in linguaggi rari (Bash, alcuni Lisp dialects)
- Le tecniche per modificare lo scope a runtime (`eval`, `with`) sono deprecate e causano problemi di performance
- Lo scope lessicale è **immutabile** dopo la fase di parsing
