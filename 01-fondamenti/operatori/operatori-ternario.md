# [[../../appunti-completi#5-operatori|Operatore Ternario]]

L'operatore ternario (`? :`) fornisce una sintassi compatta per esprimere condizioni logiche, rappresentando un'alternativa più concisa al costrutto `if-else` per l'assegnamento di valori.

## Sintassi e Funzionamento

È l'unico operatore in JavaScript a richiedere tre operandi:

```javascript
condizione ? espressioneSeVero : espressioneSeFalso;
```

Il funzionamento prevede la valutazione della `condizione`:

- Se risulta "truthy", viene eseguita e restituita `espressioneSeVero`
- Se risulta "falsy", viene eseguita e restituita `espressioneSeFalso`

## Esempi di Utilizzo

L'uso primario riguarda l'assegnazione condizionale di variabili:

```javascript
// Assegnazione base
let eta = 20;
let tipo = eta >= 18 ? "adulto" : "minore";
console.log(tipo); // "adulto"
```

L'operatore ternario può essere utilizzato direttamente all'interno di espressioni concatenate o interpolazioni:

```javascript
let punti = 85;
console.log("Esito: " + (punti >= 60 ? "passato" : "fallito"));
```

## Operatori Ternari Annidati

È possibile annidare più operatori ternari per gestire scenari con molteplici condizioni, sebbene questa pratica richieda cautela per preservare la leggibilità del codice.

```javascript
let voto = 75;
let giudizio =
  voto >= 90
    ? "Eccellente"
    : voto >= 70
      ? "Buono"
      : voto >= 60
        ? "Sufficiente"
        : "Insufficiente";
console.log(giudizio); // "Buono"
```

In presenza di una logica complessa, spesso si raccomanda l'utilizzo dei costrutti `if-else` tradizionali o `switch` per mantenere il codice maggiormente comprensibile.
