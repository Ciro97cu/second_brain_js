# [[../../appunti-completi#311-lidentificatore-this|Problemi con il Binding di this]]

Uno dei problemi più comuni in JavaScript è la **perdita del binding di `this`** quando si passano funzioni come callback o handler. Questo accade perché il call-site determina `this`, non il punto di definizione della funzione.

## 🎯 Concetti Chiave

- **Binding loss**: Passare un metodo come callback fa perdere il contesto dell'oggetto
- **Call-site invisibile**: In callback e handler, il call-site è spesso nel codice di librerie/framework
- **Tre soluzioni**: Arrow functions, `bind()`, o variabile `self` (legacy)
- **Arrow functions non sono sempre la risposta**: Non usarle come metodi diretti di oggetti
- **Eccezioni di binding**: `null`/`undefined` vengono ignorati (default binding applicato)
- **DMZ object pattern**: Usa `Object.create(null)` come placeholder sicuro per `this`
- **Riferimenti indiretti**: Assegnazioni come `(p.foo = o.foo)()` producono default binding
- **Soft binding**: Alternativa flessibile a `bind()` che permette override manuali di `this`

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

## 🚨 Eccezioni di Binding

Oltre ai problemi comuni di perdita di binding, ci sono situazioni in cui il comportamento di `this` può essere **sorprendente per design**.

### `null` e `undefined` Vengono Ignorati

Se passi `null` o `undefined` come binding di `this` a `call`, `apply` o `bind`, questi valori vengono **ignorati** e viene applicata la **regola di default binding**:

```javascript
function foo() {
  console.log(this.a);
}

var a = 2;

foo.call(null); // 2 (default binding!)
foo.apply(undefined); // 2 (default binding!)
```

**Perché usare `null`?**

È comune quando non ti interessa il binding di `this` ma hai bisogno di un placeholder:

```javascript
function sum(a, b) {
  return a + b;
}

// Spreading array come parametri
sum.apply(null, [2, 3]); // 5

// Currying con bind
var addTwo = sum.bind(null, 2);
addTwo(3); // 5
```

**⚠️ Il Pericolo di `null`:**

Se la funzione **usa effettivamente `this`**, il default binding può mutare il global object:

```javascript
function dangerous() {
  this.leaked = "oops!"; // Muta window/global!
}

dangerous.call(null);
console.log(window.leaked); // "oops!" (in browser)
```

Questo è particolarmente pericoloso con **funzioni di terze parti** che non controlli.

### Soluzione: DMZ Object (Zona Demilitarizzata)

Usa un oggetto **completamente vuoto** come placeholder sicuro:

```javascript
// Crea oggetto DMZ (più vuoto di {})
var ø = Object.create(null);

function foo(a, b) {
  console.log("a:" + a + ", b:" + b);
}

// Usa ø invece di null
foo.apply(ø, [2, 3]); // a:2, b:3 ✅

var bar = foo.bind(ø, 2);
bar(3); // a:2, b:3 ✅
```

**Perché `Object.create(null)`?**

- `{}` ha delegazione a `Object.prototype`
- `Object.create(null)` è **totalmente vuoto** (no prototype chain)
- Qualsiasi uso accidentale di `this` resta isolato nell'oggetto vuoto

**Simbolo `ø`:**

- U+00F8 (empty set in matematica)
- Su Mac: `⌥+o` (Option-o)
- Nome variabile semantico: "voglio this vuoto"
- Alternativa: chiamalo `emptyThis` o come preferisci

### Confronto: `null` vs DMZ Object

```javascript
function maybeUsesThis(a, b) {
  // Supponiamo non sappiamo se usa this
  if (this && this.log) {
    this.log(a + b);
  }
  return a + b;
}

// ❌ Con null: potenziale global pollution
var result1 = maybeUsesThis.apply(null, [2, 3]);

// ✅ Con DMZ: isolato e sicuro
var ø = Object.create(null);
var result2 = maybeUsesThis.apply(ø, [2, 3]);
```

### Alternative ES6+

**Spread operator** elimina bisogno di `apply`:

```javascript
function foo(a, b, c) {
  return a + b + c;
}

var args = [1, 2, 3];

// ES5: Serve apply (e quindi this placeholder)
foo.apply(null, args); // 6

// ES6: Spread evita il problema
foo(...args); // 6 (no this necessario!)
```

**⚠️ Nota**: Non esiste equivalente ES6 per currying con `bind`, quindi serve ancora il placeholder per `this`.

### Tabella Riepilogativa

| Scenario                       | Problema                         | Soluzione                |
| ------------------------------ | -------------------------------- | ------------------------ |
| `apply(null, array)`           | Global pollution se usa `this`   | Usa DMZ: `apply(ø, arr)` |
| `bind(null, preset)`           | Global pollution se usa `this`   | Usa DMZ: `bind(ø, val)`  |
| Spread array come args         | Serve placeholder per `this`     | ES6: `foo(...arr)` ✅    |
| Currying parametri             | Ancora serve `bind`              | Usa DMZ: `bind(ø, val)`  |
| Funzione 3rd-party sconosciuta | Might mutare global unexpectedly | Sempre usare DMZ object  |

### Indirection (Riferimenti Indiretti)

Un'altra situazione che può causare comportamenti inattesi è la creazione (intenzionale o accidentale) di **"riferimenti indiretti"** alle funzioni. Quando un riferimento indiretto viene invocato, si applica la **regola di default binding**.

Il modo più comune in cui si verificano riferimenti indiretti è tramite **assegnazione**:

```javascript
function foo() {
  console.log(this.a);
}

var a = 2;
var o = { a: 3, foo: foo };
var p = { a: 4 };

o.foo(); // 3 (implicit binding)

(p.foo = o.foo)(); // 2 (default binding!)
```

