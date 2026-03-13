# [[../../../appunti-completi#Explicit Binding|Explicit Binding: call e apply]]

L'**explicit binding** permette di indicare esplicitamente quale oggetto deve essere utilizzato come `this` durante l'esecuzione di una funzione. Questo approccio forza una funzione a usare uno specifico contesto senza dover mutare l'oggetto stesso.

## call() e apply()

In JavaScript, tutte le funzioni hanno accesso ai metodi `call()` e `apply()`, ereditati tramite `[[Prototype]]`.

Entrambi i metodi:

- Accettano come **primo parametro** l'oggetto da usare come `this`.
- Invocano immediatamente la funzione con il contesto specificato.

```javascript
function foo() {
  console.log(this.a);
}

var obj = {
  a: 2,
};

foo.call(obj); // 2
foo.apply(obj); // 2
```

## Differenze nei Parametri

La differenza tra i due metodi risiede nel modo in cui vengono passati gli argomenti aggiuntivi alla funzione:

- **`call()`**: richiede che gli argomenti siano passati separatamente, uno dopo l'altro.
- **`apply()`**: richiede che gli argomenti siano passati raggruppati all'interno di un array.

```javascript
function somma(b, c) {
  console.log(this.a + b + c);
}

var obj = { a: 1 };

somma.call(obj, 2, 3); // 6
somma.apply(obj, [2, 3]); // 6
```

Una regola mnemonica utile è associare l'iniziale di `apply` con la parola `array` (**A**pply = **A**rray).

## Boxing dei Primitivi

Passando un valore primitivo (`string`, `boolean`, `number`) come argomento per il contesto `this`, JavaScript esegue automaticamente un'operazione chiamata **boxing**. Il valore primitivo viene avvolto nel suo oggetto equivalente (`new String()`, `new Boolean()`, `new Number()`).

```javascript
function showType() {
  console.log(typeof this); // "object"
}

showType.call(42); // [Number: 42]
showType.call("hello"); // [String: 'hello']
showType.call(true); // [Boolean: true]
```
