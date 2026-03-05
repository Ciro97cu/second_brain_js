# [[../../appunti-completi#311-lidentificatore-this|Problemi con il Binding di this]]

Uno dei problemi più comuni in JavaScript è la **perdita del binding di `this`** quando si passano funzioni come callback o handler. Questo accade perché il call-site determina `this`, non il punto di definizione della funzione.

## 🎯 Concetti Chiave

- **Binding loss**: Passare un metodo come callback fa perdere il contesto dell'oggetto
- **Call-site invisibile**: In callback e handler, il call-site è spesso nel codice di librerie/framework
- **Tre soluzioni**: Arrow functions, `bind()`, o variabile `self` (legacy)
- **Arrow functions non sono sempre la risposta**: Non usarle come metodi diretti di oggetti

## 💻 Esempi di Codice

### Il Problema: Callback Perde this

```javascript
var obj = {
  value: 42,

  getValue: function () {
    console.log(this.value);
  },
};

obj.getValue(); // 42 - Funziona (implicit binding)

// Passato come callback
setTimeout(obj.getValue, 100); // undefined
// this diventa window/global (default binding)
```

**Perché succede**:

```javascript
// Quando passi obj.getValue come callback, è equivalente a:
var fn = obj.getValue; // Estrai il riferimento alla funzione
setTimeout(fn, 100); // fn viene chiamata senza contesto oggetto

// Il call-site diventa:
fn(); // Default binding → this = global object
```

### Soluzione 1: Arrow Function Wrapper

```javascript
setTimeout(() => obj.getValue(), 100); // 42

// Event handler
document
  .querySelector("button")
  .addEventListener("click", () => button.handleClick());
```

### Soluzione 2: bind() - Hard Binding

```javascript
var boundGetValue = obj.getValue.bind(obj);
setTimeout(boundGetValue, 100); // 42

// Event handler con possibilità di rimuovere
var handler = button.handleClick.bind(button);
element.addEventListener("click", handler);
element.removeEventListener("click", handler); // Funziona!
```

### Soluzione 3: self/that Pattern (Legacy)

```javascript
var obj = {
  value: 42,

  setup: function () {
    var self = this; // Salva riferimento

    setTimeout(function () {
      console.log(self.value); // 42 (usa closure)
    }, 100);
  },
};
```

### Eventi DOM

```javascript
var button = {
  label: "Click me",
  count: 0,

  handleClick: function () {
    this.count++;
    console.log(this.label + " clicked " + this.count + " times");
  },
};

// ❌ Perde this
element.addEventListener("click", button.handleClick);

// ✅ Mantiene this
element.addEventListener("click", button.handleClick.bind(button));
// O con arrow
element.addEventListener("click", () => button.handleClick());
```

### Classi ES6 - Class Fields

```javascript
class Component {
  count = 0;

  // Arrow function come field - this sempre corretto
  handleClick = () => {
    this.count++;
    console.log(this.count);
  };
}

var component = new Component();
element.addEventListener("click", component.handleClick); // Funziona!
```

### Promise Chains

```javascript
var api = {
  baseUrl: "https://api.example.com",
  data: [],

  fetchData: function () {
    return fetch(this.baseUrl + "/data")
      .then((response) => response.json())
      .then((data) => {
        this.data = data; // this = api grazie ad arrow
        return this.processData();
      });
  },

  processData: function () {
    console.log("Processing " + this.data.length + " items");
  },
};
```

## ⚠️ Gotcha / Errori Comuni

### Arrow Function come Metodo - NON Funziona!

```javascript
// ❌ SBAGLIATO
var obj = {
  value: 42,
  getValue: () => {
    console.log(this.value); // undefined!
  },
};

obj.getValue(); // undefined (this catturato da contesto esterno)
```

Arrow functions catturano `this` **dal contesto lessicale al momento della definizione**. In un oggetto letterale, `this` esterno è spesso `window`.

**Correzione**:

```javascript
// ✅ CORRETTO
var obj = {
  value: 42,

  getValue: function () {
    return this.value;
  },

  setup: function () {
    setTimeout(() => {
      console.log(this.value); // 42 - cattura this di setup()
    }, 100);
  },
};
```

### bind() Multipli Ignorati

```javascript
function foo() {
  console.log(this.a);
}

var obj1 = { a: 1 };
var obj2 = { a: 2 };

var bar = foo.bind(obj1);
var baz = bar.bind(obj2); // Secondo bind ignorato!

baz(); // 1 (non 2!)
```

### Performance: Binding in Rendering Loop

```javascript
// ❌ Non ottimale - crea funzione ogni render
items.forEach((item) => {
  render(<Button onClick={() => this.handleClick(item)} />);
});

// ✅ Meglio - salva bound function
var boundHandlers = items.map((item) => this.handleClick.bind(this, item));
```

## ✅ Best Practices

1. **Metodi di oggetti**: Usa `function` regolare o method shorthand, MAI arrow functions

```javascript
// ✅ Corretto
var obj = {
  value: 1,
  increment() {
    // method shorthand
    this.value++;
  },
};
```

2. **Callback interni**: Usa arrow functions per catturare `this` lessicalmente

```javascript
// ✅ Corretto
setup: function() {
  setTimeout(() => this.doSomething(), 100);
}
```

3. **Event handler in classi**: Preferisci arrow function come class field

```javascript
class Button {
  handleClick = () => {
    // this sempre corretto
  };
}
```

4. **Rimuovere listener**: Usa `bind()` e salva il riferimento

```javascript
this.handler = this.handleEvent.bind(this);
element.addEventListener("click", this.handler);
// Poi puoi rimuoverlo
element.removeEventListener("click", this.handler);
```

5. **Array methods**: Arrow functions sono perfette

```javascript
numbers.map((n) => n * this.multiplier);
items.filter((item) => this.isValid(item));
```

## 🔗 Collegamenti

**Prerequisiti**:

- [[this-concept]] - Comprendere il binding di this
- [[this-binding-rules]] - Le regole di binding
- [[funzioni]] - Funzioni JavaScript

**Concetti Correlati**:

- [[this-arrow-functions]] - Arrow functions e lexical this
- [[this-call-apply-bind]] - Metodi bind, call, apply

**Approfondimenti**:

- [[../classi/class-fields]] - Class fields con arrow functions
- [[../promises/promise-chains]] - Promises e this
- [[../eventi/event-handlers]] - Event handler patterns

## 📚 Riferimenti

- **MDN**: [this in callbacks](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
- **MDN**: [Function.prototype.bind()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
- **You Don't Know JS**: this & Object Prototypes - Chapter 2
- **JavaScript.info**: [Arrow functions revisited](https://javascript.info/arrow-functions)

## 📌 Note Personali

[Annotazioni personali sui problemi di this]

---

**Tags**: `#javascript` `#this` `#callbacks` `#binding-loss` `#arrow-functions` `#bind`
