# [[../../../appunti-completi#311-lidentificatore-this|Precedenza delle Regole di Binding]]

Quando **più di una regola** potrebbe applicarsi allo stesso call-site, serve conoscere l'**ordine di precedenza** per determinare quale vince.

## 🎯 Concetti Chiave

- **4 livelli**: new > explicit > implicit > default
- **Priorità**: `new` vince sempre, default perde sempre
- **new sovrascrive bind**: Anche hard binding può essere overridden da `new`
- **Uso pratico**: Partial application con `bind` + `new`
- **Regola decisionale**: Checklist per determinare `this`

## 📊 Gerarchia Completa

Le regole hanno un **ordine di precedenza** specifico (dalla più forte):

```
1️⃣ new binding (massima priorità)
2️⃣ Explicit binding (call, apply, bind)
3️⃣ Implicit binding (obj.method())
4️⃣ Default binding (minima priorità)
```

**Legge fondamentale**: La regola con priorità più alta vince.

## 🔍 Algoritmo Decisionale

Per determinare `this`, fai queste domande **in ordine** (top-down):

### 1. La funzione è chiamata con `new`?

```javascript
var obj = new foo();
```

✅ **`this` è il nuovo oggetto creato da `new`**

### 2. La funzione è chiamata con `call`/`apply`/`bind`?

```javascript
foo.call(obj);
foo.apply(obj, [args]);
var bar = foo.bind(obj);
bar();
```

✅ **`this` è l'oggetto specificato esplicitamente**

### 3. La funzione è chiamata come metodo (`obj.foo()`)?

```javascript
obj.foo();
```

✅ **`this` è l'oggetto contenitore**

### 4. Altrimenti?

```javascript
foo();
```

✅ **`this` è il global object** (o `undefined` in strict mode)

## 💻 Esempi di Precedenza

### Explicit > Implicit

Explicit binding vince su implicit:

```javascript
function foo() {
  console.log(this.valore);
}

var obj1 = { valore: "obj1", foo: foo };
var obj2 = { valore: "obj2" };

obj1.foo(); // "obj1" (implicit)
obj1.foo.call(obj2); // "obj2" (explicit vince!)
```

Anche se `foo` è chiamato come metodo di `obj1`, `call(obj2)` lo sovrascrive.

### new > Implicit

`new` vince su implicit:

```javascript
function foo(something) {
  this.a = something;
}

var obj1 = { foo: foo };

obj1.foo(2);
console.log(obj1.a); // 2 (implicit funziona)

var bar = new obj1.foo(4);
console.log(obj1.a); // 2 (non modificato)
console.log(bar.a); // 4 (new ha creato nuovo oggetto)
```

`new` crea un **nuovo oggetto**, ignorando l'implicit binding a `obj1`.

### new > Explicit (Sorpresa!)

`new` vince anche su **hard binding** (`bind`)!

```javascript
function foo(something) {
  this.a = something;
}

var obj1 = {};

var bar = foo.bind(obj1);
bar(2);
console.log(obj1.a); // 2 (bind funziona normalmente)

var baz = new bar(3);
console.log(obj1.a); // 2 (obj1 non modificato da new!)
console.log(baz.a); // 3 (new ha creato nuovo oggetto)
```

**Osservazioni**:

- `bar` è hard-bound a `obj1` con `bind`
- Chiamare `bar(2)` imposta `obj1.a = 2` ✅
- Ma `new bar(3)` crea un **nuovo oggetto** con `a = 3` ✅
- `obj1.a` rimane `2` (non modificato da `new`)

**`new` sovrascrive anche hard binding!**

### Implicit > Default

Implicit binding vince su default:

```javascript
function foo() {
  console.log(this.a);
}

var a = "global";
var obj = { a: "oggetto", foo: foo };

obj.foo(); // "oggetto" (implicit vince)
foo(); // "global" (default - nessuna regola più forte applicabile)
```

## 🧪 Test Completo della Precedenza

Esempio comprehensive che testa tutte le combinazioni:

```javascript
function foo(something) {
  this.a = something;
}

var obj1 = { foo: foo };
var obj2 = {};

// 1. Implicit binding
obj1.foo(2);
console.log(obj1.a); // 2 ✅

// 2. Explicit vince su Implicit
obj1.foo.call(obj2, 3);
console.log(obj2.a); // 3 ✅
console.log(obj1.a); // 2 (non modificato) ✅

// 3. new vince su Implicit
var bar = new obj1.foo(4);
console.log(obj1.a); // 2 (non modificato) ✅
console.log(bar.a); // 4 (nuovo oggetto) ✅

// 4. new vince anche su Explicit (bind)
var bound = foo.bind(obj1);
bound(5);
console.log(obj1.a); // 5 (bind funziona) ✅

var baz = new bound(6);
console.log(obj1.a); // 5 (non modificato da new!) ✅
console.log(baz.a); // 6 (new ha creato nuovo oggetto) ✅
```

