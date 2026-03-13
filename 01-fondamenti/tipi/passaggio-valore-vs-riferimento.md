# [[../../appunti-completi#passaggio-parametri-e-tipi|Passaggio di Parametri per Valore vs Riferimento]]

Il modo in cui le variabili vengono elaborate durante il passaggio come argomenti alle funzioni varia radicalmente a seconda che si stia manipolando un tipo primitivo o un oggetto.

## Primitivi: Passaggio per Valore

I tipi primitivi (string, number, boolean, null, undefined, symbol) sono immutabili e vengono assegnati **per valore**. Durante il passaggio di una variabile primitiva a una funzione, si esegue una copia indipendente di essa. Le modifiche non si ripercuotono sull'originale.

```javascript
function modificaPrimitivo(x) {
  x = 100;
}

let num = 42;
modificaPrimitivo(num);
console.log(num); // 42 (il valore originale è rimasto invariato)
```

## Oggetti: Passaggio per Riferimento

Le funzioni, gli array e qualsivoglia oggetto in JavaScript vengono assegnati **per riferimento** (reference). In seguito all'assegnazione, la variabile non detiene materialmente tutti i contenuti originari, ma contiene un riferimento (puntatore) ad un'area di memoria in cui le proprietà sono collocate.

Passare un oggetto a una funzione equivale a fornire quel medesimo riferimento. Di conseguenza, eventuali alterazioni alle specifiche proprietà dell'oggetto risultano immediatamente visibili all'esterno.

```javascript
// Oggetti
function modificaOggetto(obj) {
  obj.valore = 100;
}

let oggetto = { valore: 42 };
modificaOggetto(oggetto);
console.log(oggetto.valore); // 100 (l'originale è modificato!)

// Array (è anch'esso valutato come reference)
function modificaArray(arr) {
  arr.push(4);
}

let lista = [1, 2, 3];
modificaArray(lista);
console.log(lista); // [1, 2, 3, 4] (l'originale è modificato)
```

### Isolamento o Re-Assegnazione?

Occorre sottolineare che il riferimento all'oggetto è tale finché non viene riassegnata interamente la variabile referenziante. Se all'interno della funzione si tenta di re-inizializzare (`=`) il medesimo argomento a un differente oggetto strutturato, non si ottiene un'alterazione del costrutto esterno originale, ma semplicemente si re-indirizza il riferimento locale della funzione.