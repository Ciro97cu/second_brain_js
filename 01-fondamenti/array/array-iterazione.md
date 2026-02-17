# Iterazione e Trasformazione Array

**Appunti Completi**: [[../../appunti-completi#37-array]]

Metodi **higher-order functions** che eseguono operazioni su ogni elemento. Molti creano **nuovo array** senza modificare l'originale.

## forEach (esecuzione)

Esegue una funzione per ogni elemento. **Non restituisce** nuovo array.

```javascript
let numeri = [1, 2, 3];
numeri.forEach(function (numero) {
  console.log(numero * 2); // 2, 4, 6
});
// numeri rimane [1, 2, 3]
```

Usato per **side effects** (console.log, modifiche DOM), non per trasformazioni.

## map (trasformazione)

Crea **nuovo array** applicando una funzione a ogni elemento.

```javascript
let numeri = [1, 2, 3];
let doppi = numeri.map(function (n) {
  return n * 2;
});
console.log(doppi); // [2, 4, 6]
console.log(numeri); // [1, 2, 3] (originale intatto)

// Arrow function
let tripli = numeri.map((n) => n * 3); // [3, 6, 9]
```

## filter (selezione)

Crea **nuovo array** con elementi che superano un test (funzione restituisce `true`).

```javascript
let numeri = [1, 2, 3, 4, 5];
let pari = numeri.filter(function (n) {
  return n % 2 === 0;
});
console.log(pari); // [2, 4]

// Arrow function
let maggioriDi2 = numeri.filter((n) => n > 2); // [3, 4, 5]
```

## reduce (aggregazione)

**"Riduce"** array a singolo valore applicando funzione accumulatore.

```javascript
let numeri = [1, 2, 3, 4];
let somma = numeri.reduce(function (acc, val) {
  return acc + val;
}, 0); // 0 è valore iniziale
console.log(somma); // 10

// Esempio: trovare massimo
let max = numeri.reduce((acc, val) => (val > acc ? val : acc));
// max = 4
```

**Parametri**: `reduce(callback(accumulatore, valore, indice, array), valoreIniziale)`

## Pattern Comuni

```javascript
// Concatenare trasformazioni
let numeri = [1, 2, 3, 4, 5];
let risultato = numeri
  .filter((n) => n % 2 === 0) // [2, 4]
  .map((n) => n * 2) // [4, 8]
  .reduce((sum, n) => sum + n, 0); // 12
```

## Collegamenti

- [[array]] - Concetti base
- [[array-manipolazione]] - Modificare array
- [[../funzioni/funzioni]] - Le callback sono funzioni
