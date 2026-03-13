# [[../../../appunti-completi#new-vs-hard-binding|New vs Hard Binding]]

A sorpresa, anche lo stretto _hard binding_ fornito da `bind()` può essere overridden dall'uso del costruttore, rendendo il _new binding_ in assoluto il più prioritario di tutti.

## La Precedenza Sorprendente

```javascript
function foo(something) {
  this.a = something;
}

var obj1 = {};
var bar = foo.bind(obj1);
bar(2);
console.log(obj1.a); // 2 (bind funziona normalmente)

var baz = new bar(3);
console.log(obj1.a); // 2 (obj1 non modificato da new!)
console.log(baz.a); // 3 (new ha creato nuovo oggetto)
```

**Osservazioni**:

- `bar` è originariamente hard-bound a `obj1` con `bind`.
- Chiamare `bar(2)` imposta coerentemente `obj1.a = 2`.
- Ma `new bar(3)` crea a tutti gli effetti un **nuovo oggetto** con proprietà `a = 3`.
- `obj1.a` non muta e resta `2`.

**`new` sovrascrive anche l'irremovibile hard binding.**

## Il Polyfill di bind

Come fa `new` a sovrascrivere `bind()` se le definizioni primordiali hard-codificano l'origine di un argomento? Il comportamento è cablato all'interno del polyfill interno ufficiale di ES5:

```javascript
// Frammenti del polyfill di bind standard (MDN / TC39)
this instanceof fNOP && oThis ? this : oThis;
```

Questo condizionale controlla esplicitamente:

- **`this instanceof fNOP`**: La funzione è chiamata con `new`?
- **Se sì**: Sceglie il `this` generato poc'anzi.
- **Se no**: Cede al normale `oThis` (_hard binding_).

## Caso D'uso: Partial Application

Se consentire a `new` tale prelevanza contro gli intenti sembrasse strano, ne giova la pratica della _partial application (currying)_.

### Constructor con Parametri Pre-Applicati

```javascript
function person(firstName, lastName, age) {
  this.firstName = firstName;
  this.lastName = lastName;
  this.age = age;
}

// Preset per creare cognomi comuni
var createSmith = person.bind(null, undefined, "Smith");

var john = new createSmith("John", 30);
console.log(john); // { firstName: "John", lastName: "Smith", age: 30 }
```

In sintesi, i primi argomenti vengono bloccati (o saltati con `undefined`) ed a questo non viene affiancato un vero valore per `this` avendovi imposto un parametro dummy quale `null`, che verrebbe comunque sostituito dal provvidenziale intervento di `new`.
