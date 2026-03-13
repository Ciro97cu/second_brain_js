# [[../../appunti-completi#311-lidentificatore-this|call(), apply() e bind()]]

JavaScript offre tre metodi nativi per controllare esplicitamente il binding di `this`: `call()`, `apply()` e `bind()`. Questi metodi permettono di forzare una funzione a usare un oggetto specifico come contesto.

## 🎯 Concetti Chiave

- **Explicit binding**: Controllo manuale del valore di `this`
- **call() e apply()**: Invocano subito la funzione con `this` specificato
- **bind()**: Crea una nuova funzione con `this` "congelato" (hard binding)
- **Differenza call/apply**: Solo nella sintassi per passare argomenti

## 💻 call() - Chiamata Immediata

Invoca la funzione immediatamente con `this` specificato e argomenti separati.

**Sintassi**: `funzione.call(thisArg, arg1, arg2, ...)`

```javascript
function greet(greeting, punctuation) {
  console.log(greeting + ", " + this.name + punctuation);
}

var person = { name: "Kyle" };

greet.call(person, "Hello", "!"); // "Hello, Kyle!"
```

### Uso Tipico: Borrowing di Metodi

```javascript
var obj1 = {
  name: "Obj1",
  speak: function () {
    console.log("I am " + this.name);
  },
};

var obj2 = { name: "Obj2" };

obj1.speak.call(obj2); // "I am Obj2"
```

## 💻 apply() - Chiamata con Array

Identico a `call()` ma accetta argomenti come array invece di lista separata.

**Sintassi**: `funzione.apply(thisArg, [arg1, arg2, ...])`

```javascript
function greet(greeting, punctuation) {
  console.log(greeting + ", " + this.name + punctuation);
}

var person = { name: "Kyle" };

greet.apply(person, ["Hello", "!"]); // "Hello, Kyle!"
```

### Uso Tipico: Spread di Array

```javascript
var numbers = [5, 6, 2, 3, 7];

// Prima di spread operator
var max = Math.max.apply(null, numbers); // 7

// Con spread operator (moderno)
var max = Math.max(...numbers); // 7
```

## 💻 bind() - Hard Binding

Crea una **nuova funzione** con `this` permanentemente fissato. La funzione originale rimane immutata.

**Sintassi**: `var newFunc = funzione.bind(thisArg, arg1, arg2, ...)`

```javascript
function greet() {
  console.log("Hello, " + this.name);
}

var person = { name: "Kyle" };

var boundGreet = greet.bind(person);
boundGreet(); // "Hello, Kyle"

// Anche se provo a cambiarla con call
boundGreet.call({ name: "John" }); // "Hello, Kyle" (bind vince!)
```

### Hard Binding Non Sovrascrivibile

```javascript
function foo() {
  console.log(this.a);
}

var obj1 = { a: 2 };
var obj2 = { a: 3 };

var bar = foo.bind(obj1);
bar(); // 2

bar.call(obj2); // 2 (NON 3! bind ha precedenza)
```

### Partial Application (Currying)

`bind()` permette anche di "pre-caricare" argomenti:

```javascript
function multiply(a, b) {
  return a * b;
}

var double = multiply.bind(null, 2); // Primo arg sempre 2
console.log(double(5)); // 10 (2 * 5)
console.log(double(10)); // 20 (2 * 10)
```

## 📊 Confronto Metodi

| Metodo    | Esecuzione | Argomenti | Ritorno            | Permanente |
| --------- | ---------- | --------- | ------------------ | ---------- |
| `call()`  | Immediata  | Lista     | Risultato funzione | No         |
| `apply()` | Immediata  | Array     | Risultato funzione | No         |
| `bind()`  | Nessuna    | Lista     | Nuova funzione     | Sì         |

## ⚠️ Gotcha

### bind() Non Modifica Originale

```javascript
function foo() {
  console.log(this.a);
}

var obj = { a: 2 };

foo.bind(obj); // Crea nuova funzione ma non la salviamo!
foo(); // undefined (originale immutato)

var bar = foo.bind(obj); // COSÌ è corretto
bar(); // 2
```

### null/undefined come thisArg

```javascript
function foo() {
  console.log(this);
}

foo.call(null); // Window (o global object)
foo.call(undefined); // Window (o global object)
```

In non-strict mode, `null` e `undefined` vengono sostituiti con global object. In strict mode rimangono `null`/`undefined`.

### Array-Like Objects con apply

```javascript
function sum() {
  return Array.prototype.reduce.call(
    arguments,
    function (a, b) {
      return a + b;
    },
    0,
  );
}

console.log(sum(1, 2, 3, 4)); // 10
```

`arguments` non è un vero array, ma è possibile "prendere in prestito" metodi array con `call`.

## ✅ Best Practices

1. **call vs apply**: Usa `call` se hai argomenti singoli, `apply` se sono in array
2. **bind per callback**: Usa `bind()` per mantenere il contesto in event handler e callback
3. **Evita null**: Passa un oggetto vuoto `{}` invece di `null` per evitare binding accidentali al global
4. **Naming bound functions**: Nomina la funzione bound per debugging più facile

```javascript
// ❌ Non ideale
setTimeout(obj.method.bind(obj), 1000);

// ✅ Meglio
var boundMethod = obj.method.bind(obj);
setTimeout(boundMethod, 1000);
```

5. **Performance**: `bind()` crea una nuova funzione ogni volta → non usarlo in loop o render frequenti

## 💡 Pattern Utile: Safer Hard Binding

```javascript
function bind(fn, obj) {
  return function () {
    return fn.apply(obj, arguments);
  };
}

function foo() {
  console.log(this.a);
}

var obj = { a: 2 };
var bar = bind(foo, obj);

bar(); // 2
```

Questo pattern manuale mostra come `bind()` funziona internamente.

## 🔗 Collegamenti

**Prerequisiti**:

- [[this-concept]] - Comprendere this
- [[this-binding-explicit]] - Regola di explicit binding

**Concetti Correlati**:

- [[this-binding-problems]] - Quando usare bind per risolvere problemi
- [[this-arrow-functions]] - Alternative moderne con arrow functions
- [[funzioni]] - Funzioni JavaScript base

**Approfondimenti**:

- [[../avanzate/currying]] - Currying e partial application
- [[../avanzate/function-methods]] - Altri metodi delle funzioni

## 📚 Riferimenti

- **MDN**: [Function.prototype.call()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)
- **MDN**: [Function.prototype.apply()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)
- **MDN**: [Function.prototype.bind()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
- **You Don't Know JS**: this & Object Prototypes - Chapter 2

## 📌 Note Personali

[Annotazioni su call, apply, bind]

---

**Tags**: `#javascript` `#this` `#call` `#apply` `#bind` `#explicit-binding`
