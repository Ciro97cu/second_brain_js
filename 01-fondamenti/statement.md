# Statement (Istruzione)

**Tipo**: Nuovo Topic  
**Data**: 13 Febbraio 2026

---

## Descrizione

Un'istruzione è un comando che esegue un compito specifico. Un programma è composto da una serie di istruzioni.

## Anatomia di uno Statement

```javascript
let a = 2 * b;
```

Questa istruzione è composta da diverse parti:

### Variabili (a e b)

Sono "contenitori" simbolici che memorizzano valori su cui il programma può operare. Funzionano come segnaposto per i valori stessi.

### Valore Letterale (2)

È un valore scritto direttamente nel codice, che non è stato memorizzato in una variabile.

### Operatori (= e \*)

Sono simboli che eseguono azioni. L'`*` esegue una moltiplicazione, mentre l'`=` assegna il risultato dell'operazione alla variabile a sinistra.

## Punto e virgola

La maggior parte delle istruzioni in JavaScript termina con un punto e virgola (`;`).

## Esempi

```javascript
/*
 * Esempi di diverse istruzioni
 */

// Dichiarazione di variabile
let nome = "Mario";

// Operazione matematica
let risultato = 10 + 5;

// Chiamata di funzione
console.log("Ciao!");

// Istruzione condizionale
if (risultato > 10) {
  console.log("Il risultato è maggiore di 10");
}

// Ciclo
for (let i = 0; i < 3; i++) {
  console.log(i);
}
```

## Collegamenti

- [[programma]] - Un insieme di istruzioni
- [[blocchi]] - I blocchi raggruppano statement
- [[variabili]] - Contenitori di valori
- [[operatori]] - Simboli per eseguire azioni

## Riferimenti

- [MDN - Statements and declarations](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements)
