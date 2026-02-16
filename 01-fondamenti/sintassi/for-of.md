# Ciclo for...of

Introdotto in **ES6**, il ciclo `for...of` è il modo moderno e più leggibile per iterare sugli elementi di una **struttura iterabile**, come un array o una stringa.

Ad ogni iterazione, la variabile del ciclo assume il **valore** dell'elemento corrente.

## Sintassi

```javascript
/*
 * Sintassi for...of
 */

for (let elemento of iterabile) {
  // lavora con elemento
}
```

## Esempi con Array

```javascript
/*
 * Iterare su array
 */

let frutti = ["mela", "banana", "arancia"];

for (let frutto of frutti) {
  console.log(frutto);
}

// Output:
// "mela"
// "banana"
// "arancia"
```

## Esempi con Stringhe

```javascript
/*
 * Iterare sui caratteri di una stringa
 */

let parola = "ciao";

for (let carattere of parola) {
  console.log(carattere);
}

// Output:
// "c"
// "i"
// "a"
// "o"
```

## Confronto for vs for...of

```javascript
/*
 * for tradizionale (con indice)
 */

let numeri = [10, 20, 30];

for (let i = 0; i < numeri.length; i++) {
  console.log(numeri[i]); // Devi accedere con [i]
}

/*
 * for...of (diretto sul valore)
 */

for (let numero of numeri) {
  console.log(numero); // Hai direttamente il valore
}
```

## Vantaggi

✅ **Più leggibile** - La sintassi è chiara e concisa

✅ **Meno propenso agli errori** - Niente indici fuori range

✅ **Universale** - Funziona con qualsiasi iterabile (array, stringhe, Set, Map, ecc.)

## const vs let

```javascript
/*
 * ✅ Usa const quando non riassegni
 */

for (const item of array) {
  console.log(item);
  // item non viene riassegnato
}

/*
 * Usa let solo se devi modificare
 */

for (let item of array) {
  item = item * 2; // Riassegnazione
  console.log(item);
}
```

## Quando Usare for...of

Il `for...of` è ideale quando:

- Devi iterare su **valori** (non indici)
- Non ti servono gli indici
- Vuoi codice più leggibile
- Lavori con iterabili (array, stringhe, Set, Map)

## Quando NON Usare for...of

- Se ti servono gli indici (usa `for` tradizionale)
- Se devi iterare su **proprietà di oggetti** (usa `for...in`)
- Se devi modificare l'array stesso (rischio di comportamenti inattesi)

## Collegamenti

- [[for]] - Ciclo for tradizionale (con indici)
- [[for-in]] - Ciclo for...in (per proprietà oggetti)
- [[while]] - Ciclo while
- [[../array/array-iterazione]] - Metodi di iterazione array (forEach, map, filter)
