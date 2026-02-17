# Scope Chain (Catena degli Scope)

**Appunti Completi**: [[../../appunti-completi#44-scope-ambito]]

La **scope chain** è il meccanismo che permette al codice di cercare variabili risalendo attraverso scope annidati.

## Scope Annidati

Scope possono essere **annidati** gerarchicamente. Scope lessicale: codice interno accede scope esterni.

```javascript
let a = "globale";

function esterna() {
  let b = "esterna";

  function interna() {
    let c = "interna";

    console.log(a); // ✅ Accessibile (scope globale)
    console.log(b); // ✅ Accessibile (scope esterna)
    console.log(c); // ✅ Accessibile (scope corrente)
  }

  interna();
  console.log(a); // ✅ Accessibile
  // console.log(c);  // ❌ ReferenceError
}

esterna();
// console.log(b);  // ❌ ReferenceError
```

`interna` vede tutto (a, b, c). `esterna` vede solo (a, b). Globale vede solo a.

## Meccanismo Scope Chain

JavaScript cerca variabili con **ricerca a risalita**:

1. Cerca nello **scope corrente**
2. Se non trova, sale allo **scope esterno**
3. Ripete fino a **scope globale**
4. Se non trova, genera **ReferenceError**

```javascript
let x = 10; // Globale

function livello1() {
  let y = 20; // Scope livello1

  function livello2() {
    let z = 30; // Scope livello2

    // Cerca z: trovato qui (livello2)
    console.log(z); // 30

    // Cerca y: non qui, risale a livello1
    console.log(y); // 20

    // Cerca x: non qui, non livello1, risale a globale
    console.log(x); // 10

    // Cerca w: non trovato in nessun scope
    // console.log(w);  // ❌ ReferenceError: w is not defined
  }

  livello2();
}

livello1();
```

## ReferenceError

**ReferenceError** si verifica quando si tenta di accedere a variabile non disponibile nello scope corrente né in scope esterni.

```javascript
function test() {
  // console.log(inesistente);  // ❌ ReferenceError
}

if (true) {
  let x = 10;
}
// console.log(x);  // ❌ ReferenceError (fuori block scope)
```

## Pericolo: Variabili Globali Accidentali

Un comportamento **pericoloso** di JavaScript (in modalità non-stretta) si verifica quando si assegna un valore a una variabile **non dichiarata** con `var`, `let` o `const`.

```javascript
function esempio() {
  x = 10; // ❌ Nessuna dichiarazione (var/let/const)
  // JavaScript risale la scope chain fino in cima
  // Non trova 'x' dichiarata da nessuna parte
  // Crea AUTOMATICAMENTE 'x' nello scope globale
}

esempio();
console.log(x); // 10 (variabile globale accidentale!)
```

JavaScript risale la catena degli scope fino in cima e, non trovando alcuna dichiarazione, **crea automaticamente una nuova variabile nello scope globale**.

### Perché è Pericoloso

Questa è una **pessima pratica** perché:

**Inquinamento scope globale**: variabili globali involontarie

**Bug difficili da tracciare**: parti diverse del codice modificano la stessa variabile globale

**Conflitti di nomi**: sovrascrittura accidentale di variabili esistenti

```javascript
let x = 100; // Variabile globale intenzionale

function funzioneA() {
  x = 200; // ✅ OK, modifica x globale (intenzionale)
}

function funzioneB() {
  y = 50; // ❌ Crea y globale (accidentale!)
}

funzioneA();
console.log(x); // 200

funzioneB();
console.log(y); // 50 (variabile globale accidentale)
```

### Soluzione: Strict Mode

**Regola fondamentale**: dichiara sempre formalmente le variabili con `let`, `const` o `var`.

Lo **strict mode** (`"use strict"`) previene questo problema trasformando assegnamenti non dichiarati in **errori**.

```javascript
"use strict";

function test() {
  x = 10; // ❌ ReferenceError: x is not defined
  // Strict mode impedisce la creazione automatica
}

// Soluzione corretta
function test() {
  let x = 10; // ✅ Dichiarazione esplicita
}
```

## Shadowing (Variabili Ombra)

Lo **shadowing** si verifica quando una variabile dichiarata in uno **scope locale** ha lo stesso nome di una variabile in uno **scope più esterno**. In questo caso, la variabile locale **"nasconde"** o **"mette in ombra"** (shadows) quella esterna.

All'interno dello scope locale, qualsiasi riferimento a quel nome di variabile utilizzerà la **versione locale**.

```javascript
let x = 10; // Scope globale

function esempio() {
  let x = 20; // Scope locale, "shadows" la x globale

  console.log(x); // 20 (usa la x locale)
}

esempio();
console.log(x); // 10 (usa la x globale)
```

### Shadowing Annidato

Lo shadowing può verificarsi a **più livelli**:

```javascript
let nome = "Globale";

function esterna() {
  let nome = "Esterna"; // Shadows globale
  console.log(nome); // "Esterna"

  function interna() {
    let nome = "Interna"; // Shadows esterna (e globale)
    console.log(nome); // "Interna"
  }

  interna();
  console.log(nome); // "Esterna" (non modificata)
}

esterna();
console.log(nome); // "Globale" (non modificata)
```

### Shadowing con Blocchi

Anche i blocchi `{}` con `let`/`const` creano shadowing:

```javascript
let x = 100;

if (true) {
  let x = 200; // Shadows x esterna
  console.log(x); // 200
}

console.log(x); // 100
```

**Importante**: Non puoi ri-dichiarare la stessa variabile con `let`/`const` nello stesso scope, ma puoi farlo in scope diversi (shadowing).

```javascript
let y = 10;
// let y = 20;  // ❌ SyntaxError: già dichiarata

{
  let y = 20; // ✅ OK, diverso scope (shadowing)
}
```

## Collegamenti

- [[scope]] - Concetti base scope
- [[../variabili/variabili]] - Scope delle variabili, dichiarazione formale
- [[../funzioni/funzioni]] - Funzioni creano scope annidati
- [[../sintassi/blocchi]] - Block scope e annidamento
