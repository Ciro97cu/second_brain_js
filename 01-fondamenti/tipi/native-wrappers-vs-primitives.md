# [[../../appunti-completi#35-boxing-e-metodi-dei-primitivi|Wrapper Objects vs Primitivi]]

JavaScript fornisce oggetti built-in con nomi che sembrano corrispondere ai tipi primitivi: `String`, `Number`, `Boolean`, `Object`, `Function`, `Array`, `Date`, `RegExp`, `Error`.

I nomi con iniziale maiuscola possono far pensare a tipi o classi come in altri linguaggi orientati agli oggetti, ma in realtà in JavaScript sono funzioni che possono essere usate come costruttori con l'operatore `new`.

## Differenza tra Primitivo e Wrapper Object

```javascript
/* Primitivo */
var strPrimitive = "I am a string";
console.log(typeof strPrimitive); // "string"
console.log(strPrimitive instanceof String); // false

/* Wrapper Object built-in */
var strObject = new String("I am a string");
console.log(typeof strObject); // "object"
console.log(strObject instanceof String); // true

/*
 * Ispezionando il sottotipo interno:
 */
console.log(Object.prototype.toString.call(strObject)); // "[object String]"
/*
 * Conferma che strObject è un oggetto
 * creato dal costruttore String
 */
```

## Pratica Raccomandata: Preferire la Forma Letterale

La regola fondamentale in JavaScript per quanto riguarda l'istanziazione di stringhe, numeri e booleani è di preferire sempre la forma letterale alla forma costruita. Il motore JavaScript gestirà il boxing quando necessario, permettendo di mantenere un codice più pulito ed evitare le insidie dei tipi oggetto.

```javascript
/* ✅ PREFERITO: Forma letterale primitiva */
var str1 = "hello";
var num1 = 42;
var bool1 = true;

/* ❌ EVITARE: Wrapper espliciti inutili */
var str2 = new String("hello");
var num2 = new Number(42);
var bool2 = new Boolean(true);

console.log(typeof str1); // "string"
console.log(typeof str2); // "object" (!)
```

## Casi Speciali

Mentre la forma letterale è preferibile in quasi tutti i casi, ci sono delle notevoli eccezioni:
- `Date` richiede sempre il costruttore, poiché non esiste una forma letterale.
- `Error` viene solitamente creato automaticamente nei blocchi catch e si consiglia il costruttore tramite `throw new Error("msg")`.
- `Array`, `RegExp`, `Function`: usare la rispettiva versione letterale anziché usare `new` quando disponibile.
- I primitivi `null` e `undefined` non hanno alcun costruttore associato, solo il loro valore primitivo.

## Collegamenti

- [[boxing-concept]] - Il processo di boxing implicito
- [[object-wrappers-caveats]] - Comportamenti confusi causati dai wrapper objects espliciti
- [[../oggetti/object-literal-vs-constructed]] - Object literal vs built-ins
