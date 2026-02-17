# Tipizzazione Dinamica (Dynamic Typing)

**Tipo**: Nuovo Topic  
**Data**: 13 Febbraio 2026

**Appunti Completi**: [[../../appunti-completi#32-tipizzazione-dinamica-dynamic-typing]]

---

## Descrizione

JavaScript è un linguaggio a tipizzazione dinamica. Questo significa che una variabile non è legata a un tipo di dato specifico. La stessa variabile può contenere un number in un momento, e una string in un momento successivo. Questa flessibilità permette di usare una singola variabile per rappresentare un valore che cambia forma nel corso del programma.

```javascript
let valore = 42;
console.log(typeof valore); // "number"

valore = "Ciao!";
console.log(typeof valore); // "string"

valore = true;
console.log(typeof valore); // "boolean"
```

## Esempio

```javascript
// Una variabile può cambiare tipo
let dato = 100; // number
dato = "Centoventi"; // string
dato = { valore: 100 }; // object

// Problema: errori runtime
function somma(a, b) {
  return a + b;
}
console.log(somma(5, 3)); // 8
console.log(somma("5", 3)); // "53" - concatenazione inattesa!

// Soluzione: validare i tipi
function sommaNumeri(a, b) {
  if (typeof a !== "number" || typeof b !== "number") {
    throw new Error("Argomenti devono essere numeri");
  }
  return a + b;
}
```

## Collegamenti

- [[../variabili/variabili]] - Le variabili in JavaScript hanno tipizzazione dinamica
- [[../../00-introduzione/che-cose-javascript]] - JavaScript è un linguaggio a tipizzazione debole e dinamica
- [[coercizione]] - Conversione esplicita e implicita tra tipi

## Riferimenti

- [MDN - JavaScript data types and data structures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)
- [MDN - typeof operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof)
