# Nomi delle Variabili e Identificatori

**Tipo**: Nuovo Topic  
**Data**: 13 Febbraio 2026

---

## Descrizione

La scelta di un buon nome per una variabile o una funzione è cruciale per la leggibilità del codice. In JavaScript, questi nomi devono essere identificatori validi (valid identifiers) e seguire regole precise.

## Regole per un Identificatore Valido

Le regole sintattiche per un identificatore sono semplici:

### Carattere Iniziale

Deve iniziare con una lettera (da a a z, maiuscola o minuscola), un trattino basso (\_) o il simbolo del dollaro ($). Non può iniziare con un numero.

### Caratteri Successivi

Dopo il primo carattere, può contenere qualsiasi combinazione di lettere, numeri, trattini bassi o simboli del dollaro.

```javascript
// ✅ Identificatori validi
let nome;
let _privato;
let $jquery;
let camelCase;
let PascalCase;
let nome123;
let _nome_con_underscore;

// ❌ Identificatori NON validi
// let 123nome;      // Non può iniziare con un numero
// let nome-utente;  // Il trattino non è permesso
// let nome utente;  // Gli spazi non sono permessi
// let nome@utente;  // Caratteri speciali non permessi
```

Generalmente, le stesse regole si applicano ai nomi delle proprietà degli oggetti, ma con un'eccezione importante.

## Parole Riservate (Reserved Words)

Esistono delle parole riservate che hanno un significato speciale nel linguaggio e non possono essere usate come nomi di variabili. Queste includono le parole chiave come if, for, function, return, e anche null, true e false.

Tuttavia, queste parole riservate possono essere usate come nomi di proprietà all'interno di un oggetto, specialmente se si usa la notazione a parentesi quadre.

```javascript
// ❌ Non si possono usare parole riservate come variabili
// let if = 5;
// let for = 10;
// let function = "test";
// let return = true;
// let null = "vuoto";

// ✅ Ma si possono usare come proprietà degli oggetti
let oggetto = {
  if: "condizione",
  for: "ciclo",
  function: "funzione",
  return: "ritorno",
  class: "classe",
};

console.log(oggetto.if); // "condizione"
console.log(oggetto["for"]); // "ciclo"

// Parole riservate comuni da evitare come nomi di variabili:
// break, case, catch, class, const, continue, debugger, default,
// delete, do, else, export, extends, finally, for, function,
// if, import, in, instanceof, let, new, return, super, switch,
// this, throw, try, typeof, var, void, while, with, yield
```

## Convenzioni e Buone Pratiche

Oltre alle regole sintattiche, la comunità JavaScript segue delle convenzioni per scrivere codice più pulito e comprensibile:

### Nomi Descrittivi

Scegliere nomi che spieghino chiaramente lo scopo della variabile (es. prezzoUnitario invece di p). Evitare abbreviazioni ambigue.

### Notazione camelCase

È la convenzione standard in JavaScript. Si inizia con una lettera minuscola e si usa la maiuscola per l'inizio di ogni parola successiva, senza spazi (es. nomeUtente, calcolaPrezzoFinale).

### Plurali per le Collezioni

Usare un nome plurale per gli array o altre collezioni di dati, per indicare che contengono più elementi (es. utenti, prodotti).

## Esempio

```javascript
// ✅ Nomi descrittivi con camelCase
let nomeUtente = "Mario";
let prezzoUnitario = 10;

function calcolaPrezzoFinale(prezzo, sconto) {
  return prezzo - (prezzo * sconto) / 100;
}

// ✅ UPPER_CASE per costanti
const MAX_TENTATIVI = 3;
const API_BASE_URL = "https://api.example.com";

// ✅ Plurali per collezioni
let utente = { nome: "Mario" };
let utenti = [{ nome: "Mario" }, { nome: "Luigi" }];

// ✅ Prefissi per booleani
let isAttivo = true;
let hasPermessi = false;

console.log("Totale:", carrelloAcquisti.calcolaTotaleCarrello()); // 1057
```

## Collegamenti

- [[variabili]] - I nomi delle variabili devono essere identificatori validi
- [[programma]] - Un codice leggibile usa nomi descrittivi

## Riferimenti

- [MDN - Grammar and types](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types#variables)
- [MDN - Lexical grammar](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar)
