# [[../../appunti-completi#hoisting|Hoisting delle Funzioni]]

## 🎯 Concetto

Le **function declarations** in JavaScript vengono **hoisted completamente** (dichiarazione + corpo), a differenza delle variabili dove viene hoisted solo la dichiarazione. Questo permette di chiamare una funzione prima che sia stata definita nel codice.

Le **function expressions**, invece, seguono le regole dell'hoisting delle variabili: solo la variabile viene hoisted, non il corpo della funzione.

**Importante**: Questo riguarda solo le funzioni. Per l'hoisting delle variabili (`var`, `let`, `const`), vedi [[../variabili/hoisting|Hoisting delle Variabili]].

## 💻 Function Declarations (Hoisted Completamente)

### Chiamare Prima di Dichiarare

Le **function declarations** vengono hoisted **completamente** (dichiarazione + corpo):

```javascript
// Codice scritto
foo(); // "Hello!" - Funziona!

function foo() {
  console.log("Hello!");
}

// Come viene eseguito dal motore
function foo() {
  // TUTTA la funzione hoisted in cima
  console.log("Hello!");
}

foo(); // "Hello!"
```

**Motivo**: Durante la fase di compilazione, l'intera funzione viene processata e spostata in cima al suo scope.

### Hoisting in Scope Annidati

```javascript
function outer() {
  inner(); // ✅ Funziona (inner hoisted nello scope di outer)

  function inner() {
    console.log("Inner function");
  }
}

outer(); // "Inner function"
```

## 🚫 Function Expressions (Solo Variabile Hoisted)

### Il Problema con le Function Expressions

Le **function expressions** seguono le regole delle variabili: solo la **dichiarazione della variabile** viene hoisted, **non il corpo della funzione**.

```javascript
// Codice scritto
foo(); // ❌ TypeError: foo is not a function

var foo = function () {
  console.log("Hello!");
};

// Come viene eseguito
var foo; // Solo dichiarazione hoisted
foo(); // TypeError (foo è undefined, non una funzione)

foo = function () {
  // Assegnazione rimane qui
  console.log("Hello!");
};
```

**Errore comune**: Si ottiene `TypeError` (non `ReferenceError`) perché `foo` esiste ma contiene `undefined`, e cercare di eseguire `undefined` come funzione genera `TypeError`.

### Con let/const

```javascript
bar(); // ❌ ReferenceError: Cannot access 'bar' before initialization

const bar = function () {
  console.log("Hello!");
};

// let/const hanno Temporal Dead Zone (TDZ)
```

## 📛 Named Function Expressions

Anche le **named function expressions** seguono le regole delle variabili:

```javascript
// Codice scritto
bar(); // ❌ TypeError: bar is not a function

var bar = function foo() {
  console.log("Hello!");
};

// Come viene eseguito
var bar; // Solo 'bar' hoisted
bar(); // TypeError

bar = function foo() {
  // Assegnazione
  console.log("Hello!");
};
```

**Nota**: Il nome `foo` è accessibile **solo all'interno della funzione**:

```javascript
var bar = function foo() {
  console.log(typeof foo); // "function" (accessibile qui)
};

bar();
console.log(typeof foo); // "undefined" (non accessibile fuori)
```

## ⚖️ Funzioni vs Variabili: Chi Vince?

### Le Funzioni Hanno la Precedenza

Quando c'è un conflitto di nome tra una **function declaration** e una dichiarazione di variabile, la **funzione vince**:

```javascript
// Codice scritto
console.log(foo); // [Function: foo]

var foo = 2;

function foo() {
  console.log("Hello!");
}

console.log(foo); // 2

// Come viene eseguito
function foo() {
  // Function declaration hoisted PRIMA
  console.log("Hello!");
}
var foo; // Dichiarazione ignorata (foo già dichiarato)

console.log(foo); // [Function: foo]
foo = 2; // Assegnazione SOVRASCRIVE
console.log(foo); // 2
```

**Regola**: Le function declarations hanno la precedenza sulle dichiarazioni `var`, ma le **assegnazioni** vengono eseguite normalmente.

### Ordine di Hoisting

1. **Function declarations** - Hoisted per prime
2. **Dichiarazioni variabili** - Se il nome esiste già (da funzione), vengono ignorate
3. **Assegnazioni** - Eseguite nell'ordine originale

## 🔄 Dichiarazioni Duplicate

### Più Function Declarations con Stesso Nome

Quando ci sono **più function declarations con lo stesso nome**, l'**ultima sovrascrive le precedenti**:

```javascript
foo(); // "3"

function foo() {
  console.log("1");
}

var foo = function () {
  console.log("2");
};

function foo() {
  console.log("3");
}

// Come viene eseguito
function foo() {
  // Prima function declaration
  console.log("1");
}
function foo() {
  // Seconda function declaration SOVRASCRIVE
  console.log("3");
}
var foo; // Ignorata (foo già dichiarato come funzione)

foo(); // "3"

foo = function () {
  // Assegnazione sovrascrive tutto
  console.log("2");
};
```

### Perché l'Ultima Vince

```javascript
foo(); // "B"

function foo() {
  console.log("A");
}

function foo() {
  console.log("B");
}

// Durante hoisting, la seconda foo sovrascrive la prima
```

## 🚨 Function Declarations nei Blocchi

### Comportamento Inaffidabile

