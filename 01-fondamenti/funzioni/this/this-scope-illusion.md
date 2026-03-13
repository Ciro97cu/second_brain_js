# [[../../../appunti-completi#confusione-2-this-come-riferimento-allo-scope-lessicale|This: L'Illusione dello Scope]]

Un equivoco comune è credere che `this` si riferisca in qualche modo allo scope lessicale della funzione. È una questione complicata perché in un certo senso c'è un fondo di verità, ma in un altro senso è completamente fuorviante.

## 🎯 Concetti Chiave

- **`this` NON si riferisce allo scope lessicale** di una funzione.
- `this` e lexical scope sono **meccanismi completamente separati**.
- Lo "scope object" esiste internamente nell'engine ma **non è accessibile** al codice JavaScript.
- **Non esiste ponte** tra lookup lessicale e binding di `this`.

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

**Cosa si potrebbe pensare**:

1. `this.bar()` chiamerebbe la funzione `bar()`.
2. `this.a` in `bar()` accedrebbe alla variabile `a` dello scope di `foo()`.
3. `this` creerebbe un "ponte" tra gli scope di `foo()` e `bar()`.

**Cosa succede realmente**:

1. `this.bar()` funziona **per caso** (se `bar` è nel global object).
2. `this.a` cerca `a` nel global object, non nello scope di `foo()`.
3. Non esiste alcun ponte - `this` punta al global object (default binding).

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

- In chiamata diretta `foo()`, `this` = global object.
- `this.bar()` diventa `window.bar()` (in browser).
- Se `bar` è nel global scope, viene trovata **per caso**.
- **Modo corretto**: Semplicemente `bar()` (lexical reference).

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

- La variabile `a` esiste solo nello scope lessicale interno di `foo()`.
- `this.a` cerca una proprietà `a` sull'oggetto puntato da `this`.
- **Non si può mai** accedere alla variabile locale `a` di un'altra funzione in questo modo.
- Non importa come si imposta `this` - le variabili locali sono inaccessibili come proprietà di un oggetto.

## 💡 Lo Scope Object (Interno)

### Cosa Esiste Internamente

Nell'implementazione del motore JavaScript, lo scope è rappresentato come una sorta di "oggetto":

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

  // ❌ Non è possibile fare questo:
  // console.log(scopeObject.a);
  // console.log(this.scopeObject.a);

  // ✅ È possibile solo fare questo:
  console.log(a); // Lookup lessicale normale
}
```

Lo "scope object" è una **struttura dati interna** dell'engine, non un vero oggetto JavaScript accessibile.