**Conclusione**: `new` vince sempre, default perde sempre.

## 🔧 Come `new` Sovrascrive Hard Binding

Come fa `new` a sovrascrivere `bind()`? È una caratteristica built-in!

### Helper Semplice (Non Supporta new)

Il nostro helper "fake" bind non lo permetterebbe:

```javascript
function bind(fn, obj) {
  return function () {
    fn.apply(obj, arguments); // Sempre obj, nessun check su new
  };
}
```

Questa versione usa **sempre** `obj`, anche con `new`.

### Polyfill Ufficiale di ES5

`Function.prototype.bind()` built-in è più sofisticato:

```javascript
if (!Function.prototype.bind) {
  Function.prototype.bind = function (oThis) {
    // Validazione
    if (typeof this !== "function") {
      throw new TypeError(
        "Function.prototype.bind - what is trying to be bound is not callable",
      );
    }

    var aArgs = Array.prototype.slice.call(arguments, 1),
      fToBind = this,
      fNOP = function () {},
      fBound = function () {
        return fToBind.apply(
          // 👇 LA MAGIA STA QUI!
          this instanceof fNOP && oThis ? this : oThis,
          aArgs.concat(Array.prototype.slice.call(arguments)),
        );
      };

    fNOP.prototype = this.prototype;
    fBound.prototype = new fNOP();

    return fBound;
  };
}
```

### Il Trick Chiave

```javascript
this instanceof fNOP && oThis ? this : oThis;
```

Questa riga controlla:

- **`this instanceof fNOP`**: La funzione è chiamata con `new`?
- **Se sì**: Usa il `this` appena creato (nuovo oggetto)
- **Se no**: Usa `oThis` (hard binding normale)

```javascript
function foo(something) {
  this.a = something;
}

var obj = { a: 1 };
var bar = foo.bind(obj);

// Senza new: usa hard binding
bar(2);
// this instanceof fNOP → false
// Usa oThis (obj)
console.log(obj.a); // 2 ✅

// Con new: sovrascrive hard binding
var baz = new bar(3);
// this instanceof fNOP → true
// Usa this (nuovo oggetto)
console.log(baz.a); // 3 ✅
console.log(obj.a); // 2 (non modificato) ✅
```

## 🎯 Caso d'Uso: Partial Application

Perché permettere a `new` di sovrascrivere `bind`? **Partial application (currying)**!

### Esempio: Constructor con Parametri Pre-Applicati

```javascript
function multiply(a, b) {
  this.result = a * b;
}

// Presetta il primo parametro a 2
var multiplyByTwo = multiply.bind(null, 2);

// Usa con new per fornire il secondo parametro
var obj1 = new multiplyByTwo(3); // 2 * 3
var obj2 = new multiplyByTwo(5); // 2 * 5

console.log(obj1.result); // 6
console.log(obj2.result); // 10
```

**Passaggi**:

1. `bind(null, 2)` presetta `a = 2` (si usa `null` perché verrà sovrascritto da `new`)
2. `new multiplyByTwo(3)` fornisce `b = 3`
3. `new` crea nuovo oggetto con `result = 6`

### Partial Application Complesso

```javascript
function Person(firstName, lastName, age) {
  this.firstName = firstName;
  this.lastName = lastName;
  this.age = age;
}

// Factory per cognome comune
var createSmith = Person.bind(null, undefined, "Smith");

var john = new createSmith("John", 30);
var jane = new createSmith("Jane", 25);

console.log(john); // { firstName: "John", lastName: "Smith", age: 30 }
console.log(jane); // { firstName: "Jane", lastName: "Smith", age: 25 }
```

⚠️ **Nota**: Devi usare `undefined` o `null` per parametri che non vuoi pre-applicare.

## 🔀 Diagramma di Flusso

```
Determinare `this`:

┌─────────────────────┐
│ new foo()?          │
└──────┬──────────────┘
       │ Sì → this = nuovo oggetto creato
       │ No ↓
┌─────────────────────┐
│ call/apply/bind?    │
└──────┬──────────────┘
       │ Sì → this = oggetto specificato
       │ No ↓
┌─────────────────────┐
│ obj.foo()?          │
└──────┬──────────────┘
       │ Sì → this = obj (contenitore)
       │ No ↓
┌─────────────────────┐
│ Default             │
└──────┬──────────────┘
       │ → this = global (o undefined in strict)
```

