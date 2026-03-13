# [[../../../appunti-completi#311-lidentificatore-this|New Binding: Algoritmo e Funzionamento]]

Quando una funzione viene invocata preceduta dalla parola chiave `new`, si effettua una **constructor call**. In questo caso, `this` viene impostato a un nuovo oggetto creato appositamente.

## Concetti Chiave

- **Constructor call**: una funzione invocata con `new`.
- **Nuovo oggetto**: `new` crea automaticamente un oggetto.
- **Auto-return**: il nuovo oggetto viene ritornato automaticamente.
- **Assenza di classi storiche**: in JavaScript pre-ES6, le "constructor functions" sono funzioni normali.

## Cos'è una Constructor Call

In JavaScript, l'aggiunta di `new` davanti a una chiamata di funzione la trasforma in una **constructor call**.

```javascript
function Foo() {
  // Invocata come constructor
}

var bar = new Foo(); // Constructor call
```

Non esistono vere e proprie "constructor functions" a livello di linguaggio base, ma solo **constructor calls** di normali funzioni.

```javascript
function foo(a) {
  this.a = a;
}

// Può essere chiamata in entrambi i modi:
foo(2); // Normal call (default binding)
var bar = new foo(2); // Constructor call (new binding)
```

## I 4 Passaggi del `new`

Quando una funzione viene invocata con `new`, il motore JavaScript esegue automaticamente **4 operazioni**:

### 1. Creazione Nuovo Oggetto

Un nuovo oggetto vuoto viene creato sul momento.

### 2. Link Prototipale

Il nuovo oggetto viene collegato tramite `[[Prototype]]` al prototipo della funzione costruttrice.

### 3. Effettuazione del Binding di `this`

Il nuovo oggetto diventa il binding di `this` per l'esecuzione di quella specifica chiamata di funzione.

### 4. Ritorno Automatico

La funzione ritorna automaticamente il nuovo oggetto appena costruito, a meno che non venga specificato un diverso ritorno esplicito di un oggetto.

```javascript
function Foo(name) {
  // 1. {} viene creato
  // 2. {} viene [[Prototype]]-linked a Foo.prototype
  // 3. this = {}

  this.name = name;

  // 4. viene effettuato un return automatico di this
}

var bar = new Foo("bar");
console.log(bar.name); // "bar"
```

## Esempi di Base

### Costruttore Semplice

```javascript
function Person(name) {
  this.name = name;
}

var mario = new Person("Mario");

console.log(mario.name); // "Mario"
console.log(mario instanceof Person); // true
```

### Constructor con Proprietà e Metodi

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
