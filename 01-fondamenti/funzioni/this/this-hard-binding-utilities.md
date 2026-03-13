# [[../../../appunti-completi#API Context|API Call Contexts e Pattern Comuni]]

L'uso di esplicito del `this` si ritrova spesso in metodologie comuni e nelle utility messe a disposizione dalle API native di JavaScript.

## Funzioni Built-in con Parametro Context

Molte funzioni integrate, in particolare i metodi degli array come `forEach()`, `map()`, `filter()`, accettano un parametro opzionale per fornire il contesto. Questo evita la necessità di usare `bind()` sulle funzioni di callback passate come argomenti.

```javascript
function foo(el) {
  console.log(el, this.id);
}

var obj = { id: "awesome" };

// Il secondo parametro stabilisce esplicitamente il "this" per il callback
[1, 2, 3].forEach(foo, obj);
// 1 awesome
// 2 awesome
// 3 awesome
```

Internamente, questi metodi ricorrono a `call()` o `apply()` per impostare il contesto della callback. Lo stesso principio è valido per `some()` o `every()`.

## Borrowing di Metodi

Uno degli utilizzi più noti di `call()` e `apply()` è il "method borrowing" (prendere in prestito metodi). Permette di utilizzare la funzione appartenente a un oggetto nel contesto di un altro oggetto che ne è sprovvisto.

```javascript
function speak() {
  console.log(`${this.sound}! Type: ${this.type}`);
}

var cat = { type: "cat", sound: "Meow" };
var dog = { type: "dog", sound: "Woof" };

speak.call(cat); // "Meow! Type: cat"
speak.call(dog); // "Woof! Type: dog"
```

## Array-like Objects e Argomenti

In contesti precedenti all'introduzione dello spread operator di ES6, un pattern diffuso per convertire l'oggetto speciale `arguments` in un vero array consisteva nel prendere in prestito il metodo `slice` dagli Array.

```javascript
function convertArgs() {
  // arguments non è un array reale
  var args = Array.prototype.slice.call(arguments);
  return args;
}

var result = convertArgs(1, 2, 3);
console.log(Array.isArray(result)); // true
```

Tutti questi pattern mostrano la potenza pratica fornita dal controllo esplicito del binding introdotto da `call`, `apply` e dalle API costruite per interagirci dinamicamente.
