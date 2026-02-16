# Hoisting delle Variabili

**Tipo**: Nuovo Topic  
**Data**: 13 Febbraio 2026

---

## Descrizione

L'hoisting (letteralmente "sollevamento") è un meccanismo di JavaScript che riguarda il modo in cui le dichiarazioni di variabili vengono processate dal motore del linguaggio. Durante la fase di compilazione, che precede l'esecuzione, è come se le dichiarazioni venissero concettualmente "sollevate" in cima al loro scope di appartenenza.

Tuttavia, il comportamento dell'hoisting cambia radicalmente a seconda della parola chiave usata per la dichiarazione: var, let o const.

## Hoisting con var

Quando si dichiara una variabile con var, solo la dichiarazione viene sollevata, non l'assegnazione del valore. Questo significa che la variabile esiste in tutto il suo scope fin dall'inizio, ma il suo valore sarà undefined fino a quando il codice non raggiunge il punto in cui le viene assegnato un valore.

```javascript
console.log(nome); // undefined (non ReferenceError!)
var nome = "Mario";
console.log(nome); // "Mario"
```

È come se il motore JavaScript interpretasse il codice in questo modo:

```javascript
var nome; // dichiarazione sollevata
console.log(nome); // undefined
nome = "Mario"; // assegnazione rimane qui
console.log(nome); // "Mario"
```

Questo comportamento può portare a bug difficili da individuare, ed è uno dei motivi principali per cui l'uso di var è oggi sconsigliato.

## Hoisting con let e const e la Temporal Dead Zone (TDZ)

Anche le variabili dichiarate con let e const vengono "sollevate", ma si comportano in modo molto più sicuro e prevedibile grazie alla Temporal Dead Zone (TDZ).

La TDZ è una "zona temporale" che inizia all'inizio dello scope della variabile e termina nel punto esatto in cui la variabile viene dichiarata nel codice. Durante questo intervallo, la variabile esiste ma è in uno stato inaccessibile. Qualsiasi tentativo di leggere o scrivere la variabile all'interno della TDZ provocherà un ReferenceError.

### Comportamento di let

```javascript
console.log(eta); // ❌ ReferenceError: Cannot access 'eta' before initialization
let eta = 25;
console.log(eta); // 25
```

### Comportamento di const

const segue le stesse regole di let per quanto riguarda la TDZ. La differenza principale è che una const deve essere inizializzata contestualmente alla sua dichiarazione e non può essere riassegnata.

```javascript
console.log(PI); // ❌ ReferenceError: Cannot access 'PI' before initialization
const PI = 3.14159;
console.log(PI); // 3.14159
```

## Sintesi

In sintesi, la TDZ impedisce di usare una variabile prima che sia stata dichiarata, eliminando la fonte di errori tipica dell'hoisting di var e promuovendo un codice più pulito e robusto.

## Esempio

```javascript
// VAR - solo la dichiarazione viene sollevata
console.log(nome); // undefined (non ReferenceError!)
var nome = "Mario";

// Interpretato come:
// var nome;
// console.log(nome); // undefined
// nome = "Mario";

// LET/CONST - Temporal Dead Zone (TDZ)
// console.log(eta); // ❌ ReferenceError!
let eta = 25;

// const richiede inizializzazione e ha TDZ
// console.log(PI); // ❌ ReferenceError!
const PI = 3.14159;
```

## Collegamenti

- [[variabili]] - Dichiarazione con let, const e var
- [[funzioni/funzioni]] - Le function declarations vengono sollevate
- [[esecuzione]] - Come JavaScript compila ed esegue il codice
- [[../scope/scope]] - Hoisting e scope delle variabili

## Riferimenti

- [MDN - Hoisting](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)
- [MDN - Temporal Dead Zone](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#temporal_dead_zone_tdz)