**Perché accade:**

Il valore risultante dall'espressione `p.foo = o.foo` è un **riferimento diretto all'oggetto funzione sottostante**, non a `p.foo()` o `o.foo()`.

L'effettivo call-site diventa semplicemente `foo()`, quindi si applica il default binding che punta al global object (dove `a = 2`).

**⚠️ Promemoria importante:**

Indipendentemente da **come** si arriva a un'invocazione che usa default binding, è **lo stato strict mode del _contenuto_ della funzione invocata** (non il call-site!) che determina il valore di `this`:

```javascript
"use strict";

function foo() {
  console.log(this.a); // undefined in strict mode
}

var a = 2;

// Funzione in strict mode → this = undefined
(p.foo = o.foo)(); // TypeError: Cannot read property 'a' of undefined
```

```javascript
function foo() {
  // Funzione non-strict
  console.log(this.a);
}

var a = 2;

// Funzione non-strict → this = global
(p.foo = o.foo)(); // 2
```

### Softening Binding (Binding Flessibile)

L'**hard binding** (tramite `bind()`) previene efficacemente una funzione dal ricadere nel default binding, forzandola a usare un `this` specifico. Tuttavia, questo approccio ha un grosso limite: **riduce drasticamente la flessibilità**.

Una volta applicato l'hard binding, è **impossibile** sovrascrivere `this` manualmente tramite:

- Implicit binding (`obj.method()`)
- Explicit binding successivo (`call`, `apply`)
- Solo `new` può sovrascriverlo

Sarebbe utile avere un **default personalizzato** per il default binding (invece di `global` o `undefined`), ma **lasciando comunque la possibilità** di override manuale tramite implicit o explicit binding.

#### Implementazione Soft Binding

Si può creare un'utility `softBind()` che emula questo comportamento:

```javascript
if (!Function.prototype.softBind) {
  Function.prototype.softBind = function (obj) {
    var fn = this;

    /*
     * Cattura eventuali parametri per il currying
     */
    var curried = [].slice.call(arguments, 1);

    var bound = function () {
      /*
       * Controlla this al momento della chiamata:
       * - Se è global/undefined → usa obj (default personalizzato)
       * - Altrimenti → mantieni this attuale (permetti override)
       */
      return fn.apply(
        !this || this === (window || global) ? obj : this,
        curried.concat.apply(curried, arguments),
      );
    };

    bound.prototype = Object.create(fn.prototype);
    return bound;
  };
}
```

**Come funziona:**

1. **Controlla `this` al call-time** (non al binding-time come `bind()`)
2. Se `this` è globale o `undefined` → usa il fallback `obj`
3. Se `this` è stato impostato (implicit/explicit binding) → lo rispetta
4. Supporta currying come `bind()`

#### Esempio d'Uso

```javascript
function foo() {
  console.log("name: " + this.name);
}

var obj = { name: "obj" };
var obj2 = { name: "obj2" };
var obj3 = { name: "obj3" };

var fooOBJ = foo.softBind(obj);

/*
 * Default binding → usa obj come fallback
 */
fooOBJ(); // name: obj

/*
 * Implicit binding → override manuale permesso!
 */
obj2.foo = foo.softBind(obj);
obj2.foo(); // name: obj2 <---- non "obj"!

/*
 * Explicit binding → override permesso!
 */
fooOBJ.call(obj3); // name: obj3 <---- non "obj"!

/*
 * Callback (default binding) → ricade sul soft-binding
 */
setTimeout(obj2.foo, 10); // name: obj
```

**Confronto Soft vs Hard Binding:**

| Caratteristica         | Hard Binding (`bind`) | Soft Binding              |
| ---------------------- | --------------------- | ------------------------- |
| Default personalizzato | ✅ Sì                 | ✅ Sì                     |
| Implicit override      | ❌ No (sempre hard)   | ✅ Sì                     |
| Explicit override      | ❌ No (sempre hard)   | ✅ Sì                     |
| `new` override         | ✅ Sì                 | ✅ Sì                     |
| Callback safety        | ✅ Sì (this fisso)    | ✅ Sì (fallback default)  |
| Flessibilità           | ❌ Bassa (locked)     | ✅ Alta (adattabile)      |
| Use case               | Context permanente    | Default sicuro + override |

**Quando usare soft binding:**

- ✅ Vuoi un default sicuro per callback/timer
- ✅ Devi permettere override in alcuni contesti
- ✅ Funzione usata sia come callback che come metodo
- ❌ Non serve se il context deve essere **sempre** lo stesso (usa `bind()`)

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

6. **Placeholder per `this`**: Usa DMZ object invece di `null`

```javascript
// ❌ Evita
foo.apply(null, args);
var bar = fn.bind(null, preset);

// ✅ Preferisci
var ø = Object.create(null);
foo.apply(ø, args);
var bar = fn.bind(ø, preset);

// ✅ Ancora meglio (ES6+)
foo(...args); // Usa spread operator
```

## 🔗 Collegamenti

**Prerequisiti**:

- [[this-concept]] - Comprendere il binding di this
- [[this-binding-precedence]] - Le regole di binding
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
- **MDN**: [Object.create()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create)
- **You Don't Know JS**: this & Object Prototypes - Chapter 2
- **JavaScript.info**: [Arrow functions revisited](https://javascript.info/arrow-functions)

## 📌 Note Personali

[Annotazioni personali sui problemi di this]

---

**Tags**: `#javascript` `#this` `#callbacks` `#binding-loss` `#arrow-functions` `#bind` `#binding-exceptions` `#dmz-object` `#null-safety` `#indirect-references` `#soft-binding`
