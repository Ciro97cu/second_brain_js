# [[../../../appunti-completi#311-lidentificatore-this|Implicit Binding (Regola 2)]]

L'**implicit binding** si verifica quando una funzione viene chiamata come metodo di un oggetto. L'oggetto contenitore diventa automaticamente il contesto `this`.

## 🎯 Concetti Chiave

- **Oggetto contenitore**: Quando `obj.foo()`, `this` = `obj`
- **NON è possesso**: La funzione non è "posseduta" dall'oggetto, solo referenziata
- **Solo ultimo livello**: In catene come `obj1.obj2.foo()`, conta solo `obj2`
- **Implicitly Lost**: Problema comune - perdita del binding nei callback
- **Precedenza**: Più forte di default, più debole di explicit e new

## 💻 Quando Si Applica

**Quando**: La funzione viene chiamata come metodo di un oggetto (con contesto oggetto)

```javascript
function foo() {
  console.log(this.a);
}

var obj = {
  a: 2,
  foo: foo,
};

obj.foo(); // 2 (this = obj)
```

## 📋 La Funzione NON è "Posseduta"

Misconception comune: la funzione appartiene all'oggetto.

**Realtà**: Anche se `foo` è dichiarata separatamente e poi aggiunta come proprietà di `obj`, la funzione non è realmente "posseduta" da `obj`. L'oggetto contiene solo un **riferimento** alla funzione.

```javascript
function foo() {
  console.log(this.a);
}

// Funzione dichiarata globalmente
console.log(typeof foo); // "function"

// Poi aggiunta come proprietà
var obj = {
  a: 2,
  foo: foo, // Solo un riferimento!
};

// La funzione esiste ancora globalmente
foo(); // undefined (o errore in strict mode)
obj.foo(); // 2 (implicit binding)
```

### Il Call-Site Usa il Contesto

Quando `foo()` è chiamata come `obj.foo()`:

1. Il call-site ha un oggetto di contesto (`obj`)
2. La regola di implicit binding dice: l'oggetto che precede la funzione diventa `this`
3. Quindi `this.a` = `obj.a` = `2`

## 🔗 Solo l'Ultimo Livello Conta

Con catene di proprietà oggetto, conta **solo l'ultimo oggetto** nella catena:

```javascript
function foo() {
  console.log(this.a);
}

var obj2 = {
  a: 42,
  foo: foo,
};

var obj1 = {
  a: 2,
  obj2: obj2,
};

obj1.obj2.foo(); // 42 (this = obj2, NON obj1!)
```

**Perché?** Il call-site è `obj2.foo()`, quindi `obj2` è il contesto.

### Esempi Catene Più Lunghe

```javascript
function greet() {
  console.log(`Hello, ${this.name}!`);
}

var top = {
  name: "Top",
  middle: {
    name: "Middle",
    bottom: {
      name: "Bottom",
      greet: greet,
    },
  },
};

top.middle.bottom.greet(); // "Hello, Bottom!"
// Conta solo l'oggetto immediatamente prima del metodo
```

## ⚠️ Implicitly Lost

**Il problema più comune**: Una funzione con implicit binding **perde il binding** e ricade sulla default binding (global object o `undefined` in strict mode).

### Perdita per Assegnazione

```javascript
function foo() {
  console.log(this.a);
}

var obj = {
  a: 2,
  foo: foo,
};

var bar = obj.foo; // Solo un riferimento a foo!

var a = "oops, global";

bar(); // "oops, global" (default binding!)
```

**Cosa succede:**

1. `bar = obj.foo` copia il **riferimento** alla funzione, non il binding
2. `bar` ora punta direttamente a `foo`
3. Quando chiamiamo `bar()`, è una plain function call
4. Si applica default binding, non implicit!

### Perdita con Callback

```javascript
function foo() {
  console.log(this.a);
}

function doFoo(fn) {
  fn(); // <-- call-site! (plain call)
}

var obj = {
  a: 2,
  foo: foo,
};

var a = "oops, global";

doFoo(obj.foo); // "oops, global"
```

**Il passaggio di parametri è un'assegnazione implicita**:

```javascript
// Internamente è come:
function doFoo(fn) {
  // var fn = obj.foo;  // ← assegnazione!
  fn(); // ← plain call
}
```

### Perdita con setTimeout

```javascript
var obj = {
  a: 2,
  foo: function () {
    console.log(this.a);
  },
};

var a = "oops, global";

setTimeout(obj.foo, 100); // "oops, global"
```

Funzioni built-in come `setTimeout` chiamano la callback con plain call → default binding.

**Pseudo-implementazione di setTimeout**:

```javascript
function setTimeout(fn, delay) {
  // Aspetta delay millisecondi...
  fn(); // ← Plain call! (default binding)
}
```

