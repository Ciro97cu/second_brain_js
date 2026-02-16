# Metodi Utility Array

Metodi utili per **ricerca**, **verifica** e **copia** di array.

## slice (copia porzione)

Restituisce **shallow copy** di una porzione senza modificare originale.

```javascript
let numeri = [1, 2, 3, 4, 5];
let porzione = numeri.slice(1, 3); // [2, 3] (da 1 a 3, escluso)
console.log(numeri); // [1, 2, 3, 4, 5] (intatto)

// Copia completa
let copia = numeri.slice(); // [1, 2, 3, 4, 5]

// Da indice a fine
let daIndice = numeri.slice(2); // [3, 4, 5]

// Indici negativi (dalla fine)
let ultimi = numeri.slice(-2); // [4, 5]
```

**`slice` vs `splice`**: `slice` copia senza modificare, `splice` modifica originale.

## includes (verifica presenza)

Controlla se array include elemento, restituisce `true`/`false`.

```javascript
let frutti = ["mela", "banana", "arancia"];
console.log(frutti.includes("banana")); // true
console.log(frutti.includes("pera")); // false

// Con indice di partenza
let numeri = [1, 2, 3, 2, 1];
numeri.includes(2, 2); // true (cerca da indice 2)
```

## find (primo elemento)

Restituisce **primo elemento** che soddisfa condizione (o `undefined`).

```javascript
let numeri = [5, 12, 8, 130, 44];
let trovato = numeri.find(function (n) {
  return n > 10;
});
console.log(trovato); // 12

// Con arrow function
let pari = numeri.find((n) => n % 2 === 0); // 12
```

**`find` vs `filter`**: `find` restituisce primo elemento o `undefined`, `filter` restituisce array di tutti gli elementi.

## findIndex (indice elemento)

Come `find` ma restituisce **indice** (o `-1` se non trovato).

```javascript
let numeri = [5, 12, 8, 130, 44];
let indice = numeri.findIndex((n) => n > 10);
console.log(indice); // 1 (posizione di 12)
```

## indexOf (indice valore)

Restituisce indice della prima occorrenza di un valore.

```javascript
let frutti = ["mela", "banana", "arancia", "banana"];
console.log(frutti.indexOf("banana")); // 1
console.log(frutti.indexOf("pera")); // -1 (non trovato)
console.log(frutti.lastIndexOf("banana")); // 3 (ultima occorrenza)
```

## Collegamenti

- [[array]] - Concetti base
- [[array-iterazione]] - forEach, map, filter, reduce
- [[array-manipolazione]] - Modificare array
