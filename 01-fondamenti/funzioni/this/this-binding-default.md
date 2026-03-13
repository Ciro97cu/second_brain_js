# [[../../../appunti-completi#311-lidentificatore-this|Default Binding (Regola 1)]]

La **default binding** è la prima regola del binding di `this` e rappresenta il caso più comune: l'invocazione standalone di una funzione senza contesto specifico.

## 🎯 Concetti Chiave

- **Regola catch-all**: Si applica quando nessuna delle altre regole (implicit, explicit, new) è applicabile
- **Plain function call**: Chiamata diretta senza decorazioni (`foo()`)
- **Global object**: In non-strict mode, `this` punta al global object
- **Strict mode**: In strict mode, `this` è `undefined`
- **Precedenza**: Priorità più bassa delle quattro regole

## 💻 Quando Si Applica

**Quando**: Chiamata diretta di funzione standalone (plain, undecorated function reference)

```javascript
function foo() {
  console.log(this.a);
}

var a = 2;

foo(); // 2 (this = global object in non-strict mode)
```

## 📋 Concetti Fondamentali

### 1. Variabili Globali = Proprietà Global Object

`var a = 2` nello scope globale crea una proprietà sul global object. Non sono copie, **sono la stessa cosa** (due facce della stessa moneta).

```javascript
var a = 42;

console.log(window.a); // 42 (browser)
console.log(this.a); // 42 (global scope)
console.log(a); // 42

// Sono tutti la stessa proprietà!
```

### 2. Plain Function Call

`foo()` è chiamata con un riferimento semplice, senza decorazioni:

- ❌ No `.call()` o `.apply()`
- ❌ No `obj.foo()` (implicit binding)
- ❌ No `new foo()` (new binding)

→ Quindi si applica la default binding.

### 3. this Punta al Global Object

In questo caso `this` punta a:

- `window` in browser
- `global` in Node.js

```javascript
function foo() {
  console.log(this === window); // true (browser)
}

foo();
```

## ⚠️ Strict Mode

**In strict mode**, il global object **non è eleggibile** per la default binding. `this` diventa `undefined`:

```javascript
function foo() {
  "use strict";
  console.log(this); // undefined
  console.log(this.a); // TypeError: Cannot read 'a' of undefined
}

var a = 2;

foo(); // TypeError
```

### Dettaglio Importante: Dove Conta lo Strict Mode

⚠️ **Regola sottile**: Il global object è eleggibile per la default binding **solo se il contenuto della funzione NON è in strict mode**.

Lo strict mode **del call-site è irrilevante**:

```javascript
function foo() {
  // NON strict mode qui
  console.log(this.a);
}

var a = 2;

(function () {
  "use strict";

  foo(); // 2 (il call-site è strict, ma foo() no!)
})();
```

**Spiegazione**: Anche se il call-site è in strict mode, `this` è ancora il global object perché **il corpo di `foo()` stesso** non è strict.

**Caso inverso**:

```javascript
function foo() {
  "use strict";
  console.log(this); // undefined
}

var a = 2;

// Call-site NON strict
foo(); // undefined (conta solo il corpo di foo)
```

## 📝 Mixing Strict/Non-Strict

📝 **Best Practice**: Generalmente sconsigliato mescolare strict e non-strict nello stesso programma.

L'intero programma dovrebbe essere:

- ✅ Tutto strict, OPPURE
- ✅ Tutto non-strict

**Eccezione**: Librerie di terze parti possono avere diverso livello di strictness. Fare attenzione a questi dettagli di compatibilità.

## 💻 Esempi Completi

### Esempio Base

```javascript
function mostraNome() {
  console.log(this.nome);
}

var nome = "Mario";

mostraNome(); // "Mario"
```

### Con Oggetti (NO Default Binding)

```javascript
function foo() {
  console.log(this.a);
}

var a = "global";

var obj = {
  a: "oggetto",
  foo: foo,
};

obj.foo(); // "oggetto" (implicit binding, NON default!)
foo(); // "global" (default binding)
```

### Strict Mode Completo

```javascript
"use strict";

function foo() {
  console.log(this); // undefined
}

var a = "global";

foo(); // undefined (non è possibile accedere a this.a)

// Errore se provi ad accedere a proprietà
function bar() {
  "use strict";
  return this.a; // TypeError!
}

// bar(); // ❌ TypeError: Cannot read 'a' of undefined
```

### Mixed Mode (Sconsigliato)

```javascript
// Funzione non-strict
function nonStrict() {
  console.log("Non-strict:", this.a);
}

// Funzione strict
function strict() {
  "use strict";
  console.log("Strict:", this); // undefined
}

var a = 42;

nonStrict(); // "Non-strict: 42"
strict(); // "Strict: undefined"
```

## ⚠️ Gotcha

### Confusione con let/const

```javascript
let a = 2; // ⚠️ let NON crea proprietà su global object

function foo() {
  console.log(this.a); // undefined!
}

foo();
```

Solo `var` in global scope crea proprietà su global object. `let` e `const` no!

### IIFE e Default Binding

```javascript
var a = "global";

(function () {
  console.log(this.a); // "global" (default binding)
})();

(function () {
  "use strict";
  console.log(this); // undefined
})();
```

## ✅ Best Practices

1. **Usa sempre strict mode** per evitare binding accidentali al global object
2. **Evita di fare affidamento sulla default binding** - rende il codice imprevedibile
3. **Se serve il global object**, passalo esplicitamente come parametro
4. **Non mescolare strict/non-strict** nello stesso file

## 🔗 Collegamenti

**Prerequisiti**:

- [[this-concept]] - Comprendere cos'è this
- [[../funzioni]] - Funzioni JavaScript base

**Regole Correlate**:

- [[this-binding-implicit]] - Implicit binding (regola 2)
- [[this-binding-explicit]] - Explicit binding (regola 3)
- [[this-binding-new]] - New binding (regola 4)
- [[this-binding-precedence]] - Ordine di precedenza delle regole

**Approfondimenti**:

- [[../../scope/strict-mode]] - Strict mode in dettaglio
- [[../../scope/lexical-scope-base]] - Scope lessicale vs this

## 📚 Riferimenti

- **You Don't Know JS**: this & Object Prototypes - Chapter 2
- **MDN**: [this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
- **MDN**: [Strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)

## 📌 Note Personali

[Spazio per annotazioni personali sulla default binding]

---

**Tags**: `#javascript` `#this` `#default-binding` `#global-object` `#strict-mode`
