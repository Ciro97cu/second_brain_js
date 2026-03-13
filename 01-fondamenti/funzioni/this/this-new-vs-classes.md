# [[../../../appunti-completi#311-lidentificatore-this|New Binding: Costruttori Tradizionali vs Classi (ES6+)]]

Sebbene il meccanismo alla base dell'istanziazione degli oggetti rimanga largamente il medesimo, l'arrivo di ECMAScript 6 ha standardizzato la sintassi `class`, semplificando l'ereditarietà basata sui prototipi e garantendo comportamenti prevedibili.

## Differenze tra Classi e Constructor Functions

Una `class` di ES6 agisce essenzialmente da costrutto sintattico (un comunissimo *syntactic sugar*) stratificato sui meccanismi classici dei costruttori. Sotto la scocca, gli elaboratori continuano ad appoggiarsi ai medesimi prototipi e princìpi.

### Utilizzo con Constructor Function (Approccio ES5)

In passato, l'istanziazione e i metodi risiedevano su due binari separati ma correlati all'interno della definizione degli oggetti.

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function () {
  return "Hello, " + this.name;
};

var mario = new Person("Mario");
```

### Utilizzo Sintassi a Classi (Approccio ES6+)

Oggi, l'esperienza viene condensata in un unico blocco logico, conferendo alle strutture una vicinanza sintattica maggiore ai concetti canonici della programmazione orientata agli oggetti.

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    return "Hello, " + this.name;
  }
}

var luigi = new Person("Luigi");
```

## Vantaggi del Costrutto Class

Sebbene il risultato in memoria differisca minimamente, transitare verso la sintassi `class` offre molteplici garanzie intrinseche:

- Viene obbligata l'invocazione mediante `new`. Invocare erroneamente la classe come se fosse una mera funzione causerà automaticamente un'eccezione a runtime.
- Risulta garantita maggiore leggibilità e coesione del blocco di codice, mantenendo costruttore e metodi nella stessa struttura d'appartenenza.
- Vengono formalizzati sistemi di derivazione tramite la keyword `extends` e la delega al costruttore superiore con la keyword `super`.
- Vengono esplicitati e standardizzati metodi o proprietà `static`, oltre allo snellimento delle dichiarazioni dei moduli *getter* e *setter*.
