# [[../../appunti-completi#311-lidentificatore-this|Arrow Functions e this]]

Le arrow functions (ES6+) hanno un comportamento completamente diverso rispetto alle funzioni tradizionali per quanto riguarda `this`. Non seguono le quattro regole standard: **ereditano `this` dal contesto lessicale esterno**.

## 🎯 Concetti Chiave

- **Lexical this**: Arrow functions NON hanno un proprio `this` - usano quello del contesto esterno
- **Immutabile**: Non è possibile cambiare il `this` di una arrow function con `call`, `apply` o `bind`
- **Soluzione ai callback**: Risolvono il problema della perdita di contesto nei callback
- **Pattern pre-ES6 equivalente**: `var self = this` fa la stessa cosa (cattura lessicale)
- **Cambio di paradigma**: Non sono solo una feature, ma un shift da binding dinamico a scoping lessicale
- **Due strade coerenti**: Scegliere tra stile lessicale (closures) o stile this (bind), non mescolare
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

## 🤔 Il Dilemma: Lexical vs this-style

### Due Paradigmi, Non Un Sostituto

Un aspetto importante da comprendere è che arrow functions e `self = this` non sono solo "soluzioni" al problema del binding di `this` - sono in realtà un **cambio di paradigma**: si sta abbandonando il meccanismo dinamico di `this` in favore dello scoping lessicale.

```javascript
var controller = {
  id: 42,

  init: function () {
    var self = this; // Stile lessicale

    document.addEventListener("click", function (evt) {
      self.handleClick(evt); // Usa variabile, non this
    });
  },

  handleClick: function (evt) {
    console.log("Controller " + this.id); // Stile this
  },
};
```

Questo codice **mescola due approcci**: dichiara di usare oggetti con metodi e `this`, ma poi non si fida di `this` e usa `self`. È concettualmente confuso.

### Due Strade Coerenti

**Opzione 1: Solo Scoping Lessicale**

Se si preferisce lo scoping lessicale, abbracciarlo completamente:

```javascript
function createController(id) {
  // Closure con variabili catturate
  var myId = id;

  return {
    init: function () {
      document.addEventListener("click", (evt) => {
        handleClick(evt);
      });
    },
  };

  function handleClick(evt) {
    console.log("Controller " + myId); // Usa closure
  }
}

var controller = createController(42);
```

**Opzione 2: Full this-style**

Se si sceglie `this`, usarlo correttamente:

```javascript
var controller = {
  id: 42,

  init: function () {
    // Usa bind per mantenere this
    document.addEventListener("click", this.handleClick.bind(this));
  },

  handleClick: function (evt) {
    console.log("Controller " + this.id); // this coerente
  },
};
```

O con arrow function come metodo (class field pattern, ES2022+):

```javascript
class Controller {
  id = 42;

  // Arrow come class field - cattura this dell'istanza
  handleClick = (evt) => {
    console.log("Controller " + this.id);
  };

  init() {
    // Nessun bind necessario
    document.addEventListener("click", this.handleClick);
  }
}
```

### Quando Mescolare è Problematico

Il problema non è usare arrow functions o `this` - è **mescolarli inconsistentemente nella stessa funzione**:

```javascript
// ❌ Confuso - mescola gli stili
var processor = {
  data: [],

  process: function () {
    var self = this; // Lessicale

    fetchData().then(function (result) {
      self.data = result; // Lessicale
      self.transform(); // this mascherato
    });
  },

  transform: function () {
    this.data = this.data.map((item) => item * this.multiplier); // this reale
  },

  multiplier: 2,
};
```

È più chiaro scegliere uno stile e mantenerlo:

```javascript
// ✅ Chiaro - stile this con arrow functions per callback
var processor = {
  data: [],

  process: function () {
    fetchData().then((result) => {
      // Arrow cattura this di process
      this.data = result;
      this.transform();
    });
  },

  transform: function () {
    this.data = this.data.map((item) => item * this.multiplier);
  },

  multiplier: 2,
};
```

### Linee Guida per Scegliere

**Usa arrow functions quando:**

- Scrivi callback che devono accedere al `this` del contesto esterno
- Lavori in una classe o oggetto che usa `this` e hai bisogno di preservarlo
- Vuoi codice più conciso e leggibile per funzioni brevi

**Usa function tradizionali quando:**

- Definisci metodi di oggetti o prototipi
- Hai bisogno di binding dinamico (diversi `this` in base al call-site)
- Usi `arguments` object
- Definisci constructor functions

**NON mescolare quando:**

- Usi `self = this` in alcune parti e arrow functions in altre (scegli uno)
- Usi `this` per alcuni lookup e variabili catturate per altri simili
- Passi da stile lexical a stile this senza ragione chiara

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

**Tags**: `#javascript` `#this` `#arrow-functions` `#es6` `#lexical-binding` `#lexical-vs-dynamic` `#self-pattern` `#code-style`
