# Commenti nel Codice

Il codice non viene scritto solo per il computer, ma anche e soprattutto per gli **esseri umani** (altri sviluppatori o il "te stesso" del futuro). Per questo, è fondamentale scrivere codice che sia non solo funzionante, ma anche **chiaro e comprensibile**.

I **commenti** sono porzioni di testo inserite nel codice che vengono completamente **ignorate dal motore JavaScript**. Il loro unico scopo è fornire spiegazioni a chi legge il codice.

## Principi per un Buon Uso dei Commenti

**Perché, non cosa**

Un buon commento dovrebbe spiegare **perché** una certa scelta è stata fatta, non **cosa** fa il codice. Il "cosa" dovrebbe essere reso evidente da un codice scritto in modo chiaro (es. nomi di variabili e funzioni significativi).

```javascript
// ❌ Cattivo commento - dice solo COSA
let p = d * 0.2; // moltiplica d per 0.2

// ✅ Buon commento - spiega PERCHÉ
// Sconto del 20% applicato per ordini superiori a €100
let sconto = totale * 0.2;
```

Un commento può spiegare il **come** solo se il codice è particolarmente complesso o insolito.

**Il giusto equilibrio**

- Un codice **senza commenti** è incompleto e difficile da mantenere
- Troppi commenti (es. uno per ogni riga) sono spesso sintomo di un **codice scritto male** e poco leggibile

```javascript
// ❌ Troppi commenti ovvi
let x = 10; // assegna 10 a x
let y = 20; // assegna 20 a y
let somma = x + y; // somma x e y

// ✅ Codice chiaro, commenti solo quando necessario
let larghezza = 10;
let altezza = 20;
let area = larghezza * altezza;
```

## Tipi di Commenti in JavaScript

### Commento su Riga Singola (//)

Tutto ciò che segue `//` fino alla fine della riga viene considerato un commento. Ideale per note brevi.

```javascript
// Questo è un commento su singola riga
let nome = "Mario"; // Commento a fine riga

// Commenti multipli
// possono essere messi
// su righe consecutive
```

### Commento Multiriga (/_ ... _/)

Tutto ciò che si trova tra `/*` e `*/` è un commento, anche se si estende su più righe.

```javascript
/*
 * Questo è un commento
 * che si estende su
 * più righe
 */

let risultato = calcolaComplesso(
  /* parametro1 */ valore1,
  /* parametro2 */ valore2,
);

/*
NOTA: Questo algoritmo è basato sul paper
"Efficient Sorting Algorithm" (Smith, 2020)
Complessità: O(n log n)
*/
function ordinaAvanzato(array) {
  // implementazione...
}
```

### Commenti di Documentazione (JSDoc)

Un tipo speciale di commento multiriga che inizia con `/**` e termina con `*/`. Segue una **sintassi strutturata** per descrivere funzioni, classi e variabili in modo formale.

```javascript
/**
 * Calcola l'area di un rettangolo
 *
 * @param {number} larghezza - La larghezza del rettangolo
 * @param {number} altezza - L'altezza del rettangolo
 * @returns {number} L'area del rettangolo
 */
function calcolaArea(larghezza, altezza) {
  return larghezza * altezza;
}

/**
 * Rappresenta un utente del sistema
 *
 * @typedef {Object} User
 * @property {string} nome - Nome dell'utente
 * @property {string} email - Email dell'utente
 * @property {number} eta - Età dell'utente
 */
```

I commenti JSDoc sono **estremamente utili** perché:

- Possono essere letti da strumenti automatici per **generare documentazione**
- Forniscono **suggerimenti intelligenti** negli editor di codice (IntelliSense)
- Aiutano a verificare la **correttezza dei tipi** in fase di sviluppo

## Best Practices

**Mantieni i commenti aggiornati**

```javascript
// ❌ Commento obsoleto - confonde!
// Calcola il totale con IVA al 20%
let totale = prezzoBase * 1.22; // IVA ora è 22%

// ✅ Commento aggiornato
// Calcola il totale con IVA al 22%
let totale = prezzoBase * 1.22;
```

**Codice auto-esplicativo > Commenti**

```javascript
// ❌ Commento necessario per codice poco chiaro
let d = new Date();
let y = d.getFullYear(); // ottiene anno corrente

// ✅ Codice chiaro senza bisogno di commenti
let oggi = new Date();
let annoCorrente = oggi.getFullYear();
```

**Usa commenti per spiegazioni complesse**

```javascript
// Algoritmo di Luhn per validare numeri di carta di credito
// Moltiplica per 2 ogni seconda cifra da destra,
// se il risultato > 9, sottrai 9
function validaCartaCredito(numero) {
  // implementazione complessa...
}
```

## Collegamenti

- [[statement]] - Statement possono essere commentati
- [[expression]] - Expression possono essere documentati
- [[blocchi]] - Blocchi di codice e commenti
- [[../funzioni/funzioni]] - Documentare funzioni con JSDoc
