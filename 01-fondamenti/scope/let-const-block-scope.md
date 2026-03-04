# [[../../appunti-completi#blocchi-come-scope-blocks-as-scopes|let e const: Block Scope Moderno]]

## 🎯 Concetto

Un **blocco** è una qualsiasi porzione di codice racchiusa tra parentesi graffe `{ ... }`. JavaScript moderno (ES6+) supporta il **block scope** con `let` e `const`, dove le variabili dichiarate in un blocco sono confinate a quel blocco e non visibili all'esterno.

**Prima di ES6**: Solo `var` (function scope, ignora i blocchi)  
**Da ES6 in poi**: `let` e `const` (true block scope)

**Vantaggio**: Estende il **Principio del Minimo Privilegio**, permettendo di nascondere le informazioni all'interno di singoli blocchi di codice.

## 💻 Il Problema con var: Falso Block Scope

### Apparenza Ingannevole

```javascript
// Sembra block scope, ma NON lo è!
for (var i = 0; i < 5; i++) {
  // 'i' sembra confinata al loop...
  console.log(i);
}

console.log(i); // 5 - ⚠️ 'i' è ancora accessibile!
// 'i' appartiene allo scope della funzione (o globale), NON al blocco for
```

La variabile `i` viene dichiarata nell'intestazione del `for`, con l'intenzione di usarla solo nel ciclo. Tuttavia, a causa del **function scope** di `var`, la variabile appartiene allo scope che la contiene (funzione o globale), non al ciclo.

### Falso Block Scope nel Blocco if

```javascript
function foo(bar) {
  if (bar) {
    var baz = bar * 2; // Dichiarata con 'var'
    console.log(baz);
  }

  // ⚠️ 'baz' è accessibile qui!
  console.log(baz); // Valore o undefined (se if non eseguito)
}

foo(5); // 10, 10
foo(false); // undefined

// 'baz' viene dichiarata nel blocco if, ma è visibile in TUTTA la funzione
```

Questo è **falso block scope**: `baz` è dichiarata nel blocco `if`, ma con `var` la sua validità si estende a tutto lo scope della funzione. Questo si basa sull'**autodisciplina** dello sviluppatore per non riutilizzare `baz` altrove.

### Perché è Problematico

```javascript
function esempio() {
  var risultato = "iniziale";

  if (true) {
    var risultato = "modificato nel blocco"; // ⚠️ SOVRASCRIVE quella esterna!
  }

  console.log(risultato); // "modificato nel blocco"
  // Ci si aspetterebbe "iniziale", ma var non rispetta i blocchi
}

esempio();
```

**Problema**: Senza block scope gli sviluppatori possono riutilizzare accidentalmente le variabili al di fuori del loro scopo previsto, causando bug difficili da tracciare.

## 🔐 try...catch: Il Primo Block Scope (ES3)

### Block Scope Storico

È un fatto poco noto che JavaScript, già a partire dalla **specifica ES3**, ha introdotto una forma di block scope per la variabile dichiarata nella clausola `catch` di un blocco `try...catch`.

```javascript
try {
  undefined(); // Genera un errore
} catch (err) {
  console.log(err); // TypeError: undefined is not a function
  // 'err' esiste SOLO in questo blocco
}

console.log(err); // ❌ ReferenceError: err is not defined
// 'err' NON è accessibile fuori dal blocco catch
```

La variabile `err` esiste **solo ed esclusivamente** all'interno del blocco `catch`.

### Linter e Variabili catch Duplicate

```javascript
try {
  operazione1();
} catch (err) {
  console.log("Errore 1:", err);
}

try {
  operazione2();
} catch (err) {
  // ⚠️ Alcuni linter segnalano errore
  console.log("Errore 2:", err);
}

// Tecnicamente NON è una ridefinizione (sono scope separati)
// Ma alcuni linter eccessivamente zelanti lo segnalano
```

**Soluzione per linter aggressivi**:

- Usare nomi diversi: `err1`, `err2`
- Disabilitare la regola di linting per nomi duplicati
- O ignorare l'avviso (è safe)

## ✨ let: Block Scope Moderno (ES6+)

### Attaccare Variabili ai Blocchi

ES6 ha introdotto la parola chiave `let` come alternativa a `var`. **let "attacca" la dichiarazione di una variabile allo scope di qualsiasi blocco** in cui è contenuta.

```javascript
var foo = true;

if (foo) {
  let bar = foo * 2;
  console.log(bar); // 2
}

console.log(bar); // ❌ ReferenceError: bar is not defined
// 'bar' esiste SOLO dentro il blocco if
```

La variabile `bar`, dichiarata con `let`, esiste solo all'interno del blocco `if`. Qualsiasi tentativo di accedervi dall'esterno risulta in un `ReferenceError`.

