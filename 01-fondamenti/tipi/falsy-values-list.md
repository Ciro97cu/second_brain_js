# [[../../appunti-completi#Valori Falsy|Lista dei Valori Falsy]]

I valori **falsy** sono quelli che, quando analizzati in un contesto booleano (coercizione booleana), vengono convertiti in `false`.

La specificità dei valori falsy in JavaScript è che costituiscono una **lista chiusa e ben definita**.

## Lista Completa dei Valori Falsy

Il linguaggio definisce esattamente 7 valori che restituiscono `false`:

```javascript
/*
 * I soli valori falsy in JavaScript
 */

false; // Il valore booleano false
0; // Il numero zero
-0; // Lo zero negativo (IEEE 754)
0n; // Il BigInt zero
(""); // La stringa vuota (valida con '', "", o ``)
null; // L'assenza intenzionale di valore
undefined; // Il valore non definito o variabile non inizializzata
NaN; // Not a Number (risultato matematico invalido)
```

**Ogni singolo valore che non rientra esattamente in questo elenco è automaticamente considerato truthy.**

## Comportamenti Pratici

Quando questi valori vengono utilizzati all'interno di un'istruzione condizionale, il ramo corrispondente non viene mai eseguito, poiché la condizione si valuta come falsa.

```javascript
/*
 * Nessuno di questi blocchi viene eseguito
 */

let stringaVuota = "";
if (stringaVuota) {
  // Non eseguito
}

let numeroZero = 0;
if (numeroZero) {
  // Non eseguito
}

let valoreAssente = null;
if (valoreAssente) {
  // Non eseguito
}
```

## Controllo di Esistenza

Grazie a questa lista definita, il controllo sull'esistenza o sulla valorizzazione di una stringa o di un oggetto può essere semplificato, omettendo confronti espliciti multipli.

```javascript
// Validazione stringa (considera falsy sia stringa vuota che assenza di valore variables)
let userInput = "";
let messaggio = userInput || "Messaggio di default";

console.log(messaggio); // "Messaggio di default"
```