Le **function declarations all'interno di blocchi** (`if`, `while`, blocchi arbitrari) hanno un **comportamento storico inaffidabile** e **NON STANDARD**.

```javascript
// ⚠️ COMPORTAMENTO INAFFIDABILE - DA EVITARE
console.log(foo); // Dipende dall'engine!

if (true) {
  function foo() {
    console.log("Hello!");
  }
}

foo(); // Potrebbe funzionare o no, dipende dall'implementazione
```

### Il Problema

Storicamente, le function declarations dentro blocchi vengono hoisted allo **scope racchiudente** (funzione o globale), **ignorando il blocco**:

```javascript
function test(condition) {
  // foo viene hoisted qui (scope della funzione)

  if (condition) {
    function foo() {
      return "A";
    }
  } else {
    function foo() {
      return "B";
    }
  }

  return foo(); // ⚠️ Quale foo? Dipende dall'engine!
}
```

### Comportamento Non Standard

Il comportamento varia tra:

- **Browser legacy**: Hoisting allo scope della funzione racchiudente
- **ES6+ strict mode**: Block scope (come `let`)
- **Modalità non-strict**: Comportamento confuso e imprevedibile

```javascript
// In modalità NON-strict (legacy)
if (false) {
  function foo() {
    console.log("Never executed");
  }
}

foo(); // ⚠️ Potrebbe funzionare o generare ReferenceError!

// In strict mode (ES6+)
("use strict");

if (false) {
  function foo() {
    console.log("Never executed");
  }
}

foo(); // ❌ ReferenceError: foo is not defined (block-scoped)
```

### Regola d'Oro

**NON dichiarare funzioni dentro blocchi**. Questo meccanismo è considerato **inaffidabile** e soggetto a cambiamenti nelle future specifiche del linguaggio.

### Alternative Sicure

```javascript
// ✅ SOLUZIONE 1: Function expression con let/const
function test(condition) {
  let foo;

  if (condition) {
    foo = function () {
      return "A";
    };
  } else {
    foo = function () {
      return "B";
    };
  }

  return foo();
}

// ✅ SOLUZIONE 2: Dichiarazione fuori dal blocco
function test(condition) {
  function fooA() {
    return "A";
  }

  function fooB() {
    return "B";
  }

  return condition ? fooA() : fooB();
}

// ✅ SOLUZIONE 3: Arrow function (ES6+)
function test(condition) {
  const foo = condition ? () => "A" : () => "B";

  return foo();
}

// ✅ SOLUZIONE 4: Operatore ternario con chiamate
function test(condition) {
  function fooA() {
    return "A";
  }

  function fooB() {
    return "B";
  }

  return (condition ? fooA : fooB)();
}
```

## 📊 Confronto Rapido

| Tipo                                | Dichiarazione Hoisted      | Corpo Hoisted | Chiamabile Prima    |
| ----------------------------------- | -------------------------- | ------------- | ------------------- |
| **Function Declaration**            | ✅                         | ✅            | ✅                  |
| **Function Expression (var)**       | ✅ (undefined)             | ❌            | ❌ (TypeError)      |
| **Function Expression (let/const)** | ❌ (TDZ)                   | ❌            | ❌ (ReferenceError) |
| **Arrow Function**                  | Segue regole var/let/const | ❌            | ❌                  |

## ⚠️ Problemi Comuni

### TypeError vs ReferenceError

```javascript
// TypeError - variabile esiste ma non è funzione
foo(); // ❌ TypeError: foo is not a function
var foo = function () {};

// ReferenceError - variabile in TDZ
bar(); // ❌ ReferenceError: Cannot access 'bar' before initialization
let bar = function () {};

// Funziona - function declaration hoisted
baz(); // ✅ "Hello!"
function baz() {
  console.log("Hello!");
}
```

### Named Function Expression Confusion

```javascript
var myFunc = function namedFunc() {
  console.log(typeof namedFunc); // "function" (accessibile qui)
};

myFunc();
console.log(typeof namedFunc); // "undefined" (NON accessibile fuori!)

// namedFunc(); // ❌ ReferenceError: namedFunc is not defined
```

## ✅ Best Practices

1. **Usa function declarations per funzioni "pubbliche"** - Possono essere chiamate ovunque nello scope
2. **Usa function expressions per funzioni "private" o condizionali** - Più controllo su quando esistono
3. **Dichiara le funzioni prima di usarle** - Migliore leggibilità, anche se non necessario
4. **NON dichiarare funzioni dentro blocchi** - Comportamento inaffidabile
5. **Usa const per function expressions** - Previene riassegnazioni accidentali
6. **Preferisci arrow functions per callback** - Più concise e lexical `this`

## 🔗 Concetti Correlati

- [[../variabili/hoisting|Hoisting delle Variabili]] - var, let, const e TDZ
- [[lexical-scope-base|Scope Lessicale]] - Come funziona lo scope
- [[let-const-block-scope|Block Scope]] - let e const in blocchi
- [[../../appunti-completi#hoisting|Hoisting Completo]]

## 📚 Risorse

- MDN: Function Hoisting
- MDN: Function Declarations vs Expressions
- "You Don't Know JS" - Scope & Closures, Chapter 4

## 📌 Tag

#javascript #functions #hoisting #function-declarations #function-expressions #scope #compilation #tdz #arrow-functions