## 💻 Cheat Sheet Pratico

| Call-Site         | `this` è...                 | Precedenza |
| ----------------- | --------------------------- | ---------- |
| `new foo()`       | Nuovo oggetto creato        | 1️⃣ Massima |
| `foo.call(obj)`   | `obj` (esplicito)           | 2️⃣ Alta    |
| `foo.bind(obj)()` | `obj` (hard binding)        | 2️⃣ Alta    |
| `obj.foo()`       | `obj` (contenitore)         | 3️⃣ Media   |
| `foo()`           | global o undefined (strict) | 4️⃣ Bassa   |

**Eccezione**: `new` vince anche su `bind()`!

## 📝 Riepilogo: Determinare `this`

Per determinare il valore di `this` da un call-site, **fai queste domande in ordine** e fermati quando la prima regola si applica:

### 1️⃣ La funzione è chiamata con `new` (new binding)?

Se sì, `this` è il nuovo oggetto costruito.

```javascript
var bar = new foo();
```

### 2️⃣ La funzione è chiamata con `call` o `apply` (explicit binding), anche nascosto dentro un `bind` hard binding?

Se sì, `this` è l'oggetto esplicitamente specificato.

```javascript
var bar = foo.call(obj2);
```

### 3️⃣ La funzione è chiamata con un contesto (implicit binding)?

Altrimenti noto come owning o containing object. Se sì, `this` è quell'oggetto contenitore.

```javascript
var bar = obj1.foo();
```

### 4️⃣ Altrimenti, default `this` (default binding)

Se in strict mode, usa `undefined`, altrimenti usa il global object.

```javascript
var bar = foo();
```

**Questo è tutto!** Queste sono tutte le regole necessarie per comprendere il binding di `this` per le normali chiamate di funzione. Beh... quasi. 😉

## ⚠️ Gotcha

### bind + new = Currying, Non Error

```javascript
function foo(a, b) {
  this.val = a + b;
}

var bar = foo.bind(null, 1); // Pre-applica a=1

var obj = new bar(2); // Fornisce b=2
console.log(obj.val); // 3 ✅ (non error!)
```

Molti sviluppatori si aspettano che `bind` "blocchi" totalmente `this`, ma `new` può sovrascriverlo.

### Doppio bind

```javascript
function foo() {
  console.log(this.a);
}

var obj1 = { a: 1 };
var obj2 = { a: 2 };

var bar = foo.bind(obj1);
var baz = bar.bind(obj2); // Seconda bind ignorata!

baz(); // 1 (prima bind vince)
```

Una funzione già bound **non può essere re-bound** (tranne con `new`).

### Arrow Functions Ignorano Tutto

Le arrow functions non seguono queste regole:

```javascript
var obj = {
  a: 2,
  foo: function () {
    var bar = () => console.log(this.a);
    bar();
  },
};

obj.foo(); // 2
obj.foo.call({ a: 3 }); // 2 (call ignorato!)
```

Arrow functions usano **lexical binding** (not dynamic).

## ✅ Best Practices

1. **Ricorda l'ordine**: new > explicit > implicit > default
2. **Usa l'algoritmo**: Top-down checklist per debugging
3. **Partial application**: Combina `bind` + `new` per factory functions
4. **Evita confusione**: Non mescolare troppe regole nello stesso codice
5. **Considera arrow**: Per evitare problemi di binding dinamico

## 🔗 Collegamenti

**Regole Individuali**:

- [[this-binding-new]] - New binding (priorità 1)
- [[this-binding-explicit]] - Explicit binding con call/apply/bind (priorità 2)
- [[this-binding-implicit]] - Implicit binding (priorità 3)
- [[this-binding-default]] - Default binding (priorità 4)

**Prerequisiti**:

- [[this-concept]] - Cos'è this
- [[this-confusion-scope]] - This vs scope

**Alternative**:

- [[this-arrow-functions]] - Arrow functions (lexical binding)

**Troubleshooting**:

- [[this-binding-problems]] - Problemi comuni e soluzioni

## 📚 Riferimenti

- **You Don't Know JS**: this & Object Prototypes - Chapter 2
- **MDN**: [Function.prototype.bind()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
- **MDN**: [new operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new)
- **TC39**: [Polyfill ufficiale di bind](https://tc39.es/ecma262/#sec-function.prototype.bind)

## 📌 Note Personali

[Spazio per annotazioni personali sulla precedenza delle regole]

---

**Tags**: `#javascript` `#this` `#precedence` `#binding-rules` `#new` `#bind` `#partial-application`
