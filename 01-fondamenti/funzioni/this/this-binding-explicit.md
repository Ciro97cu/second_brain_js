# [[../../../appunti-completi#311-lidentificatore-this|Explicit Binding (Regola 3)]]

L'**explicit binding** permette di controllare manualmente il valore di `this` usando i metodi `call()`, `apply()` o `bind()`. Forzare una funzione a usare un oggetto specifico come contesto **senza mutarel'oggetto**.

## 🎯 Concetti Chiave

- **Controllo esplicito**: Specifica manualmente quale oggetto diventa `this`
- **call() e apply()**: Invocano immediatamente la funzione con `this` specificato
- **bind()**: Crea nuova funzione con `this` "congelato" (hard binding)
- **Boxing primitivi**: Primitivi vengono automaticamente wrappati
- **Precedenza**: Più forte di implicit, più debole di new

## 💻 call() e apply()

Tutte le funzioni hanno accesso ai metodi `call()` e `apply()` (via `[[Prototype]]`).

**Entrambi**:

- Prendono come **primo parametro** l'oggetto da usare per `this`
- Invocano la funzione con quel `this` specificato

```javascript
function foo() {
  console.log(this.a);
}

var obj = {
  a: 2,
};

foo.call(obj); // 2 (this = obj)
foo.apply(obj); // 2 (this = obj)
```

### Differenza: Parametri Aggiuntivi

**call()**: Argomenti separati
**apply()**: Argomenti in array

```javascript
function somma(b, c) {
  console.log(this.a + b + c);
}

var obj = { a: 1 };

somma.call(obj, 2, 3); // 6 (call: argomenti separati)
somma.apply(obj, [2, 3]); // 6 (apply: argomenti in array)
```

**Mnemonic**: **A**pply = **A**rray

### Quando Usare Quale

```javascript
function greet(greeting, punctuation) {
  console.log(greeting + ", " + this.name + punctuation);
}

var person = { name: "Mario" };

// call - quando hai argomenti separati
greet.call(person, "Ciao", "!");

// apply - quando hai array di argomenti
var args = ["Hello", "!!!"];
greet.apply(person, args);
```

## 📦 Boxing dei Primitivi

Se passi un primitivo (`string`, `boolean`, `number`) come `this`, viene automaticamente **wrappato** nel suo oggetto equivalente.

```javascript
function foo() {
  console.log(this); // [Number: 42] (oggetto!)
  console.log(typeof this); // "object"
}

foo.call(42);
```

**Conversioni**:

- `42` → `new Number(42)`
- `"hello"` → `new String("hello")`
- `true` → `new Boolean(true)`

Processo chiamato **"boxing"**.

```javascript
function showType() {
  console.log(typeof this, this);
}

showType.call(42); // object [Number: 42]
showType.call("hello"); // object [String: 'hello']
showType.call(true); // object [Boolean: true]
```

## ⚠️ Problema: Explicit Binding Non Basta

Anche con `call()`/`apply()`, una funzione può ancora **perdere** il binding:

```javascript
function foo() {
  console.log(this.a);
}

var obj = { a: 2 };

// Funziona, ma verboso e ripetitivo
setTimeout(function () {
  foo.call(obj);
}, 100);

// Non puoi assegnare il riferimento
var bar = foo.call; // ❌ Non funziona così!
```

Serve un modo per **"congelare"** permanentemente il binding → **Hard Binding**

## 🔒 Hard Binding Pattern

La soluzione: creare una funzione wrapper che chiama sempre la funzione originale con il `this` desiderato.

### Versione Base

```javascript
function foo() {
  console.log(this.a);
}

var obj = {
  a: 2,
};

var bar = function () {
  foo.call(obj); // Sempre con obj!
};

bar(); // 2
setTimeout(bar, 100); // 2
bar.call(window); // 2 (call non può sovrascriverlo!)
```

`bar()` chiama **sempre** `foo.call(obj)` internamente. `this` è "hard-bound" a `obj`.

### Con Pass-Through di Argomenti

```javascript
function foo(something) {
  console.log(this.a, something);
  return this.a + something;
}

var obj = { a: 2 };

var bar = function () {
  return foo.apply(obj, arguments); // Passa tutti gli argomenti
};

var b = bar(3); // 2 3
console.log(b); // 5
```

### Helper Riutilizzabile

```javascript
function bind(fn, obj) {
  return function () {
    return fn.apply(obj, arguments);
  };
}

var obj = { a: 2 };

function foo(something) {
  console.log(this.a, something);
  return this.a + something;
}

var bar = bind(foo, obj);

bar(3); // 2 3
```

## ✨ Function.prototype.bind()

ES5+ fornisce **`bind()` built-in** in `Function.prototype`:

```javascript
function foo(something) {
  console.log(this.a, something);
  return this.a + something;
}

var obj = { a: 2 };

var bar = foo.bind(obj); // Hard binding

bar(3); // 2 3
setTimeout(bar, 100); // 2 3
bar.call(window, 3); // 2 3 (bind vince su call!)
```

**`bind()` restituisce una nuova funzione** hardcoded per chiamare l'originale con il `this` specificato.

### Caratteristiche di bind()

```javascript
function greet(greeting, punctuation) {
  return greeting + ", " + this.name + punctuation;
}

var person = { name: "Mario" };

var greetMario = person.bind(person);

console.log(typeof greetMario); // "function" (nuova funzione)
console.log(greetMario("Ciao", "!")); // "Ciao, Mario!"
```

### Partial Application (Currying)

`bind()` può anche **pre-applicare argomenti**:

