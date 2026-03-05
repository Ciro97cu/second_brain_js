# [[../../appunti-completi#confusione-2-this-come-riferimento-allo-scope-lessicale|Confusione: this come Riferimento allo Scope Lessicale]]

Il secondo equivoco comune è pensare che `this` si riferisca in qualche modo allo scope lessicale della funzione. È una questione complicata perché in un certo senso c'è un fondo di verità, ma in un altro senso è completamente fuorviante.

## 🎯 Concetti Chiave

- **`this` NON si riferisce allo scope lessicale** di una funzione
- `this` e lexical scope sono **meccanismi completamente separati**
- Lo "scope object" esiste internamente nell'engine ma **non è accessibile** al codice JavaScript
- **Non esiste ponte** tra lookup lessicale e binding di `this`

## 💻 Il Problema: Tentativo di Attraversare lo Scope

### Codice che Fallisce

```javascript
function foo() {
  var a = 2;
  this.bar(); // ❌ Tentativo di chiamare bar() via this
}

function bar() {
  console.log(this.a); // ❌ Tentativo di accedere a 'a' via this
}

foo(); // undefined (o ReferenceError in strict mode)
```

**Cosa lo sviluppatore pensava**:

1. `this.bar()` chiamerebbe la funzione `bar()`
2. `this.a` in `bar()` accedrebbe alla variabile `a` dello scope di `foo()`
3. `this` creerebbe un "ponte" tra gli scope di `foo()` e `bar()`

**Cosa succede realmente**:

1. `this.bar()` funziona **per caso** (se `bar` è nel global object)
2. `this.a` cerca `a` nel global object, non nello scope di `foo()`
3. Non esiste alcun ponte - `this` punta al global object (default binding)

### Spiegazione Dettagliata

**Errore 1: `this.bar()`**

```javascript
function foo() {
  this.bar(); // Cerca bar come proprietà di 'this'
}

function bar() {
  /* ... */
}

foo();
```

- In chiamata diretta `foo()`, `this` = global object
- `this.bar()` diventa `window.bar()` (in browser)
- Se `bar` è nel global scope, viene trovata **per caso**
- **Modo corretto**: Semplicemente `bar()` (lexical reference)

**Errore 2: Accesso a variabile tramite `this`**

```javascript
function foo() {
  var a = 2; // Variabile nello scope di foo
  /* ... */
}

function bar() {
  console.log(this.a); // Cerca 'a' come proprietà di 'this'
}
```

- La variabile `a` esiste solo nello scope lessicale interno di `foo()`
- `this.a` cerca una proprietà `a` sull'oggetto puntato da `this`
- **Non può mai** accedere alla variabile locale `a` di un'altra funzione
- Non importa come imposti `this` - le variabili locali sono inaccessibili

## ⚠️ Perché NON Esiste il Ponte

### Scope Lessicale: Meccanismo 1

```javascript
function outer() {
  var x = 10;

  function inner() {
    console.log(x); // Accesso lessicale - funziona ✅
  }

  inner();
}
```

**Caratteristiche**:

- Determinato **al momento della scrittura** (author-time)
- Closure su scope esterno
- Accesso via **identificatori** (nomi di variabili)
- Chain di scope (`[[Scope]]` interno)

### this Binding: Meccanismo 2

```javascript
function foo() {
  console.log(this.value);
}

var obj = { value: 42, foo: foo };

obj.foo(); // Binding di this - funziona ✅
```

**Caratteristiche**:

- Determinato **al momento della chiamata** (call-time)
- Punta a un oggetto in base al call-site
- Accesso via **proprietà** dell'oggetto
- Regole di binding (default, implicit, explicit, new)

### I Due Meccanismi Sono Separati

```javascript
function outer() {
  var x = 10;

  return function inner() {
    // Lexical scope: accede a 'x' ✅
    console.log(x);

    // this binding: accede a proprietà di 'this' ✅
    console.log(this.value);

    // Non può usare 'this' per accedere a 'x' ❌
    // console.log(this.x); // undefined
  };
}

var obj = {
  value: 42,
  fn: outer(),
};

obj.fn(); // 10, 42
```

## 💡 Lo Scope Object (Interno)

### Cosa Esiste Internamente

Nell'implementazione del JavaScript Engine, lo scope è rappresentato come una sorta di "oggetto":

```javascript
// Rappresentazione INTERNA (non accessibile)
ScopeObject {
  a: 2,
  b: 3,
  myFunc: function() { /* ... */ }
}
```

### Perché NON è Accessibile

```javascript
function foo() {
  var a = 2;

  // ❌ Non puoi fare questo:
  // console.log(scopeObject.a);
  // console.log(this.scopeObject.a);

  // ✅ Puoi solo fare questo:
  console.log(a); // Lookup lessicale normale
}
```

Lo "scope object" è una **struttura dati interna** dell'engine, non un vero oggetto JavaScript accessibile.

## ✅ Soluzioni Corrette

### Soluzione 1: Lexical Scope (Closure)

```javascript
function foo() {
  var a = 2;

  bar(); // Chiamata lessicale semplice

  function bar() {
    console.log(a); // Closure su scope di foo ✅
  }
}

foo(); // 2
```

**Quando usare**: Quando hai bisogno di accedere a variabili di scope esterno.

### Soluzione 2: this Binding (Oggetti)

```javascript
var obj = {
  a: 2,

  foo: function () {
    this.bar(); // Chiamata metodo via this ✅
  },

  bar: function () {
    console.log(this.a); // Accesso proprietà via this ✅
  },
};

obj.foo(); // 2
```

**Quando usare**: Quando lavori con proprietà di oggetti, non variabili locali.

### Soluzione 3: Passare Parametri

```javascript
function foo() {
  var a = 2;
  bar(a); // Passa esplicitamente il valore
}

function bar(value) {
  console.log(value); // Usa parametro ✅
}

foo(); // 2
```

**Quando usare**: Quando funzioni diverse devono condividere dati.

## 📊 Confronto Meccanismi

| Feature         | Lexical Scope            | this Binding              |
| --------------- | ------------------------ | ------------------------- |
| Determinato     | Author-time (scrittura)  | Call-time (esecuzione)    |
| Accede a        | Variabili locali/esterne | Proprietà di oggetti      |
| Sintassi        | Identificatore (`x`)     | Membro (`this.x`)         |
| Meccanismo      | Closure, scope chain     | Call-site, regole binding |
| Modificabile    | No (fisso)               | Sì (call/apply/bind)      |
| Ponte tra i due | **NON ESISTE**           | **NON ESISTE**            |

## 🔗 Collegamenti

**Prerequisiti**:

- [[this-concept]] - Comprendere cos'è this
- [[../scope/lexical-scope-base]] - Scope lessicale
- [[../scope/closures]] - Closure

**Concetti Correlati**:

- [[this-confusion-itself]] - L'altra confusione comune
- [[this-binding-rules]] - Come funziona this veramente

**Approfondimenti**:

- [[../scope/scope-chain]] - Come funziona la scope chain
- [[../avanzate/execution-context]] - Context vs Scope

## 📚 Riferimenti

- **You Don't Know JS**: this & Object Prototypes - Chapter 1 "Its Scope"
- **You Don't Know JS**: Scope & Closures - Chapter 2
- **MDN**: [Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
- **MDN**: [this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)

## 📌 Note Personali

[Annotazioni sulla confusione "this e scope"]

---

**Tags**: `#javascript` `#this` `#confusioni` `#lexical-scope` `#closure` `#separation-of-concerns`
