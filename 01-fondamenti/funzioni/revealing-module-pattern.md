# [[../../appunti-completi#310-il-pattern-modulo-modules|Revealing Module Pattern]]

Il Revealing Module Pattern è una variante standard per l'implementazione del Module Pattern in JavaScript. L'obiettivo è definire tutte le funzioni e le variabili nello scope privato e restituire un oggetto anonimo con puntatori diretti alle funzioni o variabili che si desidera rendere pubbliche.

## Struttura del Pattern

Nel pattern Revealing Module, la struttura tipica prevede l'esecuzione di una funzione esterna (che fa da factory) la quale restituisce un'API pubblica:

```javascript
function CoolModule() {
  var something = "cool";
  var another = [1, 2, 3];

  function doSomething() {
    console.log(something);
  }

  function doAnother() {
    console.log(another.join(" ! "));
  }

  // Rivelazione dei metodi pubblici
  return {
    doSomething: doSomething,
    doAnother: doAnother,
  };
}
```

## Utilizzo

Invocando la funzione esterna, si crea un'istanza del modulo. I metodi dell'oggetto restituito mantengono una closure sulle variabili interne:

```javascript
var foo = CoolModule();

foo.doSomething(); // "cool"
foo.doAnother(); // "1 ! 2 ! 3"
```

Questo approccio permette di mantenere nascosti i dettagli implementativi (come `something` e `another`) esponendo solo ciò che è necessario per l'interazione con il modulo.
