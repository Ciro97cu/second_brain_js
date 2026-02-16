# Variabili (Variables)

**Tipo**: Nuovo Topic  
**Data**: 13 Febbraio 2026

---

## Descrizione

Un programma ha bisogno di "ricordare" dei valori che possono cambiare durante la sua esecuzione. Per fare ciò, si utilizzano le variabili: contenitori simbolici a cui viene assegnato un nome e che possono contenere dati. La funzione primaria delle variabili è gestire lo stato (state) del programma, ovvero tenere traccia dei valori mentre cambiano.

## Dichiarazione → let, const e var

In JavaScript, le variabili vengono "create" tramite una dichiarazione. Le parole chiave moderne per farlo sono let e const.

### let

Dichiara una variabile il cui valore può essere riassegnato e modificato nel tempo.

```javascript
let contatore = 0;
contatore = 1; // OK - il valore può essere riassegnato
```

### const

Dichiara una costante, ovvero una variabile il cui valore non può essere riassegnato dopo la sua prima inizializzazione. Se si tenta di farlo, il programma genererà un errore.

```javascript
const PI = 3.14159;
PI = 3; // ❌ Errore! Non si può riassegnare una costante
```

Per convenzione, i nomi delle costanti sono spesso scritti in maiuscolo (UPPER_CASE) per renderle facilmente riconoscibili.

### var

Era il modo originale per dichiarare variabili prima dell'introduzione di let e const (in ES6). Oggi il suo uso è sconsigliato a favore di let e const, che offrono un controllo migliore sulla portata (scope) delle variabili e prevengono errori comuni.

## Esempio

```javascript
// let - valore modificabile
let nome = "Alice";
nome = "Bob"; // OK

// const - valore non riassegnabile
const PI = 3.14159;
// PI = 3; // ❌ Errore!

// var - sconsigliato (ha function scope invece di block scope)
var vecchioStile = "evitare";
```

## Collegamenti

- [[../sintassi/statement]] - Le variabili vengono dichiarate con istruzioni
- [[../sintassi/expression]] - Le variabili sono usate nelle espressioni
- [[../sintassi/blocchi]] - let/const hanno block scope
- [[../programma]] - Le variabili gestiscono lo stato del programma
- [[../scope/scope]] - Ambito e visibilità delle variabili

## Riferimenti

- [MDN - Variables](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types#declarations)
- [MDN - let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
- [MDN - const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)
