# [[../../../appunti-completi#311-lidentificatore-this|New Binding (Regola 4)]]

Quando una funzione viene invocata con `new` davanti, chiamata **constructor call**, `this` viene impostato al nuovo oggetto creato.

## 🎯 Concetti Chiave

- **Constructor call**: Funzione invocata con `new`
- **Nuovo oggetto**: `new` crea automaticamente un oggetto
- **Auto-return**: Il nuovo oggetto viene ritornato automaticamente
- **Non sono classi**: Le "constructor functions" sono funzioni normali
- **Convenzione PascalCase**: Nomi con maiuscola per indicare uso con `new`

## 🛠️ Cos'è una Constructor Call

In JavaScript, quando metti `new` davanti a una chiamata di funzione, questa diventa una **constructor call**.

```javascript
function Foo() {
  // Invocata come constructor
}

var bar = new Foo(); // Constructor call
```

⚠️ **Attenzione**: Non esistono "constructor functions", solo **constructor calls** di funzioni normali!

```javascript
function foo(a) {
  this.a = a;
}

// Può essere chiamata in ENTRAMBI i modi:
foo(2); // Normal call (default binding)
var bar = new foo(2); // Constructor call (new binding)
```

## 🏗️ I 4 Step del `new`

Quando una funzione viene invocata con `new`, JavaScript fa automaticamente **4 cose**:

### 1️⃣ Creazione Nuovo Oggetto

Un **brand new object** viene creato (out of thin air)

### 2️⃣ Link Prototipale

Il nuovo oggetto viene `[[Prototype]]`-linked

### 3️⃣ `this` Binding

Il nuovo oggetto diventa il `this` binding per quella funzione call

### 4️⃣ Auto Return

La funzione ritorna automaticamente il nuovo oggetto (a meno che non ritorni manualmente un altro object)

```javascript
function Foo(name) {
  // 1. {} viene creato
  // 2. {} viene [[Prototype]]-linked
  // 3. this = {}

  this.name = name;

  // 4. return this (implicito)
}

var bar = new Foo("bar");
console.log(bar.name); // "bar"
```

## 💻 Esempi Base

### Constructor Semplice

```javascript
function Person(name) {
  this.name = name;
}

var mario = new Person("Mario");

console.log(mario.name); // "Mario"
console.log(mario instanceof Person); // true
```

### Con Proprietà e Metodi

```javascript
function Car(make, model) {
  this.make = make;
  this.model = model;
  this.describe = function () {
    return this.make + " " + this.model;
  };
}

var myCar = new Car("Toyota", "Corolla");

console.log(myCar.describe()); // "Toyota Corolla"
```

### Confronto Normal vs Constructor Call

```javascript
function foo(a) {
  this.a = a;
}

// Normal call (default binding)
foo(2);
console.log(window.a); // 2 (in non-strict mode)

// Constructor call (new binding)
var bar = new foo(2);
console.log(bar.a); // 2
console.log(window.a); // undefined (nessun effetto su global)
```

## 🔄 Comportamento del Return

### Return Implicito (Normale)

Senza `return`, viene ritornato automaticamente il nuovo oggetto:

```javascript
function Foo(name) {
  this.name = name;
  // No return statement
}

var obj = new Foo("test");
console.log(obj.name); // "test" (obj è il nuovo oggetto)
```

### Return Esplicito di Object

Se ritorni manualmente un **object**, sovrascrive l'auto-return:

```javascript
function Foo() {
  this.name = "foo";

  // Return esplicito di object
  return {
    name: "bar",
  };
}

var obj = new Foo();
console.log(obj.name); // "bar" (return vince!)
```

### Return di Primitivo (Ignorato)

Se ritorni un **primitivo**, viene ignorato:

```javascript
function Foo(name) {
  this.name = name;

  return 42; // Primitivo, viene ignorato
}

var obj = new Foo("test");
console.log(obj.name); // "test" (comportamento normale)
console.log(obj); // { name: "test" } (non 42)
```

**Regola**: Solo `return` di **object** sovrascrive il comportamento di `new`.

## 📐 Convenzione: PascalCase

Per **convenzione**, funzioni pensate per essere usate come constructors usano **PascalCase**:

```javascript
// Constructor (PascalCase)
function Person(name) {
  this.name = name;
}

// Utility function (camelCase)
function createPerson(name) {
  return new Person(name);
}

var p1 = new Person("Mario"); // ✅
var p2 = createPerson("Luigi"); // ✅
```

⚠️ È solo **convenzione**, non enforced da JavaScript:

```javascript
function foo() {
  this.a = 1;
}

var obj = new foo(); // Funziona, ma va contro convezione
```

## 🔍 Verifica instanceof

