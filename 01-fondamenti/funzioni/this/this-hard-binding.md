# [[../../../appunti-completi#Hard Binding|Hard Binding e bind()]]

Uno dei problemi dell'explicit binding "semplice" è che una funzione può ancora perdere il proprio contesto, per esempio quando passata come callback in funzioni asincrone come `setTimeout`. Per risolvere questo ostacolo si ricorre all'**Hard Binding**.

## Il Pattern Hard Binding

L'obiettivo è "congelare" il valore di `this` avvolgendo l'invocazione originale in una funzione wrapper che garantisca l'uso di un contesto specifico.

```javascript
function foo() {
  console.log(this.a);
}

var obj = { a: 2 };

var bar = function () {
  foo.call(obj); // Chiusura (closure) che forza il contesto
};

bar(); // 2
setTimeout(bar, 100); // 2
bar.call(window); // 2 (il contesto non può essere sovrascritto)
```

## Function.prototype.bind()

Dal rilascio di ES5, JavaScript include un'utilità nativa per applicare l'hard binding: `Function.prototype.bind()`.

Il metodo `bind()` restituisce una **nuova funzione**, codificata per invocare la funzione originale con il valore di `this` specificato, indipendentemente da come la nuova funzione viene chiamata.

```javascript
function foo(something) {
  return this.a + something;
}

var obj = { a: 2 };
var bar = foo.bind(obj);

console.log(bar(3)); // 5
```

### Partial Application e Doppio Bind

Oltre al binding del contesto, `bind()` consente di pre-applicare uno o più argomenti iniziali (currying o partial application).

```javascript
function multiply(a, b) {
  return this.multiplier * a * b;
}

var obj = { multiplier: 10 };
var multiplyBy2 = multiply.bind(obj, 2);

console.log(multiplyBy2(5)); // 100
```

Un aspetto cruciale da ricordare è che l'output di un'operazione di `bind()` crea una funzione il cui contesto è "sigillato". Se si tenta di applicare `bind()` su una funzione che ha già subito del binding, il nuovo contesto verrà ignorato:

```javascript
var obj1 = { a: 1 };
var obj2 = { a: 2 };

function foo() {
  console.log(this.a);
}

var bar = foo.bind(obj1);
var baz = bar.bind(obj2);

baz(); // 1 (il primo binding non può essere sovrascritto)
```
