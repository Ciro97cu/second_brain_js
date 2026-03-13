# [[../../../appunti-completi#311-lidentificatore-this|call() e apply()]]

JavaScript offre metodi nativi per controllare esplicitamente il binding di `this`: `call()` e `apply()`. Entrambi permettono di forzare una funzione a usare un oggetto specifico come contesto (Explicit Binding) invocando la funzione immediatamente.

## 🎯 Concetti Chiave

- **Explicit binding**: Controllo manuale del valore di `this` al momento dell'invocazione.
- **Esecuzione Immediata**: Entrambi i metodi invocano subito la funzione con il `this` specificato.
- **Differenza Principale**: Riguarda unicamente la sintassi per passare gli argomenti alla funzione invocata.

## 💻 call() - Argomenti Separati

Invoca la funzione immediatamente passando gli argomenti separati da virgola.

**Sintassi**: `funzione.call(thisArg, arg1, arg2, ...)`

```javascript
function greet(greeting, punctuation) {
  console.log(greeting + ", " + this.name + punctuation);
}

var person = { name: "Kyle" };

greet.call(person, "Hello", "!"); // "Hello, Kyle!"
```

### Uso Tipico: Borrowing di Metodi

È comune usare `call()` per "prendere in prestito" metodi da altri oggetti:

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

## 💻 apply() - Argomenti in Array

Identico a `call()`, ma accetta gli argomenti racchiusi in un singolo array (o un oggetto array-like).

**Sintassi**: `funzione.apply(thisArg, [arg1, arg2, ...])`

```javascript
function greet(greeting, punctuation) {
  console.log(greeting + ", " + this.name + punctuation);
}

var person = { name: "Kyle" };

greet.apply(person, ["Hello", "!"]); // "Hello, Kyle!"
```

### Uso Tipico: Gestione di Array e Array-Like Objects

Prima dell'introduzione dello spread operator (`...`), `apply()` era ampiamente usato per passare un array a funzioni che accettavano argomenti multipli:

```javascript
var numbers = [5, 6, 2, 3, 7];
var max = Math.max.apply(null, numbers); // 7

// Con spread operator (moderno)
var maxModern = Math.max(...numbers); // 7
```

Inoltre, permette di prendere in prestito metodi degli array per oggetti "array-like" come `arguments`:

```javascript
function sum() {
  return Array.prototype.reduce.call(
    arguments,
    function (a, b) { return a + b; },
    0
  );
}

console.log(sum(1, 2, 3, 4)); // 10
```

## ⚠️ Gotcha: null e undefined

Se si passa `null` o `undefined` come primo argomento (il `thisArg`) in *non-strict mode*, JavaScript li sostituisce con l'oggetto globale (es. `window` nel browser). In *strict mode*, `this` rimane null o undefined. È considerata una best practice passare un oggetto vuoto indipendente (`Object.create(null)`) piuttosto che `null` per evitare modifiche involontarie all'oggetto globale.

```javascript
function foo() { console.log(this); }
foo.call(null); // Oggetto globale (non-strict)
```

---

**Tags**: `#javascript` `#this` `#call` `#apply` `#explicit-binding`