### let nei Cicli for

```javascript
// Con var: problematico
for (var i = 0; i < 5; i++) {
  setTimeout(function () {
    console.log(i); // Stampa sempre 5!
  }, 100);
}
// Problema: 'i' è condivisa, alla fine vale 5

// Con let: corretto
for (let j = 0; j < 5; j++) {
  setTimeout(function () {
    console.log(j); // Stampa 0, 1, 2, 3, 4
  }, 100);
}
// 'j' è RICREATA ad ogni iterazione con block scope
```

Con `let`, **ogni iterazione del loop ha la propria copia della variabile**, risolvendo il problema classico delle closures nei cicli.

### Rebinding per Iterazione

L'uso di `let` nell'intestazione del ciclo non si limita a legare la variabile al corpo del ciclo. In realtà, **ri-lega (rebinds) la variabile a ogni singola iterazione**, assicurandosi di riassegnarle il valore che aveva alla fine dell'iterazione precedente.

```javascript
for (let i = 0; i < 5; i++) {
  console.log(i);
}

// Dietro le quinte, è come se il codice funzionasse così:
{
  let i = 0;
  if (i < 5) {
    console.log(i);
    i++;
  }
}
{
  let i = 1; // Nuovo binding con valore precedente
  if (i < 5) {
    console.log(i);
    i++;
  }
}
{
  let i = 2; // Nuovo binding con valore precedente
  if (i < 5) {
    console.log(i);
    i++;
  }
}
// ... e così via fino a i = 5
```

Questo **rebinding automatico** è ciò che permette alle closures nei loop di funzionare correttamente con `let`, cosa impossibile con `var`.

### Qualsiasi Blocco { ... }

```javascript
// Blocco in un if
if (true) {
  let x = 10;
  console.log(x); // 10
}
// console.log(x); // ❌ ReferenceError

// Blocco in un while
let count = 0;
while (count < 3) {
  let messaggio = `Iterazione ${count}`;
  console.log(messaggio);
  count++;
}
// console.log(messaggio); // ❌ ReferenceError

// Blocco arbitrario (standalone)
{
  let privato = "segreto";
  console.log(privato); // "segreto"
}
// console.log(privato); // ❌ ReferenceError
```

## 🔒 const: Block Scope Immutabile

### const per Valori che Non Cambiano

`const` funziona come `let`, ma crea **binding immutabili** (non può essere riassegnato):

```javascript
const PI = 3.14159;
console.log(PI); // 3.14159

PI = 3.14; // ❌ TypeError: Assignment to constant variable

// Anche const ha block scope
if (true) {
  const MESSAGE = "Hello";
  console.log(MESSAGE); // "Hello"
}
// console.log(MESSAGE); // ❌ ReferenceError
```

### const non Significa "Immutabile"

`const` impedisce la **riassegnazione**, ma NON rende l'oggetto immutabile:

```javascript
const obj = { nome: "Mario" };

// ✅ Posso modificare le proprietà
obj.nome = "Luigi";
obj.eta = 30;
console.log(obj); // { nome: "Luigi", eta: 30 }

// ❌ NON posso riassegnare
obj = { nome: "Peach" }; // TypeError: Assignment to constant variable

// Stesso per array
const arr = [1, 2, 3];
arr.push(4); // ✅ OK
arr[0] = 10; // ✅ OK
console.log(arr); // [10, 2, 3, 4]

arr = [5, 6]; // ❌ TypeError
```

### const nei Cicli for

```javascript
// ❌ ERRORE con for classico (i viene riassegnato)
for (const i = 0; i < 5; i++) {
  // TypeError
  console.log(i);
}

// ✅ OK con for...of (ogni iterazione ha nuovo binding)
const arr = [10, 20, 30];
for (const value of arr) {
  console.log(value); // 10, 20, 30
}

// ✅ OK con for...in
const obj = { a: 1, b: 2 };
for (const key in obj) {
  console.log(key, obj[key]); // "a" 1, "b" 2
}
```

## ⚠️ Temporal Dead Zone (TDZ)

### Differenza da var (Hoisting)

A differenza di `var`, le variabili `let` e `const` **non sono accessibili prima della dichiarazione**:

```javascript
console.log(a); // undefined (hoisting di var)
var a = 10;

console.log(b); // ❌ ReferenceError: Cannot access 'b' before initialization
let b = 20;

console.log(c); // ❌ ReferenceError: Cannot access 'c' before initialization
const c = 30;
```

### Cos'è la TDZ

La **Temporal Dead Zone** è il periodo tra l'inizio del blocco e la dichiarazione della variabile:

```javascript
{
  // TDZ inizia qui per 'x'

  console.log(x); // ❌ ReferenceError (in TDZ)

  let x = 10; // TDZ finisce qui

  console.log(x); // ✅ 10
}
```

