# Expression (Espressione)

**Tipo**: Nuovo Topic  
**Data**: 13 Febbraio 2026

---

## Descrizione

Le istruzioni sono composte da una o più espressioni. Un'espressione è un qualsiasi pezzo di codice che produce un valore, come un riferimento a una variabile o una combinazione di valori e operatori.

## Analisi di un'Espressione

Analizzando l'istruzione `a = b * 2;`, si possono identificare quattro espressioni:

**2** → Un'espressione letterale, il cui valore è semplicemente 2.

**b** → Un'espressione di variabile, che si risolve nel valore contenuto in b.

**b \* 2** → Un'espressione aritmetica, che produce il risultato della moltiplicazione.

**a = b \* 2** → Un'espressione di assegnamento, che assegna il risultato di b \* 2 alla variabile a.

## Istruzione di Espressione

Un'espressione che sta da sola può formare un'intera istruzione, chiamata istruzione di espressione. Sebbene un'istruzione come `b * 2;` sia valida, è poco utile perché il risultato non viene utilizzato. Un esempio molto più comune di istruzione di espressione è una chiamata a una funzione, come `alert(a);`.

## Esempi

```javascript
/*
 * Esempi di espressioni in JavaScript
 */

// Espressioni letterali
42;
("Ciao mondo");
true;

// Espressioni di variabile
let x = 10;
x; // questa è un'espressione che produce il valore 10

// Espressioni aritmetiche
5 + 3; // produce 8
x * 2; // produce 20 (se x vale 10)

// Espressioni di assegnamento
let y = x * 2; // l'intera parte destra è un'espressione

// Espressioni di chiamata a funzione (istruzione di espressione)
console.log("Hello"); // chiama la funzione e produce undefined
alert("Attenzione!"); // mostra un alert

// Espressione complessa
let risultato = (x + 5) * 2 - 3;
/*
 * Questa contiene multiple espressioni:
 * - x (variabile)
 * - 5 (letterale)
 * - x + 5 (aritmetica)
 * - 2 (letterale)
 * - (x + 5) * 2 (aritmetica)
 * - 3 (letterale)
 * - (x + 5) * 2 - 3 (aritmetica)
 * - risultato = ... (assegnamento)
 */
```

## Collegamenti

- [[statement]] - Le istruzioni contengono espressioni
- [[blocchi]] - Le espressioni sono usate nelle istruzioni dei blocchi
- [[../programma]] - Le espressioni sono elementi dei programmi

## Riferimenti

- [MDN - Expressions and operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators)
