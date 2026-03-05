# [[../../appunti-completi#311-lidentificatore-this|Arrow Functions e this]]

Le arrow functions (ES6+) hanno un comportamento completamente diverso rispetto alle funzioni tradizionali per quanto riguarda `this`. Non seguono le quattro regole standard: **ereditano `this` dal contesto lessicale esterno**.

## 🎯 Concetti Chiave

- **Lexical this**: Arrow functions NON hanno un proprio `this` - usano quello del contesto esterno
- **Immutabile**: Non puoi cambiare il `this` di una arrow function con `call`, `apply` o `bind`
- **Soluzione ai callback**: Risolvono il problema della perdita di contesto nei callback
- **Trade-off**: Più semplici ma meno flessibili delle function tradizionali

## 💻 Binding Lessicale di this

### Arrow Function vs Function Tradizionale

```javascript
function Timer() {
  this.seconds = 0;

  // Function tradizionale - perde this
  setInterval(function () {
    this.seconds++; // this = Window! (default binding)
    console.log(this.seconds); // NaN
  }, 1000);
}

function Timer() {
  this.seconds = 0;

  // Arrow function - cattura this
  setInterval(() => {
    this.seconds++; // this = istanza Timer
    console.log(this.seconds); // 1, 2, 3...
  }, 1000);
}

new Timer();
```

### Cattura del Contesto Esterno

```javascript
var obj = {
  id: 42,

  regularFunction: function () {
    console.log(this.id); // 42

    setTimeout(function () {
      console.log(this.id); // undefined (this = global)
    }, 100);
  },

  arrowFunction: function () {
    console.log(this.id); // 42

    setTimeout(() => {
      console.log(this.id); // 42 (this catturato lessicalmente)
    }, 100);
  },
};

obj.regularFunction();
obj.arrowFunction();
```

## ⚠️ Gotcha

### Non Modificabile con call/apply/bind

```javascript
var obj1 = { value: 1 };
var obj2 = { value: 2 };

var arrow = () => {
  console.log(this.value);
};

var regular = function () {
  console.log(this.value);
};

// Function tradizionale
regular.call(obj1); // 1
regular.call(obj2); // 2

// Arrow function - ignora call/bind!
arrow.call(obj1); // undefined (usa this globale catturato)
arrow.call(obj2); // undefined
```

Il `this` di una arrow function è **fissato al momento della definizione** e non può essere cambiato.

### Non Usare come Metodi di Oggetti

```javascript
// ❌ SBAGLIATO
var obj = {
  value: 42,
  getValue: () => {
    return this.value; // this NON è obj!
  },
};

obj.getValue(); // undefined (this = contesto esterno a obj)

// ✅ CORRETTO
var obj = {
  value: 42,
  getValue: function () {
    return this.value; // this = obj
  },
};

obj.getValue(); // 42
```

Le arrow functions come metodi di oggetti letterali prendono `this` dal contesto esterno (spesso `window`), non dall'oggetto.

### Non Usare come Constructor

```javascript
var Foo = () => {
  this.value = 1;
};

var obj = new Foo(); // TypeError: Foo is not a constructor
```

Le arrow functions **non possono essere usate con `new`** - non hanno [[Construct]] interno.

### Arguments Non Disponibile

```javascript
function regular() {
  console.log(arguments); // [1, 2, 3]
}

var arrow = () => {
  console.log(arguments); // ReferenceError o arguments del contesto esterno
};

regular(1, 2, 3);
arrow(1, 2, 3);
```

Arrow functions non hanno il proprio oggetto `arguments`. Per accedere agli argomenti usa rest parameters:

```javascript
var arrow = (...args) => {
  console.log(args); // [1, 2, 3]
};

arrow(1, 2, 3);
```

## ✅ Best Practices

### Quando Usare Arrow Functions

1. **Callback e closures**: Quando vuoi mantenere il `this` del contesto esterno

```javascript
class Component {
  constructor() {
    this.data = [];
  }

  loadData() {
    fetchData().then((result) => {
      this.data = result; // this = istanza Component
    });
  }
}
```

2. **Event handler in classi**:

```javascript
class Button {
  constructor() {
    this.count = 0;
    // Arrow function mantiene this della classe
    this.handleClick = () => {
      this.count++;
    };
  }
}
```

3. **Array methods**:

```javascript
var obj = {
  multiplier: 2,

  multiply: function (numbers) {
    return numbers.map((n) => n * this.multiplier); // this = obj
  },
};

obj.multiply([1, 2, 3]); // [2, 4, 6]
```

### Quando NON Usare Arrow Functions

1. ❌ **Metodi di oggetti letterali** (usa method shorthand)

```javascript
// ❌ No
var obj = {
  value: 1,
  increment: () => this.value++,
};

// ✅ Sì
var obj = {
  value: 1,
  increment() {
    // method shorthand
    this.value++;
  },
};
```

2. ❌ **Constructor functions**

3. ❌ **Quando hai bisogno di `arguments`**

4. ❌ **Quando vuoi binding dinamico di this**

## 💡 Pattern: Self/That vs Arrow

### Vecchio Pattern (pre-ES6)

```javascript
function Timer() {
  var self = this; // Salva riferimento
  self.seconds = 0;

  setInterval(function () {
    self.seconds++;
  }, 1000);
}
```

### Pattern Moderno (ES6+)

```javascript
function Timer() {
  this.seconds = 0;

  setInterval(() => {
    this.seconds++; // Più pulito e idiomatico
  }, 1000);
}
```

Arrow functions rendono obsoleto il pattern `var self = this`.

## 📊 Confronto Funzioni

| Feature           | Function               | Arrow Function        |
| ----------------- | ---------------------- | --------------------- |
| `this`            | Dinamico (4 regole)    | Lessicale (catturato) |
| `arguments`       | Disponibile            | Non disponibile       |
| `new`             | Può essere constructor | Non può               |
| `call/apply/bind` | Modificano `this`      | Ignorati              |
| Sintassi          | `function() {}`        | `() => {}`            |

## 🔗 Collegamenti

**Prerequisiti**:

- [[this-concept]] - Comprendere il binding di this
- [[this-binding-precedence]] - Le regole che arrow functions NON seguono
- [[funzioni]] - Funzioni JavaScript base

**Concetti Correlati**:

- [[this-binding-problems]] - Problemi che arrow functions risolvono
- [[this-call-apply-bind]] - Metodi che arrow functions ignorano
- [[../es6/arrow-functions]] - Altri dettagli su arrow functions

**Approfondimenti**:

- [[../classi/class-methods]] - Arrow functions in classi ES6
- [[../avanzate/lexical-scope]] - Scope lessicale

## 📚 Riferimenti

- **MDN**: [Arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
- **JavaScript.info**: [Arrow functions revisited](https://javascript.info/arrow-functions)
- **You Don't Know JS**: ES6 & Beyond - Arrow Functions

## 📌 Note Personali

[Annotazioni su arrow functions e this]

---

**Tags**: `#javascript` `#this` `#arrow-functions` `#es6` `#lexical-binding`