### TDZ e typeof

```javascript
// Con variabile non dichiarata
console.log(typeof variabileNonEsiste); // "undefined" (safe)

// Con let in TDZ
console.log(typeof x); // ❌ ReferenceError (in TDZ!)
let x = 10;

// typeof fallisce con let/const in TDZ
```

### Perché Esiste la TDZ

La TDZ **previene errori** obbligando a dichiarare prima di usare:

```javascript
// Errore logico con var (hoisting nasconde bug)
var totale = calcolaTotale(); // undefined passato (bug!)

function calcolaTotale() {
  return prezzoBase + tassa; // NaN
}

var prezzoBase = 100;
var tassa = 10;

// Con let: errore esplicito
let totale = calcolaTotale(); // ❌ ReferenceError immediato!

function calcolaTotale() {
  return prezzoBase + tassa;
}

let prezzoBase = 100;
let tassa = 10;
```

## 🚫 Ridichiarazione Vietata

### let e const non Permettono Ridichiarazioni

```javascript
var x = 10;
var x = 20; // ✅ OK con var (silenziosamente sovrascrive)

let y = 10;
let y = 20; // ❌ SyntaxError: Identifier 'y' has already been declared

const z = 10;
const z = 20; // ❌ SyntaxError: Identifier 'z' has already been declared
```

### Nello Stesso Scope

```javascript
function esempio() {
  let x = 10;
  let x = 20; // ❌ SyntaxError
}

// Ma in scope DIVERSI è OK (shadowing)
let x = 10;

{
  let x = 20; // ✅ OK, scope diverso (shadowing)
  console.log(x); // 20
}

console.log(x); // 10
```

### var vs let nello Stesso Scope

```javascript
var a = 10;
let a = 20; // ❌ SyntaxError

let b = 10;
var b = 20; // ❌ SyntaxError

// Non puoi mescolare var e let con stesso nome nello stesso scope
```

## 📦 Blocchi Espliciti per Chiarezza

### Blocchi Impliciti vs Espliciti

Usare `let` per legare una variabile a un blocco pre-esistente può essere **implicito**. Per maggiore chiarezza, si possono creare **blocchi espliciti**:

```javascript
// Approccio IMPLICITO (blocco pre-esistente)
if (foo) {
  let bar = foo * 2; // 'bar' legato al blocco if
  // ...
}

// Approccio ESPLICITO (blocco dedicato)
if (foo) {
  {
    // Blocco esplicito per 'bar'
    let bar = foo * 2;
    console.log(bar);
  }

  // 'bar' NON esiste qui
  // console.log(bar); // ReferenceError
}
```

**Vantaggi**:

- ✅ Più chiaro dove le variabili sono confinate
- ✅ Più facile spostare il blocco durante refactoring
- ✅ Non altera la semantica dell'`if` che lo contiene

### Pattern per Variabili Temporanee

```javascript
function processData(data) {
  // Blocco esplicito per calcoli intermedi
  {
    let temp = data * 2;
    let adjusted = temp + 10;
    data = adjusted;
  }

  // 'temp' e 'adjusted' non inquinano questo scope
  // console.log(temp); // ❌ ReferenceError

  return data;
}
```

## ✅ Best Practices

1. **Usa `const` per default** - Se non devi riassegnare, usa `const`
2. **Usa `let` solo quando necessario riassegnare** - Più esplicito nell'intento
3. **Evita `var`** - Ha troppi comportamenti contro-intuitivi
4. **Confina le variabili ai blocchi più piccoli possibili** - Principio del Minimo Privilegio
5. **Crea blocchi espliciti** per variabili temporanee importanti
6. **Dichiara variabili prima dell'uso** - Evita confusione con TDZ

## 🔗 Concetti Correlati

- [[lexical-scope-base|Scope Lessicale]] - Scope determinato a compile-time
- [[nested-scope|Scope Annidato]] - Scope chain e lookup gerarchico
- [[block-scope-memory|Block Scope e Memory]] - Ottimizzazione GC con blocchi
- [[../variabili/hoisting|Hoisting delle Variabili]] - Come var/let/const vengono hoisted
- [[function-hoisting|Hoisting delle Funzioni]] - Come le funzioni vengono hoisted
- [[../../appunti-completi#blocchi-come-scope-blocks-as-scopes|Blocchi come Scope Completo]]

## 📚 Risorse

- MDN: Block Statements
- MDN: let vs var
- MDN: const
- "You Don't Know JS" - Scope & Closures, Chapter 3

## 📌 Tag

#javascript #scope #block-scope #let #const #var #es6 #tdz #hoisting #temporal-dead-zone #refactoring
