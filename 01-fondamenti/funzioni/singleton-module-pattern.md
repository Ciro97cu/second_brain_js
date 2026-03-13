# [[../../appunti-completi#310-il-pattern-modulo-modules|Singleton Module Pattern]]

Il Singleton Module Pattern è una variante del Module Pattern che garantisce la creazione di una singola istanza del modulo. Questo si ottiene tipicamente combinando il Module Pattern con una Immediately Invoked Function Expression (IIFE).

## Implementazione con IIFE

Invece di dichiarare una funzione factory da invocare esplicitamente in seguito, la funzione che definisce il modulo viene eseguita immediatamente. Il valore restituito (l'API pubblica) viene assegnato direttamente a una variabile.

```javascript
var foo = (function CoolModule() {
  var something = "cool";
  var another = [1, 2, 3];

  function doSomething() {
    console.log(something);
  }

  function doAnother() {
    console.log(another.join(" ! "));
  }

  return {
    doSomething: doSomething,
    doAnother: doAnother,
  };
})();
```

## Utilizzo del Singleton

Poiché l'IIFE viene eseguita immediatamente alla valutazione del codice, `foo` non contiene più la funzione factory del modulo, ma direttamente l'oggetto dell'API pubblica restituito.

```javascript
foo.doSomething(); // "cool"
foo.doAnother(); // "1 ! 2 ! 3"
```

In questo approccio, non è possibile creare copie multiple del modulo tramite successive invocazioni; lo stato interno è associato a quell'unica esecuzione dell'IIFE.
