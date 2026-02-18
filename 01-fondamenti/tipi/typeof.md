# [[../../appunti-completi#31-valori-e-tipi-values--types|typeof]]

L'operatore `typeof` è un operatore unario che esamina un valore e restituisce una stringa indicante il tipo di quel valore.

## Caratteristica Fondamentale

`typeof` agisce sul **valore** contenuto nella variabile in quel momento, non sulla variabile stessa. Per questo, con la tipizzazione dinamica, può restituire risultati diversi per la stessa variabile in momenti diversi.

## Casi Speciali

- `typeof null` → `"object"` ⚠️ (bug storico di JavaScript, mai corretto per retrocompatibilità)
- `typeof NaN` → `"number"` (NaN è considerato un numero speciale)
- `typeof []` → `"object"` (array sono oggetti)
- `typeof function(){}` → `"function"` (caso speciale per funzioni, anche se sono oggetti)

## Valori Restituiti

```
"string"    → stringhe
"number"    → numeri (inclusi NaN, Infinity, -Infinity)
"boolean"   → true/false
"undefined" → undefined o variabili non dichiarate
"object"    → oggetti, array, null
"symbol"    → symbol
"function"  → funzioni
"bigint"    → BigInt (ES2020)
```

## Esempio di Riferimento

```javascript
/* typeof - Verifica del tipo */

// Primitivi
console.log(typeof "Ciao"); // "string"
console.log(typeof 42); // "number"
console.log(typeof true); // "boolean"
console.log(typeof undefined); // "undefined"
console.log(typeof Symbol("id")); // "symbol"

// Casi speciali
console.log(typeof null); // "object" ⚠️ bug storico
console.log(typeof NaN); // "number"
console.log(typeof Infinity); // "number"

// Oggetti e funzioni
console.log(typeof {}); // "object"
console.log(typeof []); // "object"
console.log(typeof new Date()); // "object"
console.log(typeof function () {}); // "function"

// Tipizzazione dinamica
let x = "testo";
console.log(typeof x); // "string"
x = 100;
console.log(typeof x); // "number"

// Uso pratico: validazione input
function somma(a, b) {
  if (typeof a !== "number" || typeof b !== "number") {
    throw new Error("Argomenti devono essere numeri");
  }
  return a + b;
}

console.log(somma(5, 3)); // 8
// somma("5", 3);                // Error: Argomenti devono essere numeri

// Sicurezza: verificare senza errori
if (typeof varInesistente === "undefined") {
  console.log("Variabile non esiste"); // No ReferenceError
}

// Distinguere null da undefined
let val = null;
console.log(typeof val === "object" && val === null); // true ✅
console.log(val === null); // true (modo migliore)

// Array: meglio usare Array.isArray()
let arr = [1, 2, 3];
console.log(typeof arr); // "object" (non specifico)
console.log(Array.isArray(arr)); // true ✅ (metodo corretto)
```

## Punti Chiave

1. **typeof null**: Restituisce `"object"` per bug storico. Usare `x === null` per verificare null

2. **Array vs Object**: `typeof` restituisce `"object"` per entrambi. Usare `Array.isArray()` per distinguere

3. **Variabili inesistenti**: `typeof varInesistente` non genera ReferenceError, restituisce `"undefined"`

4. **NaN**: Restituisce `"number"`. Per verificare NaN usare `isNaN()` o `Number.isNaN()`

5. **Funzioni**: Unico caso in cui `typeof` restituisce un valore diverso da un tipo primitivo (`"function"`)

6. **Validazione runtime**: Utile per verificare tipi prima di operazioni che richiedono tipi specifici

## Collegamenti

- [[valori-tipi]] - I tipi che typeof può identificare
- [[tipizzazione-dinamica]] - typeof riflette il tipo corrente del valore
- [[../operatori]] - typeof è un operatore unario
