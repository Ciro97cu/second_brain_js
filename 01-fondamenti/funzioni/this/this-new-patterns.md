# [[../../../appunti-completi#311-lidentificatore-this|New Binding: Pattern e Convenzioni]]

Nel contesto dell'inizializzazione di oggetti con costruttori, esistono convenzioni e pattern comunemente adottati in JavaScript per garantire l'affidabilità e le prestazioni del codice.

## Convenzione PascalCase

Per **convenzione**, le funzioni designate per essere utilizzate come costruttori vengono nominate utilizzando il **PascalCase** (iniziale maiuscola). Questo segnala agli sviluppatori che la funzione dovrebbe presuntibilmente essere chiamata con `new`.

```javascript
// Costruttore (PascalCase)
function Person(name) {
  this.name = name;
}

// Funzione di utilità o factory (camelCase)
function createPerson(name) {
  return new Person(name);
}

var p1 = new Person("Mario");
var p2 = createPerson("Luigi");
```

Questa prassi non è tuttavia imposta dal linguaggio a livello sintattico:
```javascript
function foo() {
  this.a = 1;
}

var obj = new foo(); // Funziona, sebbene contravvenga alla convenzione
```

## Factory Pattern (Alternativa a new)

Un pattern robusto permette a una funzione costruttrice di funzionare in modo prevedibile indipendentemente dal fatto che venga utilizzata o meno la parola chiave `new`.

```javascript
function Person(name) {
  // Si rileva se la chiamata è avvenuta tramite new
  if (!(this instanceof Person)) {
    return new Person(name);
  }

  this.name = name;
}

var p1 = new Person("Mario"); // Con new
var p2 = Person("Luigi"); // Senza new, viene auto-corretto
```

## Costruttore con Validazione

I costruttori vengono comunemente sfruttati per convalidare i dati di istanziazione, bloccando la creazione di oggetti con stati non validi.

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

var user = new User("Mario", 30); // Esecuzione corretta
// var invalid = new User(); // Genera Error: Name required
```

## Condivisione dei Metodi via Prototype

Per ottimizzare le prestazioni e ridurre il consumo di memoria, i metodi generici non si dovrebbero includere all'interno della funzione costruttrice (poiché se ne creerebbe una nuova istanza per ogni nuovo oggetto). Questi vengono invece collegati al `prototype` del costruttore, rendendoli condivisibili tra tutte le istanze generate.

```javascript
function Person(name) {
  this.name = name;
  
  // Prassi da evitare: ogni istanza conterrebbe una propria copia della funzione
  // this.greet = function() { ... };
}

// Prassi corretta: il metodo viene condiviso globalmente
Person.prototype.greet = function () {
  return "Hello, " + this.name;
};

var mario = new Person("Mario");
var luigi = new Person("Luigi");

console.log(mario.greet === luigi.greet); // true (fanno riferimento allo stesso metodo in memoria)
```