### Esempi Reali

```javascript
var user = {
  name: "Mario",
  greet: function () {
    console.log(`Ciao, sono ${this.name}`);
  },
};

// ✅ Funziona
user.greet(); // "Ciao, sono Mario"

// ❌ Perde binding
setTimeout(user.greet, 1000); // "Ciao, sono undefined"

// ❌ Perde binding negli array methods
var greet = user.greet;
[1, 2, 3].forEach(greet); // Ogni chiamata: undefined
```

## 🎯 Event Handlers che Forzano this

Le librerie JavaScript spesso **forzano** `this` nelle callback degli event handler a puntare all'elemento DOM che ha scatenato l'evento.

```javascript
var controller = {
  name: "Controller",
  handleClick: function () {
    console.log(this.name); // "Controller" o nome elemento?
  },
};

// Pseudo-codice libreria
button.addEventListener("click", controller.handleClick);
// La libreria internamente fa:
// button.handleClick.call(button, event); // this = button!
```

Questo **toglie il controllo** sul binding di `this`.

**Risultato**: `this` non è `controller`, ma l'elemento `button`!

## ✅ Soluzioni per Implicitly Lost

### 1. Arrow Functions

```javascript
var obj = {
  a: 2,
  foo: function () {
    setTimeout(() => {
      console.log(this.a); // 2 (arrow cattura this lessicalmente)
    }, 100);
  },
};

obj.foo();
```

### 2. bind()

```javascript
var obj = {
  a: 2,
  foo: function () {
    console.log(this.a);
  },
};

setTimeout(obj.foo.bind(obj), 100); // 2
```

### 3. Variabile self/that (Legacy)

```javascript
var obj = {
  a: 2,
  foo: function () {
    var self = this; // Salva riferimento
    setTimeout(function () {
      console.log(self.a); // 2
    }, 100);
  },
};
```

Vedi [[this-binding-problems]] per approfondimenti sulle soluzioni.

## 💻 Esempi Completi

### Esempio Base

```javascript
var persona = {
  nome: "Mario",
  eta: 30,
  saluta: function () {
    console.log(`Ciao, sono ${this.nome} e ho ${this.eta} anni`);
  },
};

persona.saluta(); // "Ciao, sono Mario e ho 30 anni"
```

### Metodi Annidati

```javascript
var app = {
  nome: "MyApp",
  config: {
    timeout: 3000,
    mostraConfig: function () {
      console.log(`${this.timeout}ms`); // this = config, non app!
    },
  },
};

app.config.mostraConfig(); // "3000ms"
```

### Borrowing di Metodi

```javascript
function greet() {
  console.log(`Hello, ${this.name}`);
}

var person1 = { name: "Mario", greet: greet };
var person2 = { name: "Luigi" };

person1.greet(); // "Hello, Mario"

// "Prestare" il metodo a person2
person1.greet.call(person2); // "Hello, Luigi" (explicit binding!)
```

## ⚠️ Gotcha

### Array di Metodi

```javascript
var obj = {
  a: 2,
  foo: function () {
    console.log(this.a);
  },
};

var methods = [obj.foo]; // ← Perdita!

var a = "global";

methods[0](); // "global" (default binding)
// È come: var fn = obj.foo; fn();
```

### Destrutturazione

```javascript
var obj = {
  a: 2,
  foo: function () {
    console.log(this.a);
  },
};

var { foo } = obj; // Destrutturazione perde binding!

var a = "global";

foo(); // "global"
```

## ✅ Best Practices

1. **Attenzione ai callback**: Quando passi metodi come callback, perde il contesto
2. **Usa bind()** per "congelare" il binding quando passi metodi
3. **Arrow functions** per callback che devono mantenere il contesto lessicale
4. **Non fare affidamento** su implicit binding in codice asincrono senza precauzioni

## 🔗 Collegamenti

**Prerequisiti**:

- [[this-concept]] - Comprendere cos'è this
- [[this-binding-default]] - Default binding (regola 1)

**Regole Correlate**:

- [[this-binding-explicit]] - Explicit binding (regola 3)
- [[this-binding-new]] - New binding (regola 4)
- [[this-binding-precedence]] - Ordine di precedenza

**Problemi e Soluzioni**:

- [[this-binding-problems]] - Problemi comuni con callback
- [[this-call-apply-bind]] - bind() per fixare il binding
- [[this-arrow-functions]] - Arrow functions e this

## 📚 Riferimenti

- **You Don't Know JS**: this & Object Prototypes - Chapter 2
- **MDN**: [this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
- **MDN**: [Method definitions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Method_definitions)

## 📌 Note Personali

[Spazio per annotazioni personali sull'implicit binding]

---

**Tags**: `#javascript` `#this` `#implicit-binding` `#methods` `#callback-loss`