```javascript
function multiply(a, b) {
  return this.multiplier * a * b;
}

var obj = { multiplier: 10 };

var multiplyBy10 = multiply.bind(obj, 2); // Pre-applica `a = 2`

console.log(multiplyBy10(5)); // 100 (10 * 2 * 5)
```

**Sintassi**: `fn.bind(thisArg, arg1, arg2, ...)`

Argomenti dopo `thisArg` vengono "congelati" come argomenti iniziali.

## 🔧 API Call "Contexts"

Molte funzioni built-in offrono un parametro **"context"** opzionale per specificare `this` senza dover usare `bind()`.

### Array.prototype.forEach()

```javascript
function foo(el) {
  console.log(el, this.id);
}

var obj = {
  id: "awesome",
};

// Secondo parametro = context per this
[1, 2, 3].forEach(foo, obj);
// 1 awesome
// 2 awesome
// 3 awesome
```

Internamente, `forEach` usa `call()` o `apply()` per impostare `this`.

### Altri Metodi con Context

```javascript
// map con context
[1, 2, 3].map(
  function (n) {
    return n * this.multiplier;
  },
  { multiplier: 2 },
); // [2, 4, 6]

// filter con context
[1, 2, 3].filter(
  function (n) {
    return n > this.threshold;
  },
  { threshold: 1 },
); // [2, 3]

// every con context
[1, 2, 3].every(
  function (n) {
    return n < this.max;
  },
  { max: 10 },
); // true

// some con context
[1, 2, 3].some(
  function (n) {
    return n === this.target;
  },
  { target: 2 },
); // true
```

### jQuery Esempi

```javascript
// jQuery fornisce context in molti metodi
$("button").each(function (index) {
  // `this` è automaticamente l'elemento DOM
  console.log(this.id);
});

// Ma puoi anche usare bind per controllo custom
var controller = {
  name: "Controller",
  handleClick: function (event) {
    console.log(this.name, event.type);
  },
};

$("button").on("click", controller.handleClick.bind(controller));
```

## 💻 Esempi Completi

### Borrowing di Metodi

```javascript
function speak() {
  console.log(`${this.sound}! I'm a ${this.type}`);
}

var cat = { type: "cat", sound: "Meow" };
var dog = { type: "dog", sound: "Woof" };

speak.call(cat); // "Meow! I'm a cat"
speak.call(dog); // "Woof! I'm a dog"
```

### Array-like Objects

```javascript
function convertArgs() {
  // `arguments` è array-like, non array vera
  var args = Array.prototype.slice.call(arguments);
  return args;
}

var result = convertArgs(1, 2, 3);
console.log(result); // [1, 2, 3]
console.log(Array.isArray(result)); // true
```

Moderno (ES6+):

```javascript
function convertArgs(...args) {
  return args; // Già array!
}
```

### Hard Binding per Event Handlers

```javascript
var app = {
  name: "MyApp",
  count: 0,
  handleClick: function () {
    this.count++;
    console.log(`${this.name} clicks: ${this.count}`);
  },
};

// Senza bind (perde this)
button.addEventListener("click", app.handleClick); // ❌ this = button

// Con bind (mantiene this)
button.addEventListener("click", app.handleClick.bind(app)); // ✅ this = app
```

## ⚠️ Gotcha

### bind() Crea Nuova Funzione

```javascript
var obj = {
  a: 2,
  foo: function () {
    console.log(this.a);
  },
};

var bar = obj.foo.bind(obj);

console.log(bar === obj.foo); // false! (nuova funzione)
```

### bind() Non È Chiamata

```javascript
function foo() {
  console.log(this.a);
}

var obj = { a: 2 };

var bar = foo.bind(obj); // Non chiama foo!

bar(); // Ora chiama foo con this = obj
```

### Doppio bind

```javascript
function foo() {
  console.log(this.a);
}

var obj1 = { a: 1 };
var obj2 = { a: 2 };

var bar = foo.bind(obj1); // Prima bind
bar(); // 1

var baz = bar.bind(obj2); // Seconda bind (ignorata!)
baz(); // 1 (prima bind vince sempre)
```

Una funzione già bound **non può essere re-bound**!

## ✅ Best Practices

1. **call/apply**: Usa per invocazioni singole con this controllato
2. **bind()**: Usa per creare funzioni persistent con this fisso
3. **Context parameter**: Preferisci quando disponibile (forEach, map, etc.)
4. **Evita re-binding**: Una volta bound, la funzione è "sealed"

## 🔗 Collegamenti

**Prerequisiti**:

- [[this-concept]] - Comprendere cos'è this
- [[this-binding-default]] - Default binding (regola 1)
- [[this-binding-implicit]] - Implicit binding (regola 2)

**Dettagli**:

- [[this-call-apply-bind]] - Approfondimento su call, apply, bind

**Regole Correlate**:

- [[this-binding-new]] - New binding (regola 4)
- [[this-binding-precedence]] - Ordine di precedenza

**Problemi**:

- [[this-binding-problems]] - Problemi comuni e soluzioni
- [[this-arrow-functions]] - Alternative con arrow functions

## 📚 Riferimenti

- **You Don't Know JS**: this & Object Prototypes - Chapter 2
- **MDN**: [Function.prototype.call()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)
- **MDN**: [Function.prototype.apply()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)
- **MDN**: [Function.prototype.bind()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)

## 📌 Note Personali

[Spazio per annotazioni personali sull'explicit binding]

---

**Tags**: `#javascript` `#this` `#explicit-binding` `#call` `#apply` `#bind` `#hard-binding`