Puoi verificare se un oggetto è stato creato da un constructor con `instanceof`:

```javascript
function Person(name) {
  this.name = name;
}

var mario = new Person("Mario");

console.log(mario instanceof Person); // true
console.log(mario instanceof Object); // true (tutto è Object)
```

`instanceof` controlla la catena `[[Prototype]]`.

## 💻 Pattern Comuni

### Factory Pattern (Alternative a new)

```javascript
function Person(name) {
  // Supporta chiamata con o senza new
  if (!(this instanceof Person)) {
    return new Person(name);
  }

  this.name = name;
}

var p1 = new Person("Mario"); // Con new
var p2 = Person("Luigi"); // Senza new, auto-corretto
```

### Constructor con Validazione

```javascript
function User(name, age) {
  if (!name) {
    throw new Error("Name required");
  }
  if (age < 0) {
    throw new Error("Age must be positive");
  }

  this.name = name;
  this.age = age;
}

var user = new User("Mario", 30); // ✅
var invalid = new User(); // ❌ Error: Name required
```

### Condivisione Metodi (Prototype)

Per **performance**, metti metodi sul `prototype` invece che su ogni istanza:

```javascript
function Person(name) {
  this.name = name;

  // ❌ Ogni istanza ha una copia
  // this.greet = function() { ... };
}

// ✅ Condiviso tra tutte le istanze
Person.prototype.greet = function () {
  return "Hello, " + this.name;
};

var mario = new Person("Mario");
var luigi = new Person("Luigi");

console.log(mario.greet === luigi.greet); // true (stesso metodo)
```

## ⚠️ Gotcha

### Dimenticare `new`

Chiamare constructor senza `new` applica **default binding**:

```javascript
function Person(name) {
  this.name = name;
}

var p = Person("Mario"); // ❌ Dimenticato new

console.log(p); // undefined (no return)
console.log(window.name); // "Mario" (global pollution!)
```

**Soluzioni**:

1. Usa `class` (ES6+) che forza `new`
2. Check `this instanceof Constructor`
3. Usa linter per warning

### new con Arrow Functions

Le **arrow functions** non possono essere usate come constructors:

```javascript
const Foo = () => {
  this.a = 1;
};

var obj = new Foo(); // ❌ TypeError: Foo is not a constructor
```

Arrow functions non hanno concept di constructor call.

### new sovrascrive bind

`new` ha **precedenza** su hard binding:

```javascript
function Foo(name) {
  this.name = name;
}

var obj1 = {};

var Bar = Foo.bind(obj1);
Bar("obj1");
console.log(obj1.name); // "obj1"

var obj2 = new Bar("obj2");
console.log(obj1.name); // "obj1" (non cambiato)
console.log(obj2.name); // "obj2" (new ha creato nuovo oggetto)
```

Vedi [[this-binding-precedence]] per dettagli.

## ✅ Best Practices

1. **PascalCase**: Usa per constructor functions
2. **Avoid manual return**: Lascia che `new` gestisca return
3. **Prototype per metodi**: Condividi metodi via prototype
4. **Preferisci class**: In codice moderno, usa `class` (ES6+)
5. **instanceof**: Usa per type checking

## 🆚 class vs Constructor Function

ES6+ offre sintassi `class`, che è **sugar syntax** su constructor functions:

```javascript
// Constructor Function (ES5)
function Person(name) {
  this.name = name;
}
Person.prototype.greet = function () {
  return "Hello, " + this.name;
};

// Class (ES6+)
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    return "Hello, " + this.name;
  }
}

// Entrambi funzionano allo stesso modo
var mario = new Person("Mario");
```

**Differenze**:

- `class` forza uso di `new` (nessun `new` = error)
- `class` più leggibile e familiare (stile OOP)
- `class` ha super, static, getters/setters built-in

## 🔗 Collegamenti

**Prerequisiti**:

- [[this-concept]] - Comprendere cos'è this
- [[this-binding-default]] - Default binding (regola 1)
- [[this-binding-implicit]] - Implicit binding (regola 2)
- [[this-binding-explicit]] - Explicit binding (regola 3)

**Correlati**:

- [[this-binding-precedence]] - New ha precedenza massima
- [[prototype-chains]] - Come funziona [[Prototype]]

**Errori Comuni**:

- [[this-binding-problems]] - Dimenticare new

## 📚 Riferimenti

- **You Don't Know JS**: this & Object Prototypes - Chapter 2
- **MDN**: [new operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new)
- **MDN**: [instanceof](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/instanceof)
- **MDN**: [Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)

## 📌 Note Personali

[Spazio per annotazioni personali sul new binding]

---

**Tags**: `#javascript` `#this` `#new-binding` `#constructor` `#new-operator` `#class`
