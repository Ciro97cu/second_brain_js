# Appunti JavaScript - Completi

_Ultimo aggiornamento: 13 Febbraio 2026_

---

## 1. Introduzione

### 1.1 Che cos'è Javascript

**Tipo**: Nuovo Topic

JavaScript (JS) è un linguaggio di programmazione versatile, comunemente usato per creare interattività nelle pagine web. Permette di manipolare dinamicamente i contenuti, animare elementi, gestire eventi (come il click di un pulsante) e comunicare con un server per aggiornare parti della pagina senza doverla ricaricare completamente.

Sebbene sia spesso descritto come un linguaggio interpretato (interpreted), la sua esecuzione è più complessa. I moderni motori JavaScript (JavaScript engines) — come V8 (in Chrome) o SpiderMonkey (in Firefox) — non si limitano a interpretare il codice riga per riga. Eseguono invece una compilazione Just-In-Time (JIT), traducendo il codice sorgente (source code) in codice macchina ottimizzato poco prima dell'esecuzione, garantendo così prestazioni molto più elevate.

JavaScript è un linguaggio a tipizzazione debole e dinamica (weakly and dynamically typed). Questo significa che non è necessario dichiarare il tipo di dato di una variabile (es. numero, testo, ecc.) quando la si crea. Una stessa variabile può contenere tipi di dati diversi nel corso del programma. Il linguaggio gestisce inoltre conversioni di tipo automatiche, un processo chiamato coercizione di tipo (type coercion). Questa flessibilità può accelerare lo sviluppo, ma richiede attenzione per evitare errori e comportamenti inattesi.

```javascript
/*
 * Esempi di interattività e tipizzazione dinamica in JavaScript
 */

// Manipolazione dinamica del contenuto
document.getElementById("titolo").textContent = "Benvenuto!";

// Gestione di eventi (click di un pulsante)
document.getElementById("mioBottone").addEventListener("click", function () {
  alert("Hai cliccato il pulsante!");
});

// Animazione di elementi
let box = document.querySelector(".box");
box.style.transform = "translateX(100px)";

// Tipizzazione dinamica - la stessa variabile può contenere tipi diversi
let valore = 42; // numero
console.log(typeof valore); // "number"

valore = "Ciao"; // ora è una stringa
console.log(typeof valore); // "string"

valore = true; // ora è un booleano
console.log(typeof valore); // "boolean"

// Type coercion (conversione automatica di tipo)
let risultato = "5" + 3; // "53" (il numero viene convertito in stringa)
let somma = "5" - 3; // 2 (la stringa viene convertita in numero)
let confronto = "10" == 10; // true (i valori vengono confrontati dopo conversione)

/*
 * Comunicazione con un server (AJAX)
 * Permette di aggiornare parti della pagina senza ricaricarla
 */
fetch("https://api.example.com/dati")
  .then((response) => response.json())
  .then((dati) => {
    console.log("Dati ricevuti:", dati);
    // Aggiorna la pagina con i nuovi dati
  });
```

---

### 1.2 ECMAScript

**Tipo**: Nuovo Topic

ECMAScript è una specifica, uno standard tecnico, che definisce le regole, le funzionalità e il comportamento che un linguaggio di scripting deve avere. Non è un linguaggio di programmazione, ma la "ricetta" su cui si basano diversi linguaggi.

JavaScript è l'implementazione più famosa e diffusa dello standard ECMAScript.

La relazione tra i due si può riassumere così:

- **Nascita e Standardizzazione** → JavaScript fu creato da Netscape. Per evitare che ogni browser sviluppasse una propria versione incompatibile del linguaggio, fu necessario creare uno standard. Nel 1997, JavaScript fu sottomesso a Ecma International, un'organizzazione di standardizzazione, che ne formalizzò le specifiche con il nome di ECMAScript.

- **Evoluzione Continua** → Lo standard ECMAScript si evolve costantemente. Nuove versioni vengono rilasciate (annualmente dal 2015) per aggiungere funzionalità e migliorare il linguaggio. Una delle versioni più importanti è stata ECMAScript 2015 (ES6), che ha introdotto cambiamenti fondamentali come le classi (classes), le funzioni freccia (arrow functions) e i moduli (modules).

- **Implementazioni Diverse** → Sebbene JavaScript nei browser sia l'implementazione (implementation) principale, non è l'unica. Anche ambienti come Node.js (per lo sviluppo server-side) e Deno implementano lo standard ECMAScript, permettendo di usare una sintassi e funzionalità coerenti in contesti diversi dal web.

In sintesi, ECMAScript definisce come il linguaggio "dovrebbe" funzionare, mentre JavaScript è il linguaggio che gli sviluppatori usano concretamente, il quale "implementa" quelle definizioni.

```javascript
/*
 * Esempi di evoluzione ECMAScript: confronto ES5 vs ES6
 */

// ===== VARIABILI =====
// ES5 - solo var
var nome = "Mario";

// ES6 - let e const
let eta = 25;
const PI = 3.14159;

// ===== FUNZIONI =====
// ES5 - funzione tradizionale
function somma(a, b) {
  return a + b;
}

// ES6 - arrow function
const sommaES6 = (a, b) => a + b;

// ===== CLASSI =====
// ES5 - constructor function
function Persona(nome, eta) {
  this.nome = nome;
  this.eta = eta;
}
Persona.prototype.saluta = function () {
  return "Ciao, sono " + this.nome;
};

// ES6 - class syntax
class PersonaES6 {
  constructor(nome, eta) {
    this.nome = nome;
    this.eta = eta;
  }

  saluta() {
    return `Ciao, sono ${this.nome}`;
  }
}

// ===== TEMPLATE LITERALS =====
// ES5 - concatenazione stringhe
var messaggio = "Ciao " + nome + ", hai " + eta + " anni";

// ES6 - template literals
const messaggioES6 = `Ciao ${nome}, hai ${eta} anni`;

// ===== MODULI =====
// ES6 - import/export
// In un file math.js:
// export function quadrato(x) { return x * x; }

// In un altro file:
// import { quadrato } from './math.js';

// ===== DESTRUCTURING =====
// ES6 - destrutturazione
const utente = { nome: "Anna", eta: 30, citta: "Roma" };
const { nome: nomeUtente, citta } = utente;

const numeri = [1, 2, 3, 4, 5];
const [primo, secondo, ...resto] = numeri;

/*
 * Implementazioni diverse dello standard ECMAScript
 */

// Browser (JavaScript)
console.log("Esecuzione nel browser");

// Node.js (implementazione ECMAScript lato server)
// const fs = require('fs'); // moduli Node.js

// Deno (altra implementazione server-side moderna)
// import { serve } from "https://deno.land/std/http/server.ts";
```

---

### 1.3 Dove Inserire il Codice JavaScript in HTML

**Tipo**: Nuovo Topic

Per far interagire JavaScript con una pagina web, è necessario includere il codice nel documento HTML. Questo si fa tramite il tag `<script>`, che può essere posizionato in punti diversi del file. La posizione e gli attributi usati (async, defer) hanno un impatto significativo sul caricamento della pagina e sulle performance.

Il modo più comune è collegare un file .js esterno usando l'attributo src.

```html
<script src="script.js"></script>
```

#### Nel `<head>` (Senza Attributi)

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Esempio</title>
    <script src="script.js"></script>
  </head>
  <body>
    <h1>Contenuto della pagina</h1>
  </body>
</html>
```

- **Comportamento** → Il browser interrompe l'analisi (parsing) del file HTML, scarica ed esegue immediatamente lo script. Solo dopo riprende a costruire la pagina.

- **Impatto** → È un metodo bloccante (blocking). Rallenta la visualizzazione iniziale della pagina, perché l'utente non vedrà alcun contenuto finché lo script non avrà finito. Oggi è una pratica generalmente sconsigliata.

#### Alla Fine del `<body>`

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Esempio</title>
  </head>
  <body>
    <h1>Contenuto della pagina</h1>
    <p>Tutto il contenuto HTML viene caricato prima dello script</p>

    <script src="script.js"></script>
  </body>
</html>
```

- **Comportamento** → Il browser analizza e visualizza tutto il contenuto HTML della pagina. Solo alla fine, scarica ed esegue lo script.

- **Impatto** → La pagina appare velocemente all'utente. Quando lo script viene eseguito, ha già accesso a tutti gli elementi del DOM. È stata la tecnica più raccomandata per anni.

#### Nel `<head>` con Attributo defer

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Esempio</title>
    <script src="script.js" defer></script>
    <script src="altro-script.js" defer></script>
  </head>
  <body>
    <h1>Contenuto della pagina</h1>
  </body>
</html>
```

- **Comportamento** → Il browser scarica lo script in parallelo, senza interrompere l'analisi dell'HTML. Lo script viene eseguito solo quando l'intero documento HTML è stato analizzato, ma prima che venga lanciato l'evento DOMContentLoaded. Se ci sono più script con defer, vengono eseguiti nell'ordine in cui appaiono nel documento.

- **Impatto** → Non blocca la visualizzazione della pagina e garantisce l'ordine di esecuzione. È spesso la scelta migliore e più moderna.

#### Nel `<head>` con Attributo async

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Esempio</title>
    <script src="analytics.js" async></script>
  </head>
  <body>
    <h1>Contenuto della pagina</h1>
  </body>
</html>
```

- **Comportamento** → Il browser scarica lo script in parallelo, ma lo esegue non appena il download è completato, interrompendo momentaneamente l'analisi dell'HTML se non è ancora finita. L'ordine di esecuzione non è garantito se ci sono più script async.

- **Impatto** → Utile per script indipendenti che non devono interagire con il DOM e non dipendono da altri script (es. script di analytics, pubblicità). Non è adatto per script che manipolano la pagina o che hanno dipendenze.

```javascript
/*
 * Esempio pratico: script.js
 * Questo script manipola il DOM
 */

// Con defer o posizionamento a fine body, il DOM è già pronto
const titolo = document.querySelector("h1");
titolo.textContent = "JavaScript ha modificato questo titolo!";

// Aggiunge un listener per un evento
const bottone = document.getElementById("mioBottone");
bottone.addEventListener("click", function () {
  alert("Bottone cliccato!");
});

/*
 * Confronto visivo del caricamento
 */

// SENZA defer/async (bloccante):
// 1. Browser legge <script> nel <head>
// 2. ⏸️ BLOCCO - scarica script.js
// 3. ⏸️ BLOCCO - esegue script.js
// 4. ✅ Riprende parsing HTML
// 5. Mostra contenuto

// CON defer (raccomandato):
// 1. Browser legge <script defer> nel <head>
// 2. ⚡ Scarica script.js in parallelo
// 3. ✅ Continua parsing HTML
// 4. Mostra contenuto
// 5. ✅ Esegue script.js quando HTML è pronto

// CON async (per script indipendenti):
// 1. Browser legge <script async> nel <head>
// 2. ⚡ Scarica script.js in parallelo
// 3. ⚡ Esegue appena scaricato (può bloccare)
// 4. Continua parsing HTML

// A FINE <body> (tecnica classica):
// 1. ✅ Parsing completo di tutto l'HTML
// 2. Mostra contenuto
// 3. Scarica ed esegue script.js
```

---

### 1.4 Esecuzione

**Tipo**: Nuovo Topic

Per poter eseguire (to execute o run) le istruzioni, un programma deve essere tradotto in un formato che il computer possa comprendere. Questo compito è svolto da programmi speciali chiamati interpreti (interpreters) o compilatori (compilers).

L'**interpretazione** (interpreting) consiste nel tradurre ed eseguire il codice sorgente (source code) riga per riga, ogni volta che il programma viene avviato.

La **compilazione** (compiling) traduce l'intero programma in anticipo. Quando il programma viene eseguito, è la versione già compilata (in linguaggio macchina) ad essere avviata.

Comunemente si dice che JavaScript sia un linguaggio interpretato, ma questa è un'imprecisione. Il motore JavaScript (JavaScript engine) in realtà compila (compiles) il codice "al volo" (on the fly) e poi esegue immediatamente il risultato. Questo processo è noto come **compilazione JIT (Just-In-Time)**.

```javascript
/*
 * Esempio di codice JavaScript
 * Il JavaScript engine esegue questi passaggi:
 */

// 1. PARSING - Il codice viene letto e analizzato
function calcola(a, b) {
  return a + b;
}

// 2. COMPILAZIONE JIT - Il codice viene compilato in linguaggio macchina
let risultato = calcola(5, 3);

// 3. ESECUZIONE - Il codice compilato viene eseguito
console.log(risultato); // Output: 8

/*
 * Tutto questo avviene "al volo" quando si esegue il programma.
 * Il JavaScript engine (come V8 in Chrome/Node.js) ottimizza
 * il codice durante l'esecuzione per migliorare le performance.
 */

// Esempio di ottimizzazione JIT
function sommaRipetuta(n) {
  let totale = 0;
  for (let i = 0; i < n; i++) {
    totale += i;
  }
  return totale;
}

/*
 * Se questa funzione viene chiamata molte volte,
 * il JIT compiler la ottimizza per renderla più veloce
 */
console.log(sommaRipetuta(1000));
console.log(sommaRipetuta(2000));
console.log(sommaRipetuta(3000));
```

---

## 2. Fondamenti

### 2.1 Programma

**Tipo**: Nuovo Topic

Un programma, o codice, è un insieme di istruzioni che dicono al computer cosa fare.

Queste istruzioni sono scritte in un file di testo seguendo le regole di un linguaggio di programmazione. L'insieme di queste regole (formato, combinazioni valide, ecc.) è definito sintassi, che può essere paragonata alla grammatica e all'ortografia di una lingua umana.

```javascript
/*
 * Esempio di un semplice programma JavaScript
 * Questo programma calcola l'area di un rettangolo
 */
let larghezza = 10;
let altezza = 5;
let area = larghezza * altezza;

console.log("L'area del rettangolo è: " + area);
```

---

### 2.2 Commenti nel Codice (Code Comments)

**Tipo**: Nuovo Topic

Il codice non viene scritto solo per il computer, ma anche e soprattutto per gli **esseri umani** (altri sviluppatori o il "te stesso" del futuro). Per questo, è fondamentale scrivere codice che sia non solo funzionante, ma anche **chiaro e comprensibile**.

I **commenti** sono porzioni di testo inserite nel codice che vengono completamente **ignorate dal motore JavaScript**. Il loro unico scopo è fornire spiegazioni a chi legge il codice.

#### Principi per un Buon Uso dei Commenti

**Perché, non cosa**

Un buon commento dovrebbe spiegare **perché** una certa scelta è stata fatta, non **cosa** fa il codice. Il "cosa" dovrebbe essere reso evidente da un codice scritto in modo chiaro (nomi di variabili e funzioni significativi).

```javascript
/*
 * Cattivo vs Buon Commento
 */

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
/*
 * Troppi commenti vs codice chiaro
 */

// ❌ Troppi commenti ovvi
let x = 10; // assegna 10 a x
let y = 20; // assegna 20 a y
let somma = x + y; // somma x e y

// ✅ Codice chiaro, commenti solo quando necessario
let larghezza = 10;
let altezza = 20;
let area = larghezza * altezza;
```

#### Tipi di Commenti in JavaScript

**Commento su Riga Singola (//)** - Tutto ciò che segue `//` fino alla fine della riga viene considerato un commento. Ideale per note brevi.

```javascript
/*
 * Commenti su singola riga
 */

// Questo è un commento su singola riga
let nome = "Mario"; // Commento a fine riga

// Commenti multipli
// possono essere messi
// su righe consecutive
```

**Commento Multiriga (/_ ... _/)** - Tutto ciò che si trova tra `/*` e `*/` è un commento, anche se si estende su più righe.

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

**Commenti di Documentazione (JSDoc)** - Un tipo speciale di commento multiriga che inizia con `/**` e termina con `*/`. Segue una **sintassi strutturata** per descrivere funzioni, classi e variabili in modo formale.

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

#### Best Practices

**Mantieni i commenti aggiornati**

```javascript
/*
 * Importanza di commenti aggiornati
 */

// ❌ Commento obsoleto - confonde!
// Calcola il totale con IVA al 20%
let totale = prezzoBase * 1.22; // IVA ora è 22%

// ✅ Commento aggiornato
// Calcola il totale con IVA al 22%
let totale = prezzoBase * 1.22;
```

**Codice auto-esplicativo > Commenti**

```javascript
/*
 * Preferire codice chiaro ai commenti
 */

// ❌ Commento necessario per codice poco chiaro
let d = new Date();
let y = d.getFullYear(); // ottiene anno corrente

// ✅ Codice chiaro senza bisogno di commenti
let oggi = new Date();
let annoCorrente = oggi.getFullYear();
```

**Usa commenti per spiegazioni complesse**

```javascript
/*
 * Commenti utili per logica complessa
 */

// Algoritmo di Luhn per validare numeri di carta di credito
// Moltiplica per 2 ogni seconda cifra da destra,
// se il risultato > 9, sottrai 9
function validaCartaCredito(numero) {
  // implementazione complessa...
}
```

**Approfondisci**:

- [[01-fondamenti/sintassi/commenti]] - Commenti nel codice

---

### 2.3 Statement (Istruzione)

**Tipo**: Nuovo Topic

Un'istruzione è un comando che esegue un compito specifico. Un programma è composto da una serie di istruzioni.

```javascript
let a = 2 * b;
```

Questa istruzione è composta da diverse parti:

- **Variabili (a e b)** → Sono "contenitori" simbolici che memorizzano valori su cui il programma può operare. Funzionano come segnaposto per i valori stessi.

- **Valore Letterale (2)** → È un valore scritto direttamente nel codice, che non è stato memorizzato in una variabile.

- **Operatori (= e \*)** → Sono simboli che eseguono azioni. L'\* esegue una moltiplicazione, mentre l'= assegna il risultato dell'operazione alla variabile a sinistra.

La maggior parte delle istruzioni in JavaScript termina con un punto e virgola (;).

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

---

### 2.4 Expression (Espressione)

**Tipo**: Nuovo Topic

Le istruzioni sono composte da una o più espressioni. Un'espressione è un qualsiasi pezzo di codice che produce un valore, come un riferimento a una variabile o una combinazione di valori e operatori.

Analizzando l'istruzione `a = b * 2;`, si possono identificare quattro espressioni:

- **2** → Un'espressione letterale, il cui valore è semplicemente 2.

- **b** → Un'espressione di variabile, che si risolve nel valore contenuto in b.

- **b \* 2** → Un'espressione aritmetica, che produce il risultato della moltiplicazione.

- **a = b \* 2** → Un'espressione di assegnamento, che assegna il risultato di b \* 2 alla variabile a.

Un'espressione che sta da sola può formare un'intera istruzione, chiamata istruzione di espressione. Sebbene un'istruzione come `b * 2;` sia valida, è poco utile perché il risultato non viene utilizzato. Un esempio molto più comune di istruzione di espressione è una chiamata a una funzione, come `alert(a);`.

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

### 2.5 Blocchi di Codice (Code Blocks)

**Tipo**: Nuovo Topic

Un blocco (block) è un gruppo di una o più istruzioni racchiuse tra parentesi graffe `{ ... }`. La sua funzione è quella di raggruppare istruzioni che appartengono logicamente insieme, creando un'unità di codice che può essere trattata come un singolo elemento.

```javascript
// Blocco di codice autonomo (raro, ma valido)
{
  let messaggio = "Questo è un blocco autonomo";
  console.log(messaggio);
}
```

Sebbene un blocco di codice possa esistere da solo (come nell'esempio sopra), questa forma è rara nella pratica. Generalmente, i blocchi sono associati a **strutture di controllo**, come le istruzioni condizionali (`if`, `else`) o i cicli (`for`, `while`, `do-while`), per definire quali istruzioni eseguire quando una certa condizione si verifica.

A differenza delle singole istruzioni, un blocco di codice **non richiede** un punto e virgola (`;`) alla fine della parentesi graffa di chiusura.

```javascript
/*
 * Blocchi di codice con strutture di controllo
 */

// Blocco con if
let temperatura = 30;

if (temperatura > 25) {
  // Questo è un blocco
  console.log("Fa caldo");
  console.log("Prendi dell'acqua");
}

// Blocco con if-else
let eta = 20;

if (eta >= 18) {
  console.log("Maggiorenne");
  console.log("Puoi votare");
} else {
  console.log("Minorenne");
  console.log("Non puoi votare");
}

// Blocco con ciclo for
for (let i = 0; i < 3; i++) {
  // Questo blocco viene eseguito 3 volte
  console.log("Iterazione numero:", i);
  let quadrato = i * i;
  console.log("Quadrato:", quadrato);
}

// Blocco con ciclo while
let contatore = 0;
while (contatore < 3) {
  console.log("Contatore:", contatore);
  contatore++;
}

/*
 * Blocchi annidati (nested blocks)
 */
let numero = 15;

if (numero > 0) {
  console.log("Numero positivo");

  if (numero > 10) {
    // Blocco annidato dentro un altro blocco
    console.log("Numero maggiore di 10");

    if (numero > 20) {
      console.log("Numero maggiore di 20");
    } else {
      console.log("Numero tra 10 e 20");
    }
  }
}

/*
 * Blocchi e scope (portata delle variabili)
 */

// let e const hanno "block scope"
{
  let x = 10;
  const y = 20;
  console.log(x, y); // 10, 20
}
// console.log(x); // ❌ ReferenceError - x non esiste fuori dal blocco
// console.log(y); // ❌ ReferenceError - y non esiste fuori dal blocco

// var ha "function scope" (non block scope)
{
  var z = 30;
}
console.log(z); // ✅ 30 - var è accessibile fuori dal blocco

/*
 * Blocchi senza strutture di controllo (rari ma utili)
 */

// Utile per limitare lo scope di variabili temporanee
{
  let tempData = fetchData(); // funzione ipotetica
  let processed = processData(tempData); // funzione ipotetica
  saveResult(processed); // funzione ipotetica
  // tempData e processed non sono più accessibili fuori da qui
}

// Isolare calcoli temporanei
let totale = 0;
{
  let prezzo = 19.99;
  let quantita = 3;
  let subtotale = prezzo * quantita;
  let sconto = subtotale * 0.1;
  totale = subtotale - sconto;
}
console.log(totale); // 53.973
// prezzo, quantita, subtotale, sconto non sono accessibili qui

/*
 * Punto e virgola con blocchi
 */

// ❌ NON serve il punto e virgola dopo un blocco
if (true) {
  console.log("Corretto");
} // ← Niente punto e virgola

// ✅ Ma serve dopo le istruzioni normali
let a = 5; // ← Punto e virgola necessario
console.log(a); // ← Punto e virgola necessario

// Eccezione: espressioni di funzione o oggetti
let funzione = function () {
  console.log("Funzione");
}; // ← Punto e virgola perché è un assegnamento

let oggetto = {
  proprieta: "valore",
}; // ← Punto e virgola perché è un assegnamento
```

---

### 2.6 Istruzioni Condizionali (Conditionals)

**Tipo**: Nuovo Topic

Le **istruzioni condizionali** permettono a un programma di prendere decisioni, eseguendo blocchi di codice diversi in base al verificarsi o meno di una determinata condizione. Sono fondamentali per creare programmi dinamici che si adattano a situazioni diverse.

#### L'Istruzione if

L'istruzione `if` è la struttura condizionale più comune. La sua logica è: **"se una certa condizione è vera, allora esegui questo blocco di codice"**.

La condizione da valutare viene inserita tra parentesi `()` e deve produrre un risultato booleano (`true` o `false`).

```javascript
/*
 * Sintassi base if
 */

if (condizione) {
  // codice eseguito solo se condizione è true
}

// Esempio pratico
let eta = 18;

if (eta >= 18) {
  console.log("Sei maggiorenne");
}

let temperatura = 35;

if (temperatura > 30) {
  console.log("Fa molto caldo!");
}
```

Se la condizione è `false`, il blocco di codice viene **saltato** e l'esecuzione continua dopo la chiusura `}`.

```javascript
/*
 * Condizione falsa - blocco saltato
 */

let punteggio = 45;

if (punteggio >= 60) {
  console.log("Hai superato l'esame"); // NON viene eseguito
}

console.log("Fine programma"); // Viene sempre eseguito
```

#### else: L'Alternativa

Spesso si vuole definire un comportamento alternativo da eseguire quando la condizione dell'`if` risulta falsa. Per questo si usa la clausola `else`.

```javascript
/*
 * if...else
 */

let eta = 15;

if (eta >= 18) {
  console.log("Sei maggiorenne");
} else {
  console.log("Sei minorenne");
}

// Output: "Sei minorenne"
```

L'`else` fornisce un **percorso alternativo**: esattamente uno dei due blocchi viene eseguito, mai entrambi.

```javascript
/*
 * Percorsi alternativi
 */

let oraCorrente = 14;

if (oraCorrente < 12) {
  console.log("Buongiorno");
} else {
  console.log("Buonasera");
}

// Output: "Buonasera"
```

#### else if: Condizioni Multiple

Per gestire una serie di condizioni alternative in sequenza, si può usare `else if`. Il programma valuta le condizioni **una dopo l'altra** e si ferma non appena ne trova una vera, eseguendo solo il blocco di codice corrispondente.

```javascript
/*
 * Catena if...else if...else
 */

let voto = 85;

if (voto >= 90) {
  console.log("Eccellente");
} else if (voto >= 75) {
  console.log("Buono");
} else if (voto >= 60) {
  console.log("Sufficiente");
} else {
  console.log("Insufficiente");
}

// Output: "Buono"
```

**Importante**: Solo il **primo blocco** la cui condizione è `true` viene eseguito, anche se più condizioni potrebbero essere vere.

```javascript
/*
 * Solo il primo blocco true viene eseguito
 */

let numero = 100;

if (numero > 50) {
  console.log("Maggiore di 50"); // ✅ Eseguito
} else if (numero > 75) {
  console.log("Maggiore di 75"); // ❌ Saltato (anche se true!)
} else if (numero > 90) {
  console.log("Maggiore di 90"); // ❌ Saltato
}

// Output: Solo "Maggiore di 50"
```

Se **nessuna condizione** è vera, viene eseguito il blocco `else` finale, se presente.

```javascript
/*
 * Nessuna condizione vera - else eseguito
 */

let giorno = "sabato";

if (giorno === "lunedì") {
  console.log("Inizio settimana");
} else if (giorno === "venerdì") {
  console.log("Fine settimana");
} else {
  console.log("Altro giorno"); // ✅ Eseguito
}

// Output: "Altro giorno"
```

#### Condizioni Complesse

Le condizioni possono essere combinate usando **operatori logici**.

```javascript
/*
 * Operatori logici nelle condizioni
 */

let eta = 25;
let haPatente = true;

// AND logico (&&) - entrambe devono essere true
if (eta >= 18 && haPatente) {
  console.log("Puoi guidare");
}

// OR logico (||) - almeno una deve essere true
let isWeekend = true;
let isVacanza = false;

if (isWeekend || isVacanza) {
  console.log("Giorno di riposo");
}

// NOT logico (!) - inverte il valore
let piove = false;

if (!piove) {
  console.log("Bel tempo!");
}
```

#### Best Practices

**Sempre usare le parentesi graffe**

```javascript
// ❌ Evitare (fragile, errori facili)
if (eta >= 18) console.log("Maggiorenne");

// ✅ Preferire (chiaro e sicuro)
if (eta >= 18) {
  console.log("Maggiorenne");
}
```

**Condizioni chiare ed esplicite**

```javascript
// ❌ Condizione implicita (confusa)
let utente = "Mario";
if (utente) {
  // cosa stiamo verificando?
}

// ✅ Condizione esplicita (chiara)
if (utente !== null && utente !== "") {
  console.log("Utente valido");
}
```

**Ordinare condizioni dalla più specifica alla più generica**

```javascript
// ✅ Ordine corretto
if (voto >= 90) {
  console.log("Eccellente");
} else if (voto >= 75) {
  console.log("Buono");
} else if (voto >= 60) {
  console.log("Sufficiente");
} else {
  console.log("Insufficiente");
}

// ❌ Ordine errato (la prima cattura tutto!)
if (voto >= 60) {
  console.log("Sufficiente"); // Anche voti alti finiscono qui!
} else if (voto >= 75) {
  // Mai eseguito
} else if (voto >= 90) {
  // Mai eseguito
}
```

**Approfondisci**:

- [[01-fondamenti/sintassi/condizionali]] - Istruzioni condizionali (if, else, else if)

---

### 2.7 Switch

**Tipo**: Nuovo Topic

Quando si ha la necessità di confrontare una singola variabile o espressione con una serie di valori specifici, una lunga catena di `if...else if` può diventare verbosa. In questi scenari, l'istruzione **switch** offre un'alternativa più pulita e strutturata.

#### Sintassi Base

La struttura dello switch si basa su:

- **`case`** → Un'etichetta che rappresenta un possibile valore per l'espressione
- **`break`** → Un'istruzione che interrompe l'esecuzione dello switch (fondamentale!)
- **`default`** → Un caso opzionale eseguito se nessun `case` corrisponde

```javascript
/*
 * Struttura dello switch
 */

switch (espressione) {
  case valore1:
    // codice eseguito se espressione === valore1
    break;
  case valore2:
    // codice eseguito se espressione === valore2
    break;
  default:
  // codice eseguito se nessun case corrisponde
}

// Esempio pratico
let giorno = "Lunedì";

switch (giorno) {
  case "Lunedì":
    console.log("Inizio settimana");
    break;
  case "Mercoledì":
    console.log("Metà settimana");
    break;
  case "Venerdì":
    console.log("Quasi weekend!");
    break;
  case "Sabato":
  case "Domenica":
    console.log("È il weekend!");
    break;
  default:
    console.log("Un giorno normale");
}
```

#### Confronto con if...else if

**Usando if...else if**:

```javascript
/*
 * Approccio con if...else if
 */

let colore = "rosso";

if (colore === "rosso") {
  console.log("Stop");
} else if (colore === "giallo") {
  console.log("Rallenta");
} else if (colore === "verde") {
  console.log("Vai");
} else {
  console.log("Colore non valido");
}
```

**Usando switch** (più pulito per confronti di uguaglianza):

```javascript
/*
 * Approccio con switch
 */

let colore = "rosso";

switch (colore) {
  case "rosso":
    console.log("Stop");
    break;
  case "giallo":
    console.log("Rallenta");
    break;
  case "verde":
    console.log("Vai");
    break;
  default:
    console.log("Colore non valido");
}
```

#### L'Importanza del break

Il **`break`** è fondamentale per evitare il **fall through** (caduta) nel caso successivo.

```javascript
/*
 * Senza break - Fall Through pericoloso
 */

let numero = 1;

switch (numero) {
  case 1:
    console.log("Uno"); // ✅ Eseguito
  // MANCA break!
  case 2:
    console.log("Due"); // ⚠️ Eseguito anche se numero !== 2
    break;
}

// Output:
// "Uno"
// "Due"
```

**Con break** (comportamento corretto):

```javascript
/*
 * Con break - Comportamento normale
 */

let numero = 1;

switch (numero) {
  case 1:
    console.log("Uno"); // ✅ Eseguito
    break; // ✅ Esce dallo switch
  case 2:
    console.log("Due"); // ❌ NON eseguito
    break;
}

// Output: "Uno"
```

#### Raggruppare i case

Una caratteristica utile dello switch è la possibilità di **raggruppare più case** per eseguire lo stesso blocco di codice, omettendo deliberatamente il `break`.

```javascript
/*
 * Raggruppamento case - Fall Through Intenzionale
 */

let giorno = "Sabato";

switch (giorno) {
  case "Lunedì":
  case "Martedì":
  case "Mercoledì":
  case "Giovedì":
  case "Venerdì":
    console.log("Giorno lavorativo");
    break;
  case "Sabato":
  case "Domenica":
    console.log("È il weekend!");
    break;
  default:
    console.log("Giorno non valido");
}

// Output: "È il weekend!"
```

In questo esempio, se `giorno` è `"Sabato"`, l'esecuzione "cade" fino al blocco di codice del caso `"Domenica"` ed esegue il codice condiviso.

#### Confronto Strict (===)

**Importante**: Lo switch usa il confronto **strict** (`===`), non il confronto loose (`==`).

```javascript
/*
 * Switch usa ===
 */

let numero = "2"; // stringa

switch (numero) {
  case 2: // number
    console.log("Due (number)"); // ❌ NON eseguito
    break;
  case "2": // string
    console.log("Due (string)"); // ✅ Eseguito
    break;
}
```

#### Quando Usare switch vs if...else

**Usa switch quando**:

- Confronti una **singola variabile/espressione** con molti valori specifici
- I confronti sono di **uguaglianza** (`===`)
- Hai **3 o più casi** da gestire
- Vuoi codice più **leggibile e strutturato**

**Usa if...else quando**:

- Hai **condizioni complesse** (range, confronti multipli)
- Usi **operatori diversi** (`>`, `<`, `>=`, `&&`, `||`)
- Hai **pochi casi** (1-2)

```javascript
// ✅ Buon caso per if...else (condizioni complesse)
if (eta >= 18 && haPatente) {
  console.log("Puoi guidare");
} else if (eta >= 16) {
  console.log("Puoi guidare con supervisione");
} else {
  console.log("Non puoi guidare");
}

// switch non può gestire condizioni complesse come questa
```

#### Best Practices

**Sempre usare break**:

```javascript
// ✅ Corretto - break in ogni case
switch (valore) {
  case 1:
    console.log("Uno");
    break; // ✅
  case 2:
    console.log("Due");
    break; // ✅
}
```

**Includere sempre default**:

```javascript
// ✅ Con default (robusto)
switch (azione) {
  case "salva":
    salva();
    break;
  case "elimina":
    elimina();
    break;
  default:
    console.log("Azione non riconosciuta");
}
```

**Documentare fall through intenzionale**:

```javascript
// ✅ Commentare fall through intenzionali
switch (livello) {
  case "admin":
    abilitaGestioneUtenti();
  // fall through - admin ha anche permessi editor
  case "editor":
    abilitaModificaContenuti();
    break;
}
```

**Approfondisci**:

- [[01-fondamenti/sintassi/switch]] - Switch statement

### 2.8 Cicli (Loops)

**Tipo**: Nuovo Topic

I **cicli** (loops) sono strutture fondamentali in programmazione che permettono di eseguire un blocco di codice ripetutamente, finché una determinata condizione rimane vera. Ogni esecuzione del blocco di codice all'interno di un ciclo è chiamata **iterazione** (iteration). I cicli sono essenziali per automatizzare compiti ripetitivi.

#### Il Ciclo while

Il ciclo `while` è una delle forme più semplici di ciclo. La sua logica è: **"mentre questa condizione è vera, continua a eseguire il blocco di codice"**. La condizione viene controllata **prima** di ogni iterazione. Se la condizione risulta falsa fin dall'inizio, il blocco di codice non verrà mai eseguito.

```javascript
/*
 * Sintassi while
 */

while (condizione) {
  // codice eseguito finché condizione è true
}

// Esempio: contare da 1 a 5
let i = 1;

while (i <= 5) {
  console.log(i);
  i++; // Fondamentale per evitare cicli infiniti!
}

// Output:
// 1
// 2
// 3
// 4
// 5
```

**⚠️ Attenzione**: Il ciclo `while` può creare **cicli infiniti** se la condizione non diventa mai falsa.

```javascript
/*
 * Ciclo infinito - EVITARE!
 */

let x = 1;

while (x <= 5) {
  console.log(x);
  // MANCA x++! Il ciclo non terminerà mai
}
```

#### Il Ciclo do...while

Il ciclo `do...while` è molto simile al `while`, ma con una differenza cruciale: la condizione viene controllata **dopo** ogni iterazione. Questo garantisce che il blocco di codice venga eseguito **almeno una volta**, anche se la condizione iniziale è falsa.

```javascript
/*
 * Sintassi do...while
 */

do {
  // codice eseguito almeno una volta
} while (condizione);

// Esempio: eseguito almeno una volta
let numero = 10;

do {
  console.log("Numero:", numero);
  numero++;
} while (numero < 5);

// Output: "Numero: 10"
// Il blocco viene eseguito una volta, poi la condizione (10 < 5) è falsa
```

**Confronto while vs do...while**:

```javascript
/*
 * while - può non eseguire mai
 */

let a = 10;

while (a < 5) {
  console.log("while:", a); // MAI eseguito
}

/*
 * do...while - esegue almeno una volta
 */

let b = 10;

do {
  console.log("do...while:", b); // Eseguito UNA volta
} while (b < 5);

// Output:
// "do...while: 10"
```

#### Il Ciclo for

Quando il numero di iterazioni è noto in anticipo o si deve contare, il ciclo `for` è spesso la scelta più chiara e compatta. La sua sintassi concentra in un'unica riga **tre parti fondamentali**:

- **Inizializzazione** → Eseguita una sola volta prima del ciclo (es. `let i = 0`)
- **Condizione** → Valutata prima di ogni iterazione. Se falsa, il ciclo termina (es. `i < 10`)
- **Aggiornamento** → Eseguito alla fine di ogni iterazione (es. `i++`)

```javascript
/*
 * Sintassi for
 */

for (inizializzazione; condizione; aggiornamento) {
  // codice eseguito ad ogni iterazione
}

// Esempio: contare da 0 a 4
for (let i = 0; i < 5; i++) {
  console.log(i);
}

// Output:
// 0
// 1
// 2
// 3
// 4
```

**Come funziona il ciclo for**:

```javascript
/*
 * Flusso di esecuzione
 */

for (let i = 0; i < 3; i++) {
  console.log("Iterazione:", i);
}

// 1. let i = 0           → Inizializzazione (una volta)
// 2. i < 3?              → Condizione (true)
// 3. console.log(...)    → Esecuzione blocco
// 4. i++                 → Aggiornamento
// 5. i < 3?              → Condizione (true)
// 6. console.log(...)    → Esecuzione blocco
// 7. i++                 → Aggiornamento
// 8. i < 3?              → Condizione (true)
// 9. console.log(...)    → Esecuzione blocco
// 10. i++                → Aggiornamento
// 11. i < 3?             → Condizione (false) → FINE
```

**Esempi pratici**:

```javascript
/*
 * Iterare all'indietro
 */

for (let i = 5; i > 0; i--) {
  console.log(i);
}
// Output: 5, 4, 3, 2, 1

/*
 * Incrementi diversi
 */

for (let i = 0; i <= 10; i += 2) {
  console.log(i);
}
// Output: 0, 2, 4, 6, 8, 10

/*
 * Iterare su array
 */

let colori = ["rosso", "verde", "blu"];

for (let i = 0; i < colori.length; i++) {
  console.log(colori[i]);
}
// Output: "rosso", "verde", "blu"
```

#### Il Ciclo for...of

Introdotto in **ES6**, il ciclo `for...of` è il modo moderno e più leggibile per iterare sugli elementi di una **struttura iterabile**, come un array o una stringa. Ad ogni iterazione, la variabile del ciclo assume il **valore** dell'elemento corrente.

```javascript
/*
 * Sintassi for...of
 */

for (let elemento of iterabile) {
  // lavora con elemento
}

// Esempio: iterare su array
let frutti = ["mela", "banana", "arancia"];

for (let frutto of frutti) {
  console.log(frutto);
}

// Output:
// "mela"
// "banana"
// "arancia"
```

**for...of con stringhe**:

```javascript
/*
 * Iterare sui caratteri di una stringa
 */

let parola = "ciao";

for (let carattere of parola) {
  console.log(carattere);
}

// Output:
// "c"
// "i"
// "a"
// "o"
```

**Confronto for vs for...of**:

```javascript
/*
 * for tradizionale (con indice)
 */

let numeri = [10, 20, 30];

for (let i = 0; i < numeri.length; i++) {
  console.log(numeri[i]); // Devi accedere con [i]
}

/*
 * for...of (diretto sul valore)
 */

for (let numero of numeri) {
  console.log(numero); // Hai direttamente il valore
}
```

**Vantaggi di for...of**:

- Più leggibile
- Meno propenso agli errori (niente indici fuori range)
- Funziona con qualsiasi iterabile (array, stringhe, Set, Map, ecc.)

#### Il Ciclo for...in

Il ciclo `for...in` è specifico per iterare sulle **proprietà enumerabili** di un oggetto. Ad ogni iterazione, la variabile del ciclo assume il **nome** (la chiave) della proprietà corrente, come stringa.

```javascript
/*
 * Sintassi for...in
 */

for (let chiave in oggetto) {
  // lavora con chiave
}

// Esempio: iterare su oggetto
let persona = {
  nome: "Mario",
  cognome: "Rossi",
  eta: 30,
};

for (let proprieta in persona) {
  console.log(proprieta + ":", persona[proprieta]);
}

// Output:
// "nome: Mario"
// "cognome: Rossi"
// "eta: 30"
```

**⚠️ Importante**: `for...in` **non è raccomandato per array**.

```javascript
/*
 * for...in con array (SCONSIGLIATO)
 */

let numeri = [10, 20, 30];

for (let indice in numeri) {
  console.log(typeof indice); // "string" (!)
  console.log(indice, numeri[indice]);
}

// Output:
// "string"
// "0" 10
// "1" 20
// "2" 30

// Problemi:
// - indice è una stringa, non un numero
// - Potrebbe includere proprietà inaspettate
// - Non garantisce l'ordine
```

**Per array, usare for...of**:

```javascript
/*
 * for...of con array (CONSIGLIATO)
 */

let numeri = [10, 20, 30];

for (let numero of numeri) {
  console.log(numero);
}
```

**Tabella Riepilogativa**:

| Ciclo      | Uso                        | Itera su   |
| ---------- | -------------------------- | ---------- |
| `for...of` | Array, stringhe, iterabili | **Valori** |
| `for...in` | Oggetti                    | **Chiavi** |

#### Interrompere un Ciclo: break

A volte è necessario interrompere un ciclo **prima** che la sua condizione diventi falsa. Per questo si usa l'istruzione `break`. Appena il programma incontra `break`, **esce immediatamente** dal ciclo e continua l'esecuzione dal codice successivo.

```javascript
/*
 * Uso di break
 */

for (let i = 0; i < 10; i++) {
  if (i === 5) {
    break; // Interrompe il ciclo quando i è 5
  }
  console.log(i);
}

// Output:
// 0
// 1
// 2
// 3
// 4
// (il ciclo si ferma, NON stampa 5, 6, 7, 8, 9)
```

**break con while**:

```javascript
/*
 * break per uscire da while
 */

let counter = 0;

while (true) {
  // Ciclo infinito!
  console.log(counter);
  counter++;

  if (counter >= 3) {
    break; // Uscita dal ciclo infinito
  }
}

console.log("Ciclo terminato");

// Output:
// 0
// 1
// 2
// "Ciclo terminato"
```

**Esempio pratico**: cercare un elemento

```javascript
/*
 * Cercare in un array e fermarsi quando trovato
 */

let numeri = [10, 20, 30, 40, 50];
let cercato = 30;
let trovato = false;

for (let numero of numeri) {
  if (numero === cercato) {
    trovato = true;
    console.log("Trovato:", numero);
    break; // Non serve continuare a cercare
  }
}

if (trovato) {
  console.log("Elemento presente");
}
```

#### Saltare un'Iterazione: continue

L'istruzione `continue` **salta** l'iterazione corrente e passa alla successiva, senza uscire dal ciclo.

```javascript
/*
 * Uso di continue
 */

for (let i = 0; i < 5; i++) {
  if (i === 2) {
    continue; // Salta quando i è 2
  }
  console.log(i);
}

// Output:
// 0
// 1
// (salta 2)
// 3
// 4
```

**Esempio pratico**: filtrare valori

```javascript
/*
 * Stampare solo numeri pari
 */

for (let i = 0; i < 10; i++) {
  if (i % 2 !== 0) {
    continue; // Salta i numeri dispari
  }
  console.log(i); // Stampa solo pari
}

// Output: 0, 2, 4, 6, 8
```

#### Best Practices

**Scegliere il ciclo giusto**:

```javascript
// ✅ for - quando sai quante iterazioni
for (let i = 0; i < 10; i++) {
  // ...
}

// ✅ for...of - per iterare su array/stringhe
for (let item of array) {
  // ...
}

// ✅ for...in - per proprietà di oggetti
for (let key in object) {
  // ...
}

// ✅ while - quando non sai quante iterazioni
while (condizione) {
  // ...
}
```

**Evitare cicli infiniti**:

```javascript
// ❌ Ciclo infinito
for (let i = 0; i < 10; ) {
  // MANCA i++!
  console.log(i);
}

// ✅ Incremento presente
for (let i = 0; i < 10; i++) {
  console.log(i);
}
```

**Usare const in for...of quando possibile**:

```javascript
// ✅ const quando non riassegni
for (const item of array) {
  console.log(item);
}

// let solo se devi modificare
for (let item of array) {
  item = item * 2; // Riassegnazione
}
```

**Limitare lavoro nei cicli**:

```javascript
// ❌ Calcolo ripetuto
for (let i = 0; i < array.length; i++) {
  // array.length calcolato ogni volta!
}

// ✅ Calcolo una volta
let len = array.length;
for (let i = 0; i < len; i++) {
  // Più efficiente
}

// ✅ Oppure usa for...of
for (let item of array) {
  // Nessun calcolo length
}
```

**Approfondisci**:

- [[01-fondamenti/sintassi/cicli]] - Cicli (Loops) - Panoramica
- [[01-fondamenti/sintassi/while]] - Ciclo while
- [[01-fondamenti/sintassi/do-while]] - Ciclo do...while
- [[01-fondamenti/sintassi/for]] - Ciclo for
- [[01-fondamenti/sintassi/for-of]] - Ciclo for...of
- [[01-fondamenti/sintassi/for-in]] - Ciclo for...in
- [[01-fondamenti/sintassi/break-continue]] - break e continue

### 2.9 Strict Mode ("Modalità Stretta")

**Tipo**: Nuovo Topic

Introdotta in **ECMAScript 5 (ES5)**, la **strict mode** ("modalità stretta") è una funzionalità che permette di attivare un insieme di regole più restrittive per il codice JavaScript. L'obiettivo è rendere il codice più **sicuro**, **robusto** e meno incline a errori comuni, trasformando "errori silenziosi" in errori espliciti che bloccano l'esecuzione.

#### Perché Usare Strict Mode

L'uso dello strict mode è considerato una **best practice** per tutti i programmi JavaScript moderni, per diverse ragioni:

- **Sicurezza** → Previene pratiche rischiose, come la creazione accidentale di variabili globali
- **Ottimizzazione** → Un codice che aderisce allo strict mode è generalmente più facile da ottimizzare per i motori JavaScript
- **Futuro del Linguaggio** → Rappresenta la direzione in cui il linguaggio si sta evolvendo. Abituarsi a scrivere codice in modalità stretta facilita l'adozione delle future funzionalità di JavaScript

#### Come Attivare lo Strict Mode

Per attivare lo strict mode, è sufficiente inserire la direttiva `"use strict";` (una semplice stringa) all'inizio di un file o di una funzione. La sua **posizione** ne determina l'**ambito di applicazione**.

```javascript
/*
 * Strict mode a livello di file
 */

"use strict";

// Tutto il codice in questo file è in strict mode

let nome = "Mario";
x = 10; // ❌ ReferenceError: x is not defined
```

**A livello di funzione**:

```javascript
/*
 * Strict mode a livello di funzione
 */

function modalitaStretta() {
  "use strict";

  // Solo questa funzione è in strict mode
  y = 5; // ❌ ReferenceError: y is not defined
}

function modalitaNormale() {
  // Questa funzione NON è in strict mode
  z = 10; // ✅ Funziona (crea variabile globale)
}

modalitaStretta(); // Errore
modalitaNormale(); // OK ma sconsigliato
console.log(z); // 10
```

#### Prevenire le Globali Accidentali

Uno dei benefici più importanti dello strict mode è che **impedisce la creazione implicita di variabili globali**. In modalità non-stretta, assegnare un valore a una variabile non dichiarata crea una nuova variabile nello scope globale. In strict mode, questo comportamento è vietato e genera un `ReferenceError`.

```javascript
/*
 * Modalità non-stretta (comportamento pericoloso)
 */

function nonStrictMode() {
  // Nessun "use strict"

  contatore = 0; // ❌ Crea variabile GLOBALE accidentalmente
  contatore++;
}

nonStrictMode();
console.log(contatore); // 1 (variabile globale!)
```

```javascript
/*
 * Strict mode (comportamento sicuro)
 */

function strictMode() {
  "use strict";

  contatore = 0; // ❌ ReferenceError: contatore is not defined
  contatore++;
}

strictMode(); // Errore bloccato subito
```

Questo costringe lo sviluppatore a **dichiarare sempre esplicitamente** le proprie variabili (con `let`, `const` o `var`), prevenendo bug difficili da tracciare.

```javascript
/*
 * ✅ Versione corretta con strict mode
 */

function strictModeCorrretto() {
  "use strict";

  let contatore = 0; // ✅ Dichiarazione esplicita
  contatore++;
  console.log(contatore); // 1
}

strictModeCorrretto(); // Funziona correttamente
```

#### Altre Restrizioni dello Strict Mode

Lo strict mode introduce molte altre regole. Ecco alcuni esempi comuni:

**Niente duplicati nei parametri**:

```javascript
/*
 * Parametri duplicati vietati
 */

"use strict";

function esempio(a, a, b) {
  // ❌ SyntaxError: Duplicate parameter name
  return a + b;
}
```

**Niente assegnamenti a proprietà read-only**:

```javascript
/*
 * Assegnamenti non validi vietati
 */

"use strict";

let obj = {};
Object.defineProperty(obj, "prop", {
  value: 42,
  writable: false,
});

obj.prop = 77; // ❌ TypeError: Cannot assign to read only property
```

**Niente delete su variabili**:

```javascript
/*
 * Delete su variabili vietato
 */

"use strict";

let x = 10;
delete x; // ❌ SyntaxError: Delete of an unqualified identifier
```

#### Best Practices

- **Attiva strict mode** in tutti i nuovi progetti
- **Dichiarate sempre variabili** con `let`, `const` o `var`
- **Usa moduli ES6** (automaticamente strict)
- **Non mischiare strict e non-strict** nello stesso file

```javascript
/*
 * ✅ Struttura consigliata
 */

"use strict";

// Tutto il file in strict mode
// Codice pulito e sicuro

let dati = [];

function elabora(item) {
  let risultato = item * 2;
  return risultato;
}
```

#### Affrontare i Problemi

Se l'attivazione dello strict mode causa problemi nel tuo programma, **non è un motivo per evitarlo**. Al contrario, è un **segnale** che il tuo codice contiene delle "cattive pratiche" che devono essere corrette. Affrontare questi problemi rende il codice più affidabile e allineato agli standard moderni.

**Approfondisci**:

- [[01-fondamenti/sintassi/strict-mode]] - Strict Mode

---

## 3. Tipi e Dati

### 3.1 Valori e Tipi (Values & Types)

**Tipo**: Nuovo Topic

In un programma, i dati vengono rappresentati in modi diversi a seconda dello scopo per cui vengono usati. Queste diverse rappresentazioni sono chiamate tipi (types). JavaScript definisce alcuni tipi di dati primitivi e fondamentali (built-in types) per gestire le informazioni e sono:

- **string** (per il testo)
- **number** (per i valori numerici)
- **boolean** (per i valori logici true/false)
- **null** e **undefined** (per rappresentare l'assenza di valore)
- **object** (per strutture di dati complesse)
- **symbol** (un tipo speciale introdotto in ES6 per creare identificatori unici)

```javascript
/*
 * Tipi primitivi in JavaScript
 */

// string - Testo racchiuso tra virgolette
let nome = "Mario";
let cognome = "Rossi";
let frase = `Ciao, ${nome}!`; // Template literal (ES6)

// number - Numeri interi o decimali
let intero = 42;
let decimale = 3.14;
let negativo = -10;
let infinito = Infinity;
let nonUnNumero = NaN; // Not a Number

// boolean - Valori logici
let isVero = true;
let isFalso = false;
let maggiorenne = eta >= 18; // risultato di un confronto

// null - Assenza intenzionale di valore
let valoreSconosciuto = null;

// undefined - Variabile dichiarata ma non inizializzata
let valoreNonDefinito;
console.log(valoreNonDefinito); // undefined

let proprieta = obj.propInesistente; // undefined

// object - Strutture dati complesse
let persona = {
  nome: "Mario",
  eta: 30,
  citta: "Roma",
};

let numeri = [1, 2, 3, 4, 5]; // Gli array sono oggetti

let data = new Date(); // Anche Date è un oggetto

// symbol - Identificatori unici (ES6)
let id1 = Symbol("id");
let id2 = Symbol("id");
console.log(id1 === id2); // false (symbol sono sempre unici)

/*
 * Esempi pratici di utilizzo
 */

// Stringhe per contenuto testuale
let benvenuto = "Benvenuto nel sistema";
let email = "utente@example.com";

// Numeri per calcoli
let prezzo = 99.99;
let quantita = 3;
let totale = prezzo * quantita; // 299.97

// Boolean per logica condizionale
let isLoggedIn = true;
if (isLoggedIn) {
  console.log("Accesso consentito");
}

// null per assenza esplicita
let risultatoRicerca = null; // nessun risultato trovato
if (risultatoRicerca === null) {
  console.log("Ricerca senza risultati");
}

// undefined per valori non ancora assegnati
function saluta(nome) {
  if (nome === undefined) {
    nome = "Ospite"; // valore di default
  }
  return "Ciao " + nome;
}
console.log(saluta()); // "Ciao Ospite"

// Object per dati strutturati
let prodotto = {
  codice: "ABC123",
  nome: "Laptop",
  prezzo: 899.99,
  disponibile: true,
};

// Symbol per chiavi uniche di oggetti
let ID_UTENTE = Symbol("userId");
let utente = {
  [ID_UTENTE]: 12345,
  nome: "Anna",
};
console.log(utente[ID_UTENTE]); // 12345
```

Per determinare il tipo di un valore durante l'esecuzione del programma, si utilizza l'operatore `typeof`. Vedere la sezione dedicata in [[typeof]] per i dettagli completi.

---

### 3.2 Tipizzazione Dinamica (Dynamic Typing)

**Tipo**: Nuovo Topic

JavaScript è un linguaggio a tipizzazione dinamica. Questo significa che una variabile non è legata a un tipo di dato specifico. La stessa variabile può contenere un number in un momento, e una string in un momento successivo. Questa flessibilità permette di usare una singola variabile per rappresentare un valore che cambia forma nel corso del programma.

```javascript
let valore = 42;
console.log(typeof valore); // "number"

valore = "Ciao!";
console.log(typeof valore); // "string"

valore = true;
console.log(typeof valore); // "boolean"
```

```javascript
/*
 * Esempi di tipizzazione dinamica in JavaScript
 */

// Una variabile può cambiare tipo durante l'esecuzione
let dato = 100;
console.log("Valore:", dato, "- Tipo:", typeof dato); // Valore: 100 - Tipo: number

dato = "Centoventi";
console.log("Valore:", dato, "- Tipo:", typeof dato); // Valore: Centoventi - Tipo: string

dato = { valore: 100 };
console.log("Valore:", dato, "- Tipo:", typeof dato); // Valore: { valore: 100 } - Tipo: object

dato = [1, 2, 3];
console.log("Valore:", dato, "- Tipo:", typeof dato); // Valore: [1, 2, 3] - Tipo: object

dato = function () {
  return 42;
};
console.log("Valore:", dato, "- Tipo:", typeof dato); // Valore: function - Tipo: function

/*
 * Esempio pratico: gestione di risposte di diverso tipo
 */
function processaRisposta(risposta) {
  console.log("Tipo ricevuto:", typeof risposta);

  if (typeof risposta === "number") {
    console.log("Numero ricevuto:", risposta);
  } else if (typeof risposta === "string") {
    console.log("Testo ricevuto:", risposta);
  } else if (typeof risposta === "boolean") {
    console.log("Booleano ricevuto:", risposta);
  } else if (typeof risposta === "object") {
    console.log("Oggetto ricevuto:", risposta);
  }
}

// La stessa funzione accetta tipi diversi
processaRisposta(42); // Tipo ricevuto: number
processaRisposta("Ciao"); // Tipo ricevuto: string
processaRisposta(true); // Tipo ricevuto: boolean
processaRisposta({ id: 1 }); // Tipo ricevuto: object

/*
 * Vantaggi e svantaggi della tipizzazione dinamica
 */

// VANTAGGI: Flessibilità
let risultato; // Non serve dichiarare il tipo

if (Math.random() > 0.5) {
  risultato = "Testa";
} else {
  risultato = 0;
}
// La variabile può contenere string o number

// SVANTAGGI: Possibili errori runtime
function somma(a, b) {
  return a + b;
}

console.log(somma(5, 3)); // 8 (numero + numero)
console.log(somma("5", 3)); // "53" (stringa + numero = concatenazione!)
console.log(somma("Ciao", 3)); // "Ciao3" (comportamento inatteso)

// Soluzione: validare i tipi quando necessario
function sommaNumeri(a, b) {
  if (typeof a !== "number" || typeof b !== "number") {
    throw new Error("Entrambi gli argomenti devono essere numeri");
  }
  return a + b;
}

console.log(sommaNumeri(5, 3)); // 8
// console.log(sommaNumeri("5", 3)); // ❌ Error: Entrambi gli argomenti devono essere numeri
```

### 3.3 Coercizione (Type Coercion)

**Tipo**: Nuovo Topic

Spesso è necessario convertire un valore da un tipo a un altro. Ad esempio, un number deve diventare una string per essere visualizzato, o una string inserita in un form deve diventare un number per essere usata in un calcolo. Questo processo di conversione in JavaScript è chiamato **coercizione** (coercion).

Esistono due tipi di coercizione: **esplicita** e **implicita**.

#### Coercizione Esplicita (Explicit Coercion)

Si ha una coercizione esplicita quando il programmatore chiede deliberatamente di convertire un tipo. Si usano costrutti del linguaggio fatti apposta per questo scopo, come le funzioni `Number()`, `String()`, `Boolean()`, `parseInt()` e `parseFloat()`. L'intenzione è chiara e il risultato prevedibile.

```javascript
/*
 * Esempi di coercizione esplicita
 */

// String → Number
let prezzo = "99.99";
let prezzoNumerico = Number(prezzo);
console.log(prezzoNumerico); // 99.99
console.log(typeof prezzoNumerico); // "number"

let quantita = "42";
let quantitaInt = parseInt(quantita);
console.log(quantitaInt); // 42

let valore = "3.14159";
let valoreFloat = parseFloat(valore);
console.log(valoreFloat); // 3.14159

// Number → String
let numero = 42;
let numeroStringa = String(numero);
console.log(numeroStringa); // "42"
console.log(typeof numeroStringa); // "string"

// Alternativa con .toString()
let eta = 25;
let etaStringa = eta.toString();
console.log(etaStringa); // "25"

// Boolean → String/Number
let attivo = true;
console.log(String(attivo)); // "true"
console.log(Number(attivo)); // 1
console.log(Number(false)); // 0

// Any → Boolean
console.log(Boolean(1)); // true
console.log(Boolean(0)); // false
console.log(Boolean("testo")); // true
console.log(Boolean("")); // false
console.log(Boolean(null)); // false
console.log(Boolean(undefined)); // false
console.log(Boolean({})); // true
console.log(Boolean([])); // true

/*
 * Caso pratico: validazione input utente
 */
function calcolaTotale(prezzoInput, quantitaInput) {
  // Conversione esplicita da string a number
  const prezzo = parseFloat(prezzoInput);
  const quantita = parseInt(quantitaInput);

  // Validazione
  if (isNaN(prezzo) || isNaN(quantita)) {
    return "Input non valido";
  }

  return prezzo * quantita;
}

console.log(calcolaTotale("19.99", "3")); // 59.97
console.log(calcolaTotale("abc", "3")); // "Input non valido"
```

#### Coercizione Implicita (Implicit Coercion)

La coercizione implicita avviene automaticamente quando JavaScript incontra un'operazione tra tipi diversi. Gli esempi più comuni sono:

- L'uso dell'operatore di uguaglianza lasca (`==`)
- L'operatore `+` con string e number
- Contesti booleani (if, while, etc.)

Quando si confrontano due valori di tipo diverso con `==`, JavaScript tenta di "aiutare" convertendone uno per farli corrispondere, prima di eseguire il confronto.

```javascript
/*
 * Esempi di coercizione implicita
 */

// == con tipi diversi
console.log("99.99" == 99.99); // true (string → number)
console.log(42 == "42"); // true (string → number)
console.log(true == 1); // true (boolean → number)
console.log(false == 0); // true (boolean → number)
console.log(null == undefined); // true (caso speciale)

// Operatore + con string
console.log(5 + 3); // 8 (number + number)
console.log("5" + 3); // "53" (number → string, concatenazione)
console.log(5 + "3"); // "53" (number → string, concatenazione)
console.log("Il risultato è " + 42); // "Il risultato è 42"

// Altri operatori matematici con string
console.log("10" - 5); // 5 (string → number)
console.log("10" * "2"); // 20 (entrambe string → number)
console.log("20" / "4"); // 5 (entrambe string → number)

// Contesto booleano (if, while, etc.)
if ("testo") {
  // string non vuota → true
  console.log("Eseguito");
}

if (0) {
  // 0 → false
  console.log("Non eseguito");
}

if ([]) {
  // array vuoto → true
  console.log("Array vuoto è truthy!");
}

// Casi complessi e ingannevoli
console.log([] + []); // "" (entrambi → string vuota)
console.log([] + {}); // "[object Object]"
console.log({} + []); // 0 (in alcuni contesti)
console.log("" == 0); // true
console.log(false == ""); // true
console.log(false == []); // true

/*
 * Esempio pratico con coercizione implicita
 */
function verificaAccesso(userId) {
  // null e undefined vengono entrambi catturati con ==
  if (userId == null) {
    console.log("Utente non autenticato");
    return false;
  }

  console.log("Accesso consentito per utente:", userId);
  return true;
}

verificaAccesso(123); // Accesso consentito per utente: 123
verificaAccesso(null); // Utente non autenticato
verificaAccesso(undefined); // Utente non autenticato
```

#### La Controversia sulla Coercizione Implicita

La coercizione implicita è uno degli argomenti più controversi in JavaScript.

- **La Critica** → Molti sviluppatori la considerano una fonte di bug e confusione. Poiché le sue regole non sono sempre intuitive, il consiglio diffuso è di evitarla completamente, preferendo sempre l'operatore di uguaglianza stretta (`===`), che non esegue coercizione.

- **L'Altra Prospettiva** → Evitare la coercizione implicita a priori significa non padroneggiare completamente il linguaggio. Se compresa, può rendere il codice più leggibile ed espressivo. Ad esempio, `userId == null` cattura sia `null` che `undefined` in un solo confronto elegante.

**Best Practice**:

- Preferire `===` quando si vuole evitare sorprese
- Usare `==` consapevolmente quando la coercizione è vantaggiosa (es. `value == null`)
- Evitare `==` con valori che possono essere `true`, `false`, `0`, `""`, `[]`
- Usare sempre coercizione **esplicita** quando la conversione è il cuore della logica

```javascript
/*
 * Confronto tra approcci
 */

// ❌ Coercizione implicita confusa
if (prezzoInput == 0) {
  // problematico: cattura "", [], false
}

// ✅ Coercizione esplicita chiara
if (Number(prezzoInput) === 0) {
  // esplicito e prevedibile
}

// ✅ Caso valido per ==
function isNullOrUndefined(value) {
  return value == null; // cattura entrambi elegantemente
}

// Alternativa più verbosa
function isNullOrUndefinedVerboso(value) {
  return value === null || value === undefined;
}
```

### 3.4 Valori Truthy e Falsy

**Tipo**: Nuovo Topic

In JavaScript, quando un valore non booleano viene usato in un **contesto che si aspetta un booleano** (come la condizione di un `if` o l'operando di un operatore logico), il linguaggio lo converte implicitamente in `true` o `false`. Questo processo è chiamato **coercizione booleana**, e i valori vengono classificati come **truthy** o **falsy** in base al risultato.

#### Valori Falsy

I valori **falsy** sono quelli che, quando forzati a diventare booleani, si convertono in `false`. La lista dei valori falsy è **breve e ben definita**:

```javascript
/*
 * Lista COMPLETA dei valori falsy
 */

false; // ovviamente falsy
0 - // zero
  0; // zero negativo
0n; // BigInt zero
(""); // stringa vuota
"" // stringa vuota (apici singoli)
``; // stringa vuota (template literal)
null; // assenza intenzionale di valore
undefined; // valore non definito/assegnato
NaN; // Not a Number
```

**Qualsiasi valore che non rientra in questa lista è considerato truthy**.

#### Valori Truthy

Un valore **truthy** è qualsiasi valore che, quando convertito in booleano, diventa `true`. Questo include praticamente **tutto il resto**.

```javascript
/*
 * Esempi di valori truthy
 */

// Stringhe non vuote
"ciao"          // truthy
"0"             // truthy (stringa, non numero!)
"false"         // truthy (stringa, non boolean!)
" "             // truthy (spazio non è stringa vuota)

// Numeri diversi da zero
42              // truthy
-1              // truthy
3.14            // truthy
Infinity        // truthy

// Array (anche vuoti!)
[]              // truthy ⚠️
[0]             // truthy

// Oggetti (anche vuoti!)
{}              // truthy ⚠️
{a: 0}          // truthy

// Funzioni
function() {}   // truthy
```

**⚠️ Attenzione**: Anche un **array vuoto** `[]` o un **oggetto vuoto** `{}` sono **truthy**. Questo può generare confusione.

```javascript
/*
 * Array e oggetti vuoti sono truthy!
 */

let arrayVuoto = [];

if (arrayVuoto) {
  console.log("Questo VIENE eseguito!"); // ✅
}

// Per controllare se un array è vuoto:
if (arrayVuoto.length === 0) {
  console.log("Array vuoto"); // ✅ Modo corretto
}
```

#### Utilizzo Pratico

La conoscenza dei valori truthy e falsy permette di scrivere codice più **conciso e leggibile**.

**Controllo Esistenza Valore**

```javascript
/*
 * Controllo se una variabile ha un valore
 */

let nomeUtente = "Mario";

// ❌ Modo verboso
if (nomeUtente !== null && nomeUtente !== undefined && nomeUtente !== "") {
  console.log("Benvenuto, " + nomeUtente);
}

// ✅ Modo conciso (sfrutta truthy/falsy)
if (nomeUtente) {
  console.log("Benvenuto, " + nomeUtente);
}
```

Se `nomeUtente` contiene una stringa non vuota (valore truthy), la condizione è vera. Se contiene `""`, `null`, o `undefined` (valori falsy), la condizione è falsa.

**Default Values**

```javascript
/*
 * Assegnare valori di default
 */

let userInput = "";
let messaggio = userInput || "Messaggio di default";

console.log(messaggio); // "Messaggio di default"
```

**Conversione Esplicita a Boolean**

```javascript
/*
 * Conversione esplicita
 */

// Usando Boolean()
let valore1 = Boolean("ciao"); // true
let valore2 = Boolean(""); // false

// Usando doppia negazione !!
let valore3 = !!"ciao"; // true
let valore4 = !!""; // false

// Come funziona !!
// !"ciao" → !true → false
// !!"ciao" → !false → true
```

#### Best Practices

**Uso Consapevole**

```javascript
/*
 * Attenzione con numeri - 0 è falsy!
 */

// ⚠️ Problema
function calcola(numero) {
  if (!numero) {
    // ❌ Salta anche se numero === 0!
    numero = 10;
  }
  return numero * 2;
}

// ✅ Controllo esplicito per numeri
function calcolaCorretto(numero) {
  if (numero === undefined || numero === null) {
    numero = 10;
  }
  return numero * 2;
}
```

**Chiarezza vs Concisione**

```javascript
// ✅ Conciso per stringhe/oggetti
if (user.nome) {
  // lavora con nome
}

// ✅ Esplicito per numeri/booleani
if (counter !== 0) {
  // 0 è valore valido
}
```

**Approfondisci**:

- [[01-fondamenti/tipi/truthy-falsy]] - Valori truthy e falsy
- [[01-fondamenti/tipi/coercizione]] - Coercizione di tipo
- [[01-fondamenti/sintassi/condizionali]] - Uso nelle condizioni

---

### 3.5 Boxing e Metodi dei Primitivi

**Tipo**: Nuovo Topic

In JavaScript, anche i **tipi primitivi** (string, number, boolean) possono esporre metodi e proprietà utili per manipolarli, nonostante non siano oggetti. Questo avviene grazie al meccanismo del **boxing**.

```javascript
/*
 * Metodi sui tipi primitivi
 */

let testo = "javascript";
console.log(testo.length); // 10 (proprietà)
console.log(testo.toUpperCase()); // "JAVASCRIPT" (metodo)

let numero = 3.14159;
console.log(numero.toFixed(2)); // "3.14" (metodo)

// Come è possibile? I primitivi non sono oggetti!
```

#### Il Meccanismo del Boxing

Il **boxing** è il processo automatico con cui JavaScript "avvolge" temporaneamente un valore primitivo in un oggetto wrapper quando si tenta di accedere a una proprietà o metodo.

**Processo**:

- JavaScript crea automaticamente un oggetto wrapper temporaneo (String, Number, Boolean)
- L'oggetto wrapper contiene i metodi del tipo corrispondente
- Il metodo viene eseguito
- L'oggetto wrapper viene immediatamente scartato

```javascript
/*
 * Cosa succede dietro le quinte
 */

let a = "ciao";

// Quando scrivi a.toUpperCase():
// 1. new String("ciao") creato temporaneamente
// 2. String.prototype.toUpperCase() viene chiamato
// 3. Risultato "CIAO" restituito
// 4. Oggetto String temporaneo eliminato

console.log(a.toUpperCase()); // "CIAO"
console.log(typeof a); // "string" (ancora primitivo!)
```

Il processo è **completamente trasparente** per lo sviluppatore, ma comprendere questo meccanismo aiuta a capire come funziona JavaScript internamente.

#### Wrapper Objects vs Primitivi

**Regola fondamentale**: Preferire sempre i **valori primitivi**, lasciare il boxing automatico a JavaScript.

```javascript
/*
 * Differenza tra primitivo e wrapper object
 */

// ✅ Primitivo (consigliato)
let str1 = "testo";
let num1 = 42;
let bool1 = true;

// ❌ Wrapper object (sconsigliato)
let str2 = new String("testo");
let num2 = new Number(42);
let bool2 = new Boolean(true);

console.log(typeof str1); // "string"
console.log(typeof str2); // "object" (!)

// Problemi con wrapper objects
console.log(str1 === "testo"); // true
console.log(str2 === "testo"); // false (object vs string)
```

#### Conversione Esplicita a Number

**Operatore Unario +** - Modo moderno e conciso:

```javascript
/*
 * Operatore unario +
 */

let str = "42";
let num = +str; // 42

console.log(+"99.99"); // 99.99
console.log(+true); // 1
console.log(+false); // 0
console.log(+""); // 0
console.log(+"testo"); // NaN
```

**parseInt() e parseFloat()** - Per parsare stringhe:

```javascript
/*
 * Parsing di stringhe a numeri
 */

// parseInt(string, radix)
console.log(parseInt("42")); // 42
console.log(parseInt("42.99")); // 42 (solo parte intera)
console.log(parseInt("42px")); // 42 (ignora il resto)
console.log(parseInt("3.14")); // 3

// parseFloat(string)
console.log(parseFloat("3.14")); // 3.14
console.log(parseFloat("99.99€")); // 99.99 (ignora simboli)
```

**Number()** - Conversione completa:

```javascript
/*
 * Conversione con Number()
 */

Number("42"); // 42
Number("3.14"); // 3.14
Number("42px"); // NaN (stringa non valida)
Number(true); // 1
Number(false); // 0
```

#### Conversione Esplicita a String

**String()** - Sicura con tutti i valori:

```javascript
/*
 * Conversione con String()
 */

String(42); // "42"
String(true); // "true"
String(null); // "null"
String(undefined); // "undefined"
String([1, 2]); // "1,2"
```

**.toString()** - Metodo su valori (non su null/undefined):

```javascript
/*
 * Conversione con .toString()
 */

let num = 42;
num.toString(); // "42"

true.toString(); // "true"

// ❌ Errori con null/undefined
// null.toString();      // TypeError
// undefined.toString(); // TypeError
```

**Raccomandazione**: Usare **String()** per robustezza, evita errori con `null` e `undefined`.

**Approfondisci**:

- [[01-fondamenti/tipi/boxing]] - Boxing e metodi dei primitivi
- [[01-fondamenti/tipi/coercizione]] - Coercizione esplicita e implicita
- [[01-fondamenti/tipi/valori-tipi]] - Tipi primitivi vs Object

---

### 3.6 Oggetti (Objects)

**Tipo**: Nuovo Topic

Il tipo **object** è uno dei più potenti e versatili in JavaScript. Un oggetto è un valore composto, una sorta di contenitore che raggruppa dati e funzionalità correlate. Questi dati sono organizzati come una collezione di **proprietà** (properties), dove ogni proprietà è una coppia **chiave-valore**. La chiave è un nome (una stringa), e il valore può essere di qualsiasi tipo: un numero, una stringa, un booleano, una funzione o persino un altro oggetto.

```javascript
/*
 * Creazione e uso degli oggetti
 */

// Definizione di un oggetto
let persona = {
  nome: "Mario",
  cognome: "Rossi",
  eta: 30,
  citta: "Roma",
  isAttivo: true,
};

console.log(persona); // { nome: 'Mario', cognome: 'Rossi', eta: 30, ... }

// Oggetto più complesso
let prodotto = {
  codice: "ABC123",
  nome: "Laptop",
  prezzo: 899.99,
  disponibile: true,
  specifiche: {
    // oggetto annidato
    processore: "Intel i7",
    ram: "16GB",
    storage: "512GB SSD",
  },
  tags: ["elettronica", "computer", "ufficio"], // array come proprietà
};
```

#### Accesso alle Proprietà

Esistono due modi per accedere alle proprietà di un oggetto:

- **Dot Notation (Notazione a Punto)** → È la sintassi più comune, breve e leggibile. Si usa il nome dell'oggetto seguito da un punto e dal nome della proprietà.

```javascript
let persona = {
  nome: "Mario",
  cognome: "Rossi",
  eta: 30,
};

// Accesso con dot notation
console.log(persona.nome); // "Mario"
console.log(persona.cognome); // "Rossi"
console.log(persona.eta); // 30
```

- **Bracket Notation (Notazione a Parentesi Quadre)** → Si usa il nome dell'oggetto seguito da parentesi quadre `[]` che contengono il nome della proprietà come stringa. Questa notazione è indispensabile in due casi:
  1. Quando il nome della proprietà contiene spazi o caratteri speciali

2. Quando il nome della proprietà è memorizzato in una variabile

```javascript
let persona = {
  nome: "Mario",
  "nome completo": "Mario Rossi", // proprietà con spazio
  "indirizzo-email": "mario@example.com", // proprietà con carattere speciale
};

// Bracket notation
console.log(persona["nome"]); // "Mario"
console.log(persona["nome completo"]); // "Mario Rossi" (spazi nel nome)
console.log(persona["indirizzo-email"]); // "mario@example.com"

// Con dot notation NON funzionerebbe:
// console.log(persona.nome completo); // ❌ Errore di sintassi

// Proprietà dinamica (in variabile)
let proprieta = "nome";
console.log(persona[proprieta]); // "Mario" (valore della variabile usato come chiave)

let campo = "cognome";
console.log(persona[campo]); // "Rossi"

// Esempio pratico con variabile
function ottieniValore(obj, chiave) {
  return obj[chiave]; // bracket notation con parametro
}

console.log(ottieniValore(persona, "nome")); // "Mario"
console.log(ottieniValore(persona, "eta")); // 30
```

#### Manipolare le Proprietà

Le proprietà di un oggetto possono essere aggiunte, modificate o eliminate dinamicamente.

```javascript
/*
 * Aggiunta e modifica di proprietà
 */
let auto = {
  marca: "Fiat",
  modello: "500",
};

// Aggiungere nuove proprietà
auto.anno = 2020; // dot notation
auto["colore"] = "rosso"; // bracket notation

console.log(auto);
// { marca: 'Fiat', modello: '500', anno: 2020, colore: 'rosso' }

// Modificare proprietà esistenti
auto.anno = 2021;
auto["colore"] = "blu";

console.log(auto);
// { marca: 'Fiat', modello: '500', anno: 2021, colore: 'blu' }

/*
 * Eliminare proprietà con delete
 */
let utente = {
  id: 1,
  nome: "Anna",
  email: "anna@example.com",
  password: "secret123",
};

// Rimuovere una proprietà
delete utente.password;

console.log(utente);
// { id: 1, nome: 'Anna', email: 'anna@example.com' }

console.log(utente.password); // undefined
```

#### L'Impatto sulle Performance: Oggetti "Fast" vs. "Dictionary"

Questa è una distinzione importante che avviene "sotto il cofano" del motore JavaScript (come V8, quello di Chrome e Node.js).

- **Oggetti "Fast" (con Hidden Classes)** → Quando si crea un oggetto con una struttura definita, il motore V8 lo ottimizza. Crea una "classe nascosta" (hidden class), una sorta di schema o blueprint che descrive la forma dell'oggetto (quali chiavi ha e in che ordine). Gli oggetti che condividono la stessa struttura possono usare la stessa hidden class, rendendo l'accesso alle loro proprietà estremamente veloce, quasi come accedere a un campo di una struct in C++.

- **Oggetti "Dictionary" (o "Slow")** → Quando si altera la forma di un oggetto in modo imprevedibile, ad esempio aggiungendo o eliminando proprietà dinamicamente (specialmente con `delete`), il motore non può più fare affidamento sulla hidden class. L'ottimizzazione salta e l'oggetto viene declassato a una struttura più lenta, simile a un dizionario o una hash map. L'accesso alle proprietà diventa più lento perché il motore deve cercare la chiave in un dizionario invece di accedere a una posizione di memoria fissa.

In sintesi, usare `delete` è funzionale, ma può avere un costo in termini di performance perché trasforma un oggetto da "fast" a "slow".

```javascript
/*
 * Oggetti ottimizzati (fast) vs non ottimizzati (slow)
 */

// ✅ FAST - Struttura prevedibile
let persona1 = { nome: "Mario", eta: 30 };
let persona2 = { nome: "Luigi", eta: 25 };
let persona3 = { nome: "Anna", eta: 28 };
// Tutti e tre condividono la stessa hidden class (nome, eta)

// ❌ SLOW - Struttura mutata con delete
let utente = { id: 1, nome: "Mario", email: "mario@example.com" };
delete utente.email; // L'oggetto diventa "dictionary mode"
// Adesso l'accesso a utente.nome è più lento
```

#### Alternative Moderne e Immutabili a delete

Per evitare le penalità di performance e seguire un approccio più moderno e "immutabile" (cioè creare un nuovo oggetto con le modifiche desiderate invece di alterare l'originale), esistono tecniche migliori per "rimuovere" una proprietà.

**Destrutturazione con Rest Syntax (...)**

Questo è il metodo più comune e leggibile. Si "estrae" la proprietà che si vuole rimuovere e si raccolgono tutte le altre in un nuovo oggetto usando l'operatore rest (`...`).

```javascript
/*
 * Rimozione immutabile con destrutturazione
 */
let persona = {
  nome: "Mario",
  cognome: "Rossi",
  eta: 30,
  email: "mario@example.com",
};

// Rimuovere la proprietà email (creando un nuovo oggetto)
let { email, ...personaSenzaEmail } = persona;

console.log(personaSenzaEmail);
// { nome: 'Mario', cognome: 'Rossi', eta: 30 }

console.log(persona);
// { nome: 'Mario', cognome: 'Rossi', eta: 30, email: 'mario@example.com' }
// L'originale rimane intatto!

// Rimuovere più proprietà
let { email: _, eta: __, ...personaMinima } = persona;
console.log(personaMinima);
// { nome: 'Mario', cognome: 'Rossi' }
```

**Object.entries, filter, e Object.fromEntries**

Questo approccio è più verboso ma molto potente, specialmente se la logica di filtraggio è complessa.

- `Object.entries(persona)` → Converte l'oggetto in un array di coppie `[chiave, valore]`
- `.filter()` → Filtra questo array, tenendo solo le coppie che non corrispondono alla chiave da rimuovere
- `Object.fromEntries()` → Riconverte l'array filtrato in un nuovo oggetto

```javascript
/*
 * Rimozione con Object.entries e filter
 */
let persona = {
  nome: "Mario",
  cognome: "Rossi",
  eta: 30,
  email: "mario@example.com",
  password: "secret123",
};

// Rimuovere una proprietà specifica
let personaSenzaPassword = Object.fromEntries(
  Object.entries(persona).filter(([chiave, valore]) => chiave !== "password"),
);

console.log(personaSenzaPassword);
// { nome: 'Mario', cognome: 'Rossi', eta: 30, email: 'mario@example.com' }

// Rimuovere più proprietà
let campiDaRimuovere = ["password", "email"];
let personaPubblica = Object.fromEntries(
  Object.entries(persona).filter(
    ([chiave, valore]) => !campiDaRimuovere.includes(chiave),
  ),
);

console.log(personaPubblica);
// { nome: 'Mario', cognome: 'Rossi', eta: 30 }

// Filtraggio condizionale (rimuovere proprietà undefined/null)
let datiIncompleti = {
  nome: "Mario",
  cognome: null,
  eta: 30,
  email: undefined,
  telefono: "123456789",
};

let datiPuliti = Object.fromEntries(
  Object.entries(datiIncompleti).filter(
    ([_, valore]) => valore !== null && valore !== undefined,
  ),
);

console.log(datiPuliti);
// { nome: 'Mario', eta: 30, telefono: '123456789' }
```

Questo metodo crea un nuovo oggetto ottimizzato ("fast") fin dall'inizio, senza mai alterare l'originale.

#### Oggetti come Riferimenti

Un concetto fondamentale è che le variabili non contengono direttamente l'oggetto, ma un **riferimento** (reference) alla sua posizione in memoria. Questo significa che due variabili diverse possono puntare allo stesso oggetto.

```javascript
/*
 * Oggetti come riferimenti
 */

// Due variabili che puntano allo stesso oggetto
let persona1 = {
  nome: "Mario",
  eta: 30,
};

let persona2 = persona1; // persona2 punta allo stesso oggetto

persona2.eta = 31; // Modifica tramite persona2

console.log(persona1.eta); // 31 (anche persona1 vede il cambiamento!)
console.log(persona2.eta); // 31

console.log(persona1 === persona2); // true (stesso riferimento)

/*
 * Oggetti con le stesse proprietà NON sono uguali
 */
let auto1 = { marca: "Fiat", modello: "500" };
let auto2 = { marca: "Fiat", modello: "500" };

console.log(auto1 === auto2); // false (due oggetti diversi in memoria)

// Anche se hanno le stesse proprietà con gli stessi valori,
// sono due entità distinte

/*
 * Copiare un oggetto (shallow copy)
 */
let originale = {
  nome: "Mario",
  eta: 30,
};

// Creare una copia indipendente con spread operator
let copia = { ...originale };

copia.eta = 31;

console.log(originale.eta); // 30 (originale non modificato)
console.log(copia.eta); // 31
console.log(originale === copia); // false (oggetti diversi)

/*
 * Attenzione: shallow copy con oggetti annidati
 */
let utente = {
  nome: "Mario",
  indirizzo: {
    citta: "Roma",
    cap: "00100",
  },
};

let copiaUtente = { ...utente };

copiaUtente.indirizzo.citta = "Milano"; // Modifica l'oggetto annidato

console.log(utente.indirizzo.citta); // "Milano" (anche l'originale cambia!)
// L'oggetto annidato è ancora condiviso (riferimento)

// Per una copia profonda (deep copy) bisogna usare altre tecniche
let copiaProfonda = JSON.parse(JSON.stringify(utente));
// Oppure librerie come lodash (_.cloneDeep)
```

### 3.7 Array

**Tipo**: Nuovo Topic

In JavaScript, anche gli **array** e le **funzioni** sono, a un livello più profondo, dei tipi speciali di oggetti. Hanno funzionalità aggiuntive (come l'accesso agli elementi tramite indice per gli array o la possibilità di essere invocate per le funzioni), ma ereditano le caratteristiche di base degli oggetti.

#### Cos'è un Array

Un **array** è una struttura dati, un **tipo speciale di oggetto**, progettato per contenere una **collezione ordinata di elementi**. A differenza degli oggetti generici, dove i valori sono associati a chiavi testuali (nomi di proprietà), in un array i valori sono posizionati in base a un **indice numerico**.

```javascript
let frutti = ["mela", "banana", "arancia"];
//           [  0  ,    1    ,     2     ]  ← indici

console.log(frutti[0]); // "mela"
console.log(frutti[1]); // "banana"
console.log(frutti.length); // 3
```

**Caratteristiche chiave**:

- **Indicizzazione da 0**: il primo elemento ha indice `[0]`, il secondo `[1]`, ecc.
- **Accesso tramite `[]`**: si usano le parentesi quadre con il numero della posizione
- **Proprietà `length`**: indica il numero di elementi, aggiornata automaticamente

#### Array vs Oggetti

Sebbene `typeof` restituisca `"object"` per un array, è importante usare ciascuno per il suo scopo specifico:

```javascript
let numeri = [10, 20, 30]; // ✅ Array per liste ordinate
let persona = { nome: "Mario", eta: 30 }; // ✅ Oggetto per proprietà nominate

console.log(typeof numeri); // "object"
console.log(Array.isArray(numeri)); // true
```

- **Array**: collezioni ordinate accessibili tramite indice numerico (liste, serie di dati)
- **Oggetti**: strutture di dati con proprietà nominate significative (entità, configurazioni)

La regola generale è: usare gli **array** per collezioni di dati a cui si accede tramite un indice numerico e gli **oggetti** per strutture di dati a cui si accede tramite nomi di proprietà significativi.

#### Metodi per Aggiungere/Rimuovere Elementi

Esistono metodi specifici per aggiungere o rimuovere elementi all'inizio o alla fine di un array. Questi metodi **modificano l'array originale**.

- **`push()`** → Aggiunge uno o più elementi alla fine dell'array

```javascript
let numeri = [1, 2, 3];
numeri.push(4); // [1, 2, 3, 4]
numeri.push(5, 6); // [1, 2, 3, 4, 5, 6]
```

- **`pop()`** → Rimuove l'ultimo elemento dall'array e lo restituisce

```javascript
let numeri = [1, 2, 3];
let ultimo = numeri.pop(); // ultimo = 3, numeri = [1, 2]
```

- **`unshift()`** → Aggiunge uno o più elementi all'inizio dell'array

```javascript
let numeri = [2, 3];
numeri.unshift(1); // [1, 2, 3]
numeri.unshift(-1, 0); // [-1, 0, 1, 2, 3]
```

- **`shift()`** → Rimuove il primo elemento dall'array e lo restituisce

```javascript
let numeri = [1, 2, 3];
let primo = numeri.shift(); // primo = 1, numeri = [2, 3]
```

- **`splice()`** → Modifica il contenuto di un array rimuovendo, sostituendo o aggiungendo elementi direttamente nell'array originale

```javascript
let numeri = [1, 2, 3, 4, 5];

// Rimuovere 2 elementi a partire dall'indice 1
numeri.splice(1, 2); // [1, 4, 5] (rimuove 2 e 3)

// Aggiungere elementi senza rimuovere
numeri.splice(1, 0, 2, 3); // [1, 2, 3, 4, 5]

// Sostituire elementi
numeri.splice(2, 1, 99); // [1, 2, 99, 4, 5] (sostituisce 3 con 99)
```

#### Metodi di Iterazione e Trasformazione

Questi metodi, spesso chiamati **"higher-order functions"**, permettono di eseguire operazioni su ogni elemento dell'array. Molti di questi metodi **creano un nuovo array** senza modificare l'originale.

- **`forEach()`** → Esegue una funzione per ogni elemento dell'array. **Non restituisce** un nuovo array

```javascript
let numeri = [1, 2, 3];
numeri.forEach(function (numero) {
  console.log(numero * 2); // 2, 4, 6
});
// numeri rimane [1, 2, 3]
```

- **`map()`** → Crea un **nuovo array** contenente i risultati di una funzione applicata a ogni elemento dell'array originale

```javascript
let numeri = [1, 2, 3];
let doppi = numeri.map(function (n) {
  return n * 2;
});
console.log(doppi); // [2, 4, 6]
console.log(numeri); // [1, 2, 3] (originale intatto)
```

- **`filter()`** → Crea un **nuovo array** contenente solo gli elementi che superano un test (una funzione che restituisce `true`)

```javascript
let numeri = [1, 2, 3, 4, 5];
let pari = numeri.filter(function (n) {
  return n % 2 === 0;
});
console.log(pari); // [2, 4]
```

- **`reduce()`** → Applica una funzione a ogni elemento per **"ridurre"** l'array a un singolo valore (es. una somma, un oggetto)

```javascript
let numeri = [1, 2, 3, 4];
let somma = numeri.reduce(function (accumulatore, valore) {
  return accumulatore + valore;
}, 0); // 0 è il valore iniziale
console.log(somma); // 10
```

#### Altri Metodi Utili

- **`slice()`** → Restituisce una **copia superficiale** (shallow copy) di una porzione dell'array in un nuovo array, **senza modificare** l'originale

```javascript
let numeri = [1, 2, 3, 4, 5];
let porzione = numeri.slice(1, 3); // [2, 3] (da indice 1 a 3, escluso)
console.log(numeri); // [1, 2, 3, 4, 5] (originale intatto)
```

- **`includes()`** → Controlla se un array include un certo elemento, restituendo `true` o `false`

```javascript
let frutti = ["mela", "banana", "arancia"];
console.log(frutti.includes("banana")); // true
console.log(frutti.includes("pera")); // false
```

- **`find()`** → Restituisce il **primo elemento** dell'array che soddisfa una condizione

```javascript
let numeri = [5, 12, 8, 130, 44];
let trovato = numeri.find(function (n) {
  return n > 10;
});
console.log(trovato); // 12
```

### 3.8 Funzioni (Functions)

**Tipo**: Nuovo Topic

#### Le Funzioni

Una funzione è un **blocco di codice riutilizzabile**, progettato per eseguire un compito specifico. Permette di organizzare il codice in pezzi logici, evitando di ripetere le stesse istruzioni più volte.

#### Le Funzioni

Una funzione è un **blocco di codice riutilizzabile**, progettato per eseguire un compito specifico. Permette di organizzare il codice in pezzi logici, evitando di ripetere le stesse istruzioni più volte.

**Anatomia di una Funzione**

Una funzione è composta da alcuni elementi chiave:

- **Dichiarazione (declaration)** → Avviene tipicamente usando la parola chiave `function`
- **Nome** → Identifica la funzione
- **Parametri (parameters)** → Variabili tra parentesi `()` che ricevono i valori
- **Corpo (body)** → Codice racchiuso tra parentesi graffe `{}`
- **Return** → Restituisce un valore e termina l'esecuzione

```javascript
/*
 * Anatomia di una funzione
 */

// Dichiarazione di funzione
function saluta(nome) {
  // 'nome' è un parametro
  console.log("Ciao, " + nome + "!");
}

// Funzione con return
function somma(a, b) {
  // 'a' e 'b' sono parametri
  return a + b; // return restituisce il risultato
}

let risultato = somma(5, 3); // 5 e 3 sono argomenti
console.log(risultato); // 8

// Funzione senza return (restituisce undefined)
function log(messaggio) {
  console.log(messaggio);
  // nessun return esplicito
}

let valore = log("Test"); // esegue la funzione
console.log(valore); // undefined

/*
 * Parametri vs Argomenti
 */
function moltiplica(x, y) {
  // x e y sono PARAMETRI (nella definizione)
  return x * y;
}

moltiplica(4, 7); // 4 e 7 sono ARGOMENTI (nella chiamata)

// Più argomenti del previsto: gli extra vengono ignorati
function dueSomma(a, b) {
  return a + b;
}
console.log(dueSomma(1, 2, 3, 4)); // 3 (solo 1 e 2 vengono usati)

// Meno argomenti del previsto: i parametri mancanti sono undefined
function treeSomma(a, b, c) {
  return a + b + c;
}
console.log(treeSomma(1, 2)); // NaN (1 + 2 + undefined = NaN)

// Parametri con valori di default (ES6)
function salutaConDefault(nome = "Ospite") {
  return "Ciao, " + nome + "!";
}
console.log(salutaConDefault()); // "Ciao, Ospite!"
console.log(salutaConDefault("Mario")); // "Ciao, Mario!"
```

I **parametri** sono come delle variabili locali che ricevono i valori (chiamati **argomenti**, arguments) passati alla funzione quando viene eseguita.

L'istruzione `return` permette a una funzione di restituire un valore al codice che l'ha chiamata, terminando la sua esecuzione. Se `return` non è presente, la funzione restituisce implicitamente `undefined`.

```javascript
/*
 * Return in azione
 */

function calcolaArea(larghezza, altezza) {
  let area = larghezza * altezza;
  return area; // restituisce il valore di area
  console.log("Questo non verrà mai eseguito"); // codice dopo return è irraggiungibile
}

let areaRettangolo = calcolaArea(10, 5);
console.log(areaRettangolo); // 50

// Return anticipato per uscire dalla funzione
function verificaEta(eta) {
  if (eta < 18) {
    return "Minorenne"; // esce subito dalla funzione
  }
  if (eta < 65) {
    return "Adulto";
  }
  return "Senior";
}

console.log(verificaEta(15)); // "Minorenne"
console.log(verificaEta(30)); // "Adulto"
console.log(verificaEta(70)); // "Senior"

// Return senza valore
function logIfPositive(num) {
  if (num <= 0) {
    return; // esce senza restituire nulla (undefined)
  }
  console.log("Numero positivo:", num);
}

logIfPositive(-5); // non stampa nulla
logIfPositive(10); // "Numero positivo: 10"
```

#### Funzioni come Oggetti (First-Class Citizens)

Un concetto fondamentale in JavaScript è che le **funzioni sono un tipo speciale di oggetto**. Questo significa che, come qualsiasi altro oggetto, possono essere:

- Assegnate a variabili
- Passate come argomenti ad altre funzioni
- Restituite da altre funzioni
- Dotate di proprietà

L'operatore `typeof` riconosce questa natura speciale restituendo la stringa `"function"`.

```javascript
/*
 * Funzioni come oggetti (first-class citizens)
 */

// Assegnare una funzione a una variabile
const miaSomma = function (a, b) {
  return a + b;
};

console.log(miaSomma(3, 4)); // 7
console.log(typeof miaSomma); // "function"

// Le funzioni possono avere proprietà!
function contatore() {
  contatore.chiamate = (contatore.chiamate || 0) + 1;
  return contatore.chiamate;
}

console.log(contatore()); // 1
console.log(contatore()); // 2
console.log(contatore()); // 3
console.log(contatore.chiamate); // 3 (proprietà della funzione)

// Passare una funzione come argomento
function esegui(operazione, a, b) {
  return operazione(a, b); // chiama la funzione passata
}

function somma(x, y) {
  return x + y;
}

function moltiplica(x, y) {
  return x * y;
}

console.log(esegui(somma, 5, 3)); // 8
console.log(esegui(moltiplica, 5, 3)); // 15

// Restituire una funzione da un'altra funzione
function creaMultiplicatore(fattore) {
  return function (numero) {
    return numero * fattore;
  };
}

let doppio = creaMultiplicatore(2);
let triplo = creaMultiplicatore(3);

console.log(doppio(5)); // 10
console.log(triplo(5)); // 15

/*
 * Array di funzioni
 */
let operazioni = [
  function (x) {
    return x + 10;
  },
  function (x) {
    return x * 2;
  },
  function (x) {
    return x - 5;
  },
];

let numero = 10;
for (let op of operazioni) {
  numero = op(numero);
  console.log(numero);
}
// Output: 20, 40, 35
```

Questa caratteristica rende le funzioni **"cittadini di prima classe"** (first-class citizens) nel linguaggio, conferendo loro un'enorme flessibilità.

#### Chiamare una Funzione

Per eseguire il codice all'interno di una funzione, bisogna **chiamarla** (call o invoke) usando il suo nome seguito dalle parentesi `()`. Se la funzione accetta parametri, gli argomenti vengono passati all'interno delle parentesi.

```javascript
/*
 * Chiamare una funzione
 */

function saluta() {
  console.log("Ciao!");
}

saluta(); // Chiamata della funzione
saluta(); // Può essere chiamata più volte

// Con argomenti
function benvenuto(nome, ora) {
  console.log("Buon" + ora + ", " + nome + "!");
}

benvenuto("Mario", "giorno"); // "Buongiorno, Mario!"
benvenuto("Anna", "asera"); // "Buonasera, Anna!"

// Funzioni annidate (chiamate dentro altre funzioni)
function calcola() {
  function somma(a, b) {
    return a + b;
  }

  function moltiplica(a, b) {
    return a * b;
  }

  let risultato = moltiplica(somma(2, 3), 4);
  return risultato;
}

console.log(calcola()); // 20 ((2+3) * 4)
```

#### Hoisting: Dichiarazione vs. Esecuzione

Il motore JavaScript elabora il codice in due fasi. Durante la prima fase, di **analisi** (parsing), "solleva" (un processo chiamato **hoisting**) le dichiarazioni di funzione in cima al loro contesto. Questo significa che è possibile chiamare una funzione dichiarata con `function` prima che appaia nel codice, senza generare errori.

```javascript
/*
 * Hoisting delle funzioni
 */

// ✅ Funziona! La dichiarazione viene "sollevata"
console.log(quadrato(5)); // 25

function quadrato(n) {
  return n * n;
}

// Questo è possibile perché il motore "vede" il codice così:
// function quadrato(n) { return n * n; }  ← sollevata in cima
// console.log(quadrato(5));

/*
 * Function expression NON vengono sollevate
 */

// ❌ Errore! Cannot access 'cubo' before initialization
// console.log(cubo(3));

const cubo = function (n) {
  return n * n * n;
};

console.log(cubo(3)); // ✅ 27 (solo dopo la dichiarazione)

/*
 * Confronto: function declaration vs function expression
 */

// FUNCTION DECLARATION (viene sollevata)
saluta1(); // ✅ "Ciao da function declaration"

function saluta1() {
  console.log("Ciao da function declaration");
}

// FUNCTION EXPRESSION (NON viene sollevata)
// saluta2(); // ❌ Errore!

const saluta2 = function () {
  console.log("Ciao da function expression");
};

saluta2(); // ✅ "Ciao da function expression"
```

Questo comportamento non si applica alle variabili dichiarate con `let` o `const`, che non possono essere usate prima della loro dichiarazione (Temporal Dead Zone - TDZ).

#### Esecuzione Diretta vs. Indiretta

Esiste una differenza fondamentale tra eseguire una funzione immediatamente e passare un riferimento ad essa per un'esecuzione futura.

- **Esecuzione Diretta** → Usare le parentesi `()` dopo il nome della funzione ne provoca l'esecuzione immediata
- **Esecuzione Indiretta (Passare un Riferimento)** → Fornire solo il nome della funzione, senza parentesi, significa passare un riferimento ad essa

```javascript
/*
 * Esecuzione diretta vs indiretta
 */

function saluta() {
  console.log("Ciao!");
}

// Esecuzione diretta
saluta(); // Esegue immediatamente, stampa "Ciao!"

// Passare un riferimento
let riferimento = saluta; // NON esegue, solo assegna il riferimento
riferimento(); // Ora esegue, stampa "Ciao!"

/*
 * Uso comune: event listeners
 */

// ❌ SBAGLIATO - esegue immediatamente
// button.addEventListener("click", saluta());
// La funzione viene eseguita subito e il risultato (undefined)
// viene passato a addEventListener

// ✅ CORRETTO - passa il riferimento
// button.addEventListener("click", saluta);
// La funzione verrà eseguita quando si verifica il click

/*
 * Esempio pratico con timeout
 */

function mostraMessaggio() {
  console.log("5 secondi sono passati!");
}

// ✅ Passa il riferimento (esegue dopo 5 secondi)
setTimeout(mostraMessaggio, 5000);

// ❌ Esecuzione immediata (sbagliato)
// setTimeout(mostraMessaggio(), 5000);
// La funzione si esegue subito, undefined viene passato a setTimeout

/*
 * Quando serve eseguire con argomenti
 */

function salutaPersona(nome) {
  console.log("Ciao, " + nome + "!");
}

// Soluzione 1: usare una arrow function
setTimeout(() => salutaPersona("Mario"), 2000);

// Soluzione 2: usare una function expression
setTimeout(function () {
  salutaPersona("Luigi");
}, 2000);

// Soluzione 3: usare bind (avanzato)
setTimeout(salutaPersona.bind(null, "Anna"), 2000);
```

Questo è comune nella gestione degli eventi, dove si dice al browser di eseguire una certa funzione solo quando si verifica un evento (es. un click).

#### IIFE (Immediately Invoked Function Expressions)

Una **IIFE** (pronunciata "iffy") è una **Espressione di Funzione Invocata Immediatamente**. È un pattern di design in cui una funzione viene dichiarata e poi eseguita subito dopo la sua creazione.

La sintassi di una IIFE può sembrare insolita a prima vista, ma è molto logica. Si compone di due parti principali:

1. Un'espressione di funzione, tipicamente anonima, avvolta tra parentesi `()`. Le parentesi servono a indicare al motore JavaScript che si tratta di un'espressione e non di una dichiarazione di funzione standard
2. Un secondo paio di parentesi `()` alla fine, che è l'operatore di chiamata che esegue la funzione immediatamente

```javascript
/*
 * Sintassi IIFE
 */

// IIFE base
(function () {
  console.log("Questa funzione si esegue immediatamente!");
})();

// Il concetto è: (espressione di funzione)(chiamata immediata)
//                 ^^^^^^^^^^^^^^^^^^^^^^^^  ^^

// IIFE con nome (opzionale, utile per debug)
(function iife() {
  console.log("IIFE con nome");
})();

// Sintassi alternativa (parentesi di chiamata dentro)
(function () {
  console.log("Sintassi alternativa");
})();

/*
 * Confronto con funzione normale
 */

// Funzione normale nominata
function saluta() {
  console.log("Ciao");
}
saluta(); // chiamata esplicita

// È simile a questo concetto
let saluta2 = function () {
  console.log("Ciao");
};
saluta2(); // chiamata esplicita

// IIFE: dichiarazione + chiamata in un'unica espressione
(function () {
  console.log("Ciao");
})(); // ← immediatamente invocata
```

**Lo Scopo Principale → Creare uno Scope Privato**

Il vantaggio più grande di una IIFE è la sua capacità di creare uno **scope privato**. Poiché ogni funzione in JavaScript crea il proprio scope, tutte le variabili dichiarate all'interno di una IIFE sono confinate al suo interno e non "inquinano" lo scope circostante (globale o di un'altra funzione).

Questo era un pattern fondamentale prima dell'introduzione di `let` e `const` (che hanno lo scope di blocco), quando si usava `var` (che ha lo scope di funzione) e si voleva evitare di creare variabili globali accidentalmente.

```javascript
/*
 * IIFE per scope privato
 */

// ❌ Senza IIFE - variabile globale con var
var contatore = 0;
var incrementa = function () {
  contatore++;
};
console.log(contatore); // 0 (accessibile globalmente)

// ✅ Con IIFE - scope privato
(function () {
  var contatore = 0; // privato, esiste solo dentro la IIFE

  function incrementa() {
    contatore++;
    console.log(contatore);
  }

  incrementa(); // 1
  incrementa(); // 2
})();

// console.log(contatore); // ❌ ReferenceError - non accessibile fuori

/*
 * Evitare conflitti di nomi
 */

// File1.js
(function () {
  var nome = "Mario";
  console.log("File 1:", nome);
})();

// File2.js
(function () {
  var nome = "Luigi"; // Nessun conflitto!
  console.log("File 2:", nome);
})();

/*
 * Pattern Module con IIFE
 */
let modulo = (function () {
  // Variabili private
  let contatore = 0;
  let segreto = "password123";

  // API pubblica (ritornata)
  return {
    incrementa: function () {
      contatore++;
    },
    getValue: function () {
      return contatore;
    },
    // segreto NON è esposto
  };
})();

modulo.incrementa();
modulo.incrementa();
console.log(modulo.getValue()); // 2
console.log(modulo.segreto); // undefined (privato)
```

**IIFE con Parametri e Valori di Ritorno**

Come ogni altra funzione, una IIFE può accettare parametri e restituire un valore. Questo è un modo elegante per inizializzare una variabile o un modulo, eseguendo una logica complessa senza lasciare variabili temporanee nello scope esterno.

```javascript
/*
 * IIFE con parametri
 */

// Passare valori alla IIFE
(function (nome, eta) {
  console.log("Nome:", nome, "Età:", eta);
})("Mario", 30);

// Passare oggetti globali come window, document (pattern comune in jQuery)
(function (global, doc) {
  console.log("Titolo:", doc.title);
  global.miVariabileGlobale = "Valore";
})(window, document);

/*
 * IIFE con return
 */

// Inizializzare una variabile con logica complessa
const risultato = (function () {
  let moltiplicatore = 5;
  let valoreBase = 10;
  return moltiplicatore * valoreBase;
})();

console.log(risultato); // 50
// moltiplicatore e valoreBase non esistono più

// Esempio più complesso: configurazione
const config = (function () {
  let ambiente = "produzione";
  let apiUrl;

  if (ambiente === "sviluppo") {
    apiUrl = "http://localhost:3000/api";
  } else {
    apiUrl = "https://api.production.com";
  }

  return {
    ambiente: ambiente,
    apiUrl: apiUrl,
    version: "1.0.0",
  };
})();

console.log(config.apiUrl); // "https://api.production.com"
// ambiente (variabile temporanea) non è più accessibile

/*
 * IIFE per inizializzazione complessa
 */

const utente = (function () {
  let nome = "Mario Rossi";
  let parti = nome.split(" ");

  return {
    nome: nome,
    iniziali: parti[0][0] + parti[1][0],
    username: (parti[0] + parti[1]).toLowerCase(),
  };
})();

console.log(utente);
// { nome: 'Mario Rossi', iniziali: 'MR', username: 'mariorossi' }

/*
 * Pattern: Default parameters con IIFE
 */

function creaWidget(opzioni) {
  opzioni = (function (opts) {
    // Valori di default
    let defaults = {
      colore: "blu",
      dimensione: "media",
      visibile: true,
    };

    // Merge con opzioni fornite
    return { ...defaults, ...opts };
  })(opzioni || {});

  console.log("Widget creato con:", opzioni);
}

creaWidget(); // usa i default
creaWidget({ colore: "rosso" }); // override solo colore
```

In questo esempio, la IIFE viene eseguita immediatamente, calcola il risultato e lo restituisce. Il valore restituito (50) viene quindi assegnato alla costante `risultato`. Le variabili `moltiplicatore` e `valoreBase` esistono solo durante l'esecuzione della IIFE e poi scompaiono.

**Approfondisci**:

- [[01-fondamenti/funzioni/funzioni]] - Funzioni in JavaScript
- [[01-fondamenti/funzioni/iife]] - IIFE (Immediately Invoked Function Expressions)

### 3.9 Closure (Chiusura)

**Tipo**: Nuovo Topic

La **Closure** (o chiusura) è uno dei concetti più importanti e spesso meno compresi in JavaScript. Si può considerare come la capacità di una funzione di **"ricordare"** e continuare ad accedere al proprio scope (le sue variabili) anche dopo che la funzione ha terminato la sua esecuzione.

Questo meccanismo permette a una **funzione interna** di mantenere un riferimento vivo alle variabili della **funzione esterna** che la contiene.

#### Esempio Base

```javascript
/*
 * Esempio classico di closure
 */

function makeAdder(x) {
  // x è una variabile nello scope di makeAdder

  function add(y) {
    // La funzione interna 'add' ha accesso a 'x'
    return x + y;
  }

  return add; // Restituisce la funzione interna
}

// Creiamo due closure diverse
let plusOne = makeAdder(1); // Crea una closure che "ricorda" x = 1
let plusTen = makeAdder(10); // Crea una closure che "ricorda" x = 10

console.log(plusOne(3)); // 4  (1 + 3)
console.log(plusOne(41)); // 42 (1 + 41)

console.log(plusTen(13)); // 23 (10 + 13)
console.log(plusTen(90)); // 100 (10 + 90)
```

Analizzando il codice:

1. **Quando viene chiamata `makeAdder(1)`**, si ottiene un riferimento alla sua funzione interna `add`, la quale "ricorda" che `x` è `1`. Questo riferimento viene assegnato alla variabile `plusOne`.

2. **Quando viene chiamata `makeAdder(10)`**, si ottiene un altro riferimento alla sua funzione interna `add`, che in questo caso "ricorda" che `x` è `10`. Questo nuovo riferimento viene assegnato a `plusTen`.

3. **Quando si esegue `plusOne(3)`**, la funzione aggiunge `3` (il suo parametro `y`) al valore `1` (la `x` che ha "ricordato"), restituendo `4`.

4. **Quando si esegue `plusTen(13)`**, la funzione aggiunge `13` (il suo `y`) al valore `10` (la `x` che ha "ricordato"), restituendo `23`.

In sostanza, ogni volta che `makeAdder` viene eseguita, viene creato un **nuovo scope** e la funzione `add` interna mantiene un collegamento a quello **specifico scope**.

#### Dati Privati con Closure

Le closure permettono di creare **dati privati** e **funzioni factory** potenti.

```javascript
/*
 * Contatore con dati privati
 */

function creaContatore() {
  let count = 0; // Variabile privata

  return {
    incrementa: function () {
      count++;
      return count;
    },
    decrementa: function () {
      count--;
      return count;
    },
    valore: function () {
      return count;
    },
  };
}

let contatore = creaContatore();

console.log(contatore.incrementa()); // 1
console.log(contatore.incrementa()); // 2
console.log(contatore.incrementa()); // 3
console.log(contatore.decrementa()); // 2
console.log(contatore.valore()); // 2

// ❌ Non possiamo accedere direttamente a 'count'
console.log(contatore.count); // undefined

// Ogni contatore ha il suo scope privato
let contatore2 = creaContatore();
console.log(contatore2.incrementa()); // 1 (indipendente!)
console.log(contatore.valore()); // 2 (non influenzato)
```

#### Closure nei Loop

Un caso comune dove le closure possono causare confusione è all'interno dei loop.

```javascript
/*
 * ❌ Problema comune con var nei loop
 */

function creaFunzioni() {
  let funzioni = [];

  for (var i = 0; i < 3; i++) {
    funzioni.push(function () {
      console.log(i); // Tutte le funzioni condividono lo stesso 'i'
    });
  }

  return funzioni;
}

let funz = creaFunzioni();
funz[0](); // 3 (non 0!)
funz[1](); // 3 (non 1!)
funz[2](); // 3 (non 2!)

// Perché? Tutte le funzioni "ricordano" lo stesso 'i',
// che alla fine del loop ha valore 3
```

**Soluzione con let**:

```javascript
/*
 * ✅ Soluzione: Usare let (block scope)
 */

function creaFunzioniCorretto() {
  let funzioni = [];

  for (let i = 0; i < 3; i++) {
    // let invece di var
    funzioni.push(function () {
      console.log(i); // Ogni iterazione ha il suo 'i'
    });
  }

  return funzioni;
}

let funz2 = creaFunzioniCorretto();
funz2[0](); // 0 ✅
funz2[1](); // 1 ✅
funz2[2](); // 2 ✅
```

**Soluzione con IIFE**:

```javascript
/*
 * ✅ Soluzione: IIFE per creare scope separati
 */

function creaFunzioniIIFE() {
  let funzioni = [];

  for (var i = 0; i < 3; i++) {
    funzioni.push(
      (function (indice) {
        return function () {
          console.log(indice);
        };
      })(i),
    ); // IIFE che cattura il valore corrente di i
  }

  return funzioni;
}

let funz3 = creaFunzioniIIFE();
funz3[0](); // 0 ✅
funz3[1](); // 1 ✅
funz3[2](); // 2 ✅
```

#### Importanza delle Closure

La closure è una delle tecniche più **potenti** e **versatili** della programmazione, e padroneggiarla è fondamentale per uno sviluppatore JavaScript.

Le closure sono alla base di molti pattern avanzati come:

- **Module pattern** (moduli privati)
- **Factory functions** (funzioni fabbrica)
- **Event handlers** (gestori eventi)
- **Callbacks** e programmazione asincrona
- **Currying** e programmazione funzionale

**Approfondisci**:

- [[01-fondamenti/funzioni/closure]] - Closure (Chiusura)

### 3.10 Module Pattern

**Tipo**: Nuovo Topic

L'uso più comune della closure in JavaScript è il **Module Pattern**. Questo pattern permette di definire dettagli implementativi **privati** (variabili e funzioni) che sono nascosti al mondo esterno, e allo stesso tempo di esporre un'**interfaccia pubblica** (public API) che può essere utilizzata per interagire con essi.

È una tecnica fondamentale per l'**incapsulamento** e l'**organizzazione del codice**.

#### Esempio Base

```javascript
/*
 * Module Pattern classico
 */

function User() {
  // Variabili private
  let username;
  let password;

  // Funzione privata
  function doLogin(user, pw) {
    username = user;
    password = pw;

    console.log("Login effettuato per:", username);
    // Password non viene mai esposta
  }

  // API pubblica (ciò che viene esposto)
  let publicAPI = {
    login: doLogin, // Riferimento alla funzione privata
  };

  return publicAPI;
}

// Creiamo un'istanza del modulo
let fred = User();

// Possiamo chiamare il metodo pubblico
fred.login("fred", "12Battery34!");
// Output: "Login effettuato per: fred"

// ❌ Non possiamo accedere alle variabili private
console.log(fred.username); // undefined
console.log(fred.password); // undefined
console.log(fred.doLogin); // undefined
```

#### Come Funziona

Analizziamo il funzionamento passo per passo:

**Scope Esterno** → La funzione `User()` agisce come uno **scope esterno** che contiene le variabili `username` e `password`, e la funzione `doLogin()`. Questi elementi sono **privati** e non possono essere raggiunti direttamente dall'esterno.

**Creazione dell'Istanza** → Eseguendo `User()`, si crea un'**istanza del modulo**. Viene generato un **nuovo scope** e, di conseguenza, una **nuova copia** di tutte le variabili e funzioni interne. L'oggetto restituito, `publicAPI`, viene assegnato alla variabile `fred`. Se si eseguisse di nuovo `User()`, si otterrebbe una nuova istanza **completamente separata** da `fred`.

```javascript
/*
 * Istanze separate
 */

let user1 = User();
let user2 = User();

user1.login("alice", "pass123");
user2.login("bob", "pass456");

// user1 e user2 sono completamente indipendenti
console.log(user1 === user2); // false
```

**Nota** → Si usa `User()` e **NON** `new User()` perché `User` è una semplice funzione che funge da **factory**, non una classe da istanziare. L'uso di `new` in questo contesto sarebbe inappropriato.

**API Pubblica** → L'oggetto `publicAPI` contiene i metodi che si vogliono **rendere pubblici**. In questo caso, ha una sola proprietà, `login`, che è un riferimento alla funzione interna `doLogin()`.

**Il Ruolo della Closure** → Quando la funzione `User()` termina la sua esecuzione, le sue variabili interne (`username`, `password`) **non vengono distrutte**. Esse vengono **"mantenute in vita"** dalla closure creata dalla funzione `doLogin()`. Per questo motivo, quando si chiama `fred.login(...)`, la funzione `doLogin` può ancora accedere e modificare le variabili `username` e `password` definite nel suo scope genitore.

```javascript
/*
 * La closure mantiene vivo lo stato privato
 */

function createWallet() {
  let balance = 0; // Privato

  return {
    deposit: function (amount) {
      balance += amount;
      console.log("Deposito:", amount);
      return balance;
    },
    withdraw: function (amount) {
      if (amount > balance) {
        console.log("Fondi insufficienti");
        return balance;
      }
      balance -= amount;
      console.log("Prelievo:", amount);
      return balance;
    },
    getBalance: function () {
      return balance;
    },
  };
}

let wallet = createWallet();
wallet.deposit(100); // "Deposito: 100"
wallet.withdraw(30); // "Prelievo: 30"
console.log(wallet.getBalance()); // 70

// ❌ Non possiamo manipolare balance direttamente
console.log(wallet.balance); // undefined
wallet.balance = 1000000; // Non ha effetto
console.log(wallet.getBalance()); // 70 (intatto!)
```

#### Module Pattern con IIFE

Una variante comune usa una **IIFE** per creare un modulo **singleton** (istanza unica).

```javascript
/*
 * Module Pattern con IIFE (singleton)
 */

let bankAccount = (function () {
  // Stato privato
  let balance = 0;
  let transactions = [];

  // Funzioni private
  function recordTransaction(type, amount) {
    transactions.push({
      type: type,
      amount: amount,
      date: new Date(),
    });
  }

  // API pubblica
  return {
    deposit: function (amount) {
      balance += amount;
      recordTransaction("deposit", amount);
      return balance;
    },
    withdraw: function (amount) {
      if (amount > balance) {
        console.log("Fondi insufficienti");
        return balance;
      }
      balance -= amount;
      recordTransaction("withdraw", amount);
      return balance;
    },
    getBalance: function () {
      return balance;
    },
    getTransactions: function () {
      // Ritorna una copia per evitare modifiche esterne
      return [...transactions];
    },
  };
})();

// Usiamo il modulo singleton
bankAccount.deposit(500);
bankAccount.withdraw(100);
console.log(bankAccount.getBalance()); // 400
console.log(bankAccount.getTransactions()); // Array con 2 transazioni

// ❌ Non possiamo accedere ai dati privati
console.log(bankAccount.balance); // undefined
console.log(bankAccount.transactions); // undefined
```

#### Vantaggi del Module Pattern

- **Incapsulamento** → Dati privati veramente privati, implementazione nascosta
- **Organizzazione** → Codice strutturato e modulare, chiara separazione tra pubblico e privato
- **Namespace** → Evita inquinamento dello scope globale, riduce conflitti di nomi
- **Manutenibilità** → Modifiche interne senza impatto sul codice esterno, API stabile e ben definita

#### Riepilogo

In sintesi, il **Module Pattern** sfrutta le closure per creare uno **stato privato** (variabili e funzioni nascoste) e un'**interfaccia pubblica** (API esposta). È un concetto chiave per scrivere codice **robusto** e **manutenibile**.

**Approfondisci**:

- [[01-fondamenti/funzioni/module-pattern]] - Module Pattern

### 3.11 L'identificatore this

**Tipo**: Concetto Fondamentale

La parola chiave `this` punta a un **oggetto**, ma l'**oggetto dipende da come la funzione è chiamata** (call-site).

**Equivoco comune**: `this` **NON** è la funzione stessa.

#### Le Quattro Regole del Binding

1. **Default Binding** → `foo()` → `this` = globale (o `undefined` in strict mode)
2. **Implicit Binding** → `obj.foo()` → `this` = `obj`  
   ⚠️ Si perde estraendo il metodo: `let fn = obj.foo; fn();`
3. **Explicit Binding** → `.call(obj)`, `.apply(obj)`, `.bind(obj)` → `this` = `obj`
4. **New Binding** → `new foo()` → `this` = nuovo oggetto vuoto creato

**Ordine di precedenza**: new > explicit > implicit > default

```javascript
function foo() {
  console.log(this.bar);
}

var bar = "global";
var obj = { bar: "obj1", foo: foo };

foo(); // "global" - default
obj.foo(); // "obj1" - implicit
foo.call(obj); // "obj1" - explicit
new foo(); // undefined - new
```

**Approfondisci**:

- [[01-fondamenti/funzioni/this]] - L'identificatore this

### 3.12 Prototipi (Prototypes)

**Tipo**: Concetto Fondamentale

I **prototipi** sono un sistema di **fallback** per le proprietà degli oggetti. Quando una proprietà non viene trovata su un oggetto, JavaScript cerca nella **catena dei prototipi** (prototype chain) fino a trovarla. Questo è chiamato **delega** (delegation).

```javascript
var foo = { a: 42 };
var bar = Object.create(foo); // bar collegato a foo

console.log(bar.a); // 42 (delegato a foo)
console.log(bar.hasOwnProperty("a")); // false
```

#### Classi ES6 e Prototipi

La sintassi `class` di ES6 è **zucchero sintattico** sui prototipi:

```javascript
// ES6
class Person {
  constructor(name) {
    this.name = name;
  }
  greet() {
    console.log("Ciao, sono " + this.name);
  }
}

// Equivalente pre-ES6
function Person(name) {
  this.name = name;
}
Person.prototype.greet = function () {
  console.log("Ciao, sono " + this.name);
};
```

#### Uso Implicito

- **Array**: `.map()`, `.filter()` sono su `Array.prototype`
- **Object**: `.toString()`, `.hasOwnProperty()` sono su `Object.prototype`
- **DOM**: `.addEventListener()` è su `EventTarget.prototype`

#### Perché Sono Importanti

- **Debugging** → Diagnosticare `TypeError: is not a function`
- **Performance** → Metodi condivisi tra istanze (risparmio memoria)
- **Polyfilling** → Estendere prototipi nativi per compatibilità

**Approfondisci**:

- [[01-fondamenti/oggetti/prototypes]] - Prototipi (Prototypes)

---

## 4. Variabili

### 4.1 Dichiarazione Variabili (let, const, var)

**Tipo**: Nuovo Topic

Un programma ha bisogno di "ricordare" dei valori che possono cambiare durante la sua esecuzione. Per fare ciò, si utilizzano le variabili: contenitori simbolici a cui viene assegnato un nome e che possono contenere dati. La funzione primaria delle variabili è gestire lo stato (state) del programma, ovvero tenere traccia dei valori mentre cambiano.

#### Dichiarazione → let, const e var

In JavaScript, le variabili vengono "create" tramite una dichiarazione. Le parole chiave moderne per farlo sono let e const.

- **let** → Dichiara una variabile il cui valore può essere riassegnato e modificato nel tempo.

```javascript
let contatore = 0;
contatore = 1; // OK - il valore può essere riassegnato
```

- **const** → Dichiara una costante, ovvero una variabile il cui valore non può essere riassegnato dopo la sua prima inizializzazione. Se si tenta di farlo, il programma genererà un errore.

```javascript
const PI = 3.14159;
PI = 3; // ❌ Errore! Non si può riassegnare una costante
```

Per convenzione, i nomi delle costanti sono spesso scritti in maiuscolo (UPPER_CASE) per renderle facilmente riconoscibili.

- **var** → Era il modo originale per dichiarare variabili prima dell'introduzione di let e const (in ES6). Oggi il suo uso è sconsigliato a favore di let e const, che offrono un controllo migliore sulla portata (scope) delle variabili e prevengono errori comuni.

```javascript
/*
 * Esempi di dichiarazione e uso delle variabili
 */

// Dichiarazione con let (valore modificabile)
let nome = "Alice";
let eta = 25;
let attivo = true;

// Modifica del valore
nome = "Bob";
eta = 26;
console.log(nome); // "Bob"

// Dichiarazione con const (valore non riassegnabile)
const GIORNI_SETTIMANA = 7;
const MAX_TENTATIVI = 3;
const API_URL = "https://api.example.com";

// GIORNI_SETTIMANA = 8; // ❌ Errore! TypeError: Assignment to constant variable

// Dichiarazione multipla
let x = 10,
  y = 20,
  z = 30;

// Dichiarazione senza inizializzazione
let valore;
console.log(valore); // undefined

// const richiede sempre un'inizializzazione
// const MANCANTE; // ❌ Errore! Missing initializer in const declaration

/*
 * Esempi di gestione dello stato del programma
 */

// Contatore che traccia il numero di click
let numeroClick = 0;

function registraClick() {
  numeroClick = numeroClick + 1;
  console.log("Click numero: " + numeroClick);
}

registraClick(); // "Click numero: 1"
registraClick(); // "Click numero: 2"

// Configurazione dell'applicazione con costanti
const CONFIG = {
  nome_app: "MiaApp",
  versione: "1.0.0",
  debug: true,
};

// Si può modificare il contenuto di un oggetto const
CONFIG.debug = false; // ✅ OK - modifica una proprietà

// Ma non si può riassegnare la variabile
// CONFIG = {}; // ❌ Errore! Assignment to constant variable

/*
 * Differenza tra var, let e const (scope)
 */

// var ha function scope
function esempiVar() {
  if (true) {
    var messaggio = "Ciao"; // var è visibile in tutta la funzione
  }
  console.log(messaggio); // ✅ "Ciao" - var è accessibile
}

// let e const hanno block scope
function esempiLet() {
  if (true) {
    let messaggio = "Ciao"; // let è visibile solo nel blocco if
  }
  // console.log(messaggio); // ❌ Errore! messaggio non è definito
}

// Preferire let e const per codice più sicuro
let contatore_moderno = 0;
const LIMITE_MODERNO = 100;
```

---

### 4.2 Nomi delle Variabili e Identificatori

**Tipo**: Nuovo Topic

La scelta di un buon nome per una variabile o una funzione è cruciale per la leggibilità del codice. In JavaScript, questi nomi devono essere identificatori validi (valid identifiers) e seguire regole precise.

#### Regole per un Identificatore Valido

Le regole sintattiche per un identificatore sono semplici:

- **Carattere Iniziale** → Deve iniziare con una lettera (da a a z, maiuscola o minuscola), un trattino basso (\_) o il simbolo del dollaro ($). Non può iniziare con un numero.

- **Caratteri Successivi** → Dopo il primo carattere, può contenere qualsiasi combinazione di lettere, numeri, trattini bassi o simboli del dollaro.

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

#### Parole Riservate (Reserved Words)

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

#### Convenzioni e Buone Pratiche

Oltre alle regole sintattiche, la comunità JavaScript segue delle convenzioni per scrivere codice più pulito e comprensibile:

- **Nomi Descrittivi** → Scegliere nomi che spieghino chiaramente lo scopo della variabile (es. prezzoUnitario invece di p). Evitare abbreviazioni ambigue.

- **Notazione camelCase** → È la convenzione standard in JavaScript. Si inizia con una lettera minuscola e si usa la maiuscola per l'inizio di ogni parola successiva, senza spazi (es. nomeUtente, calcolaPrezzoFinale).

- **Plurali per le Collezioni** → Usare un nome plurale per gli array o altre collezioni di dati, per indicare che contengono più elementi (es. utenti, prodotti).

```javascript
/*
 * Esempi di convenzioni e buone pratiche
 */

// ❌ Nomi poco descrittivi
let p = 10;
let q = 5;
let t = p * q;

// ✅ Nomi descrittivi
let prezzoUnitario = 10;
let quantita = 5;
let totale = prezzoUnitario * quantita;

// ✅ camelCase per variabili e funzioni
let nomeUtente = "Mario";
let numeroTelefono = "123456789";
let dataInizioContratto = "2026-01-01";

function calcolaPrezzoFinale(prezzo, sconto) {
  return prezzo - (prezzo * sconto) / 100;
}

// ✅ PascalCase per costruttori e classi
function Persona(nome, cognome) {
  this.nome = nome;
  this.cognome = cognome;
}

class UtenteRegistrato {
  constructor(email) {
    this.email = email;
  }
}

// ✅ UPPER_CASE per costanti globali
const MAX_TENTATIVI = 3;
const API_BASE_URL = "https://api.example.com";
const TIMEOUT_MS = 5000;

// ✅ Plurali per collezioni
let utente = { nome: "Mario", eta: 30 }; // singolo elemento
let utenti = [
  // collezione
  { nome: "Mario", eta: 30 },
  { nome: "Luigi", eta: 25 },
];

let prodotto = { nome: "Laptop", prezzo: 999 }; // singolo elemento
let prodotti = [
  // collezione
  { nome: "Laptop", prezzo: 999 },
  { nome: "Mouse", prezzo: 29 },
];

// ✅ Prefissi comuni per booleani
let isAttivo = true;
let hasPermessi = false;
let canModificare = true;
let shouldAggiornare = false;

// ✅ Underscore per "privati" (convenzione, non enforcement)
let _variabilePrivata = "Non dovrebbe essere usata direttamente";
let _calcoloInterno = function () {
  return 42;
};

/*
 * Esempio completo con buone pratiche
 */
class GestoreCarrello {
  constructor() {
    this._articoli = []; // array privato
    this.MAX_ARTICOLI = 100; // costante pubblica
  }

  aggiungiArticolo(nomeArticolo, prezzoUnitario, quantita) {
    if (this._articoli.length >= this.MAX_ARTICOLI) {
      throw new Error("Carrello pieno");
    }

    const nuovoArticolo = {
      nome: nomeArticolo,
      prezzo: prezzoUnitario,
      quantita: quantita,
      totale: prezzoUnitario * quantita,
    };

    this._articoli.push(nuovoArticolo);
  }

  calcolaTotaleCarrello() {
    let totaleComplessivo = 0;

    for (let articolo of this._articoli) {
      totaleComplessivo += articolo.totale;
    }

    return totaleComplessivo;
  }
}

const carrelloAcquisti = new GestoreCarrello();
carrelloAcquisti.aggiungiArticolo("Laptop", 999, 1);
carrelloAcquisti.aggiungiArticolo("Mouse", 29, 2);

console.log("Totale:", carrelloAcquisti.calcolaTotaleCarrello()); // 1057
```

---

### 4.3 Hoisting delle Variabili

**Tipo**: Nuovo Topic

L'hoisting (letteralmente "sollevamento") è un meccanismo di JavaScript che riguarda il modo in cui le dichiarazioni di variabili vengono processate dal motore del linguaggio. Durante la fase di compilazione, che precede l'esecuzione, è come se le dichiarazioni venissero concettualmente "sollevate" in cima al loro scope di appartenenza.

Tuttavia, il comportamento dell'hoisting cambia radicalmente a seconda della parola chiave usata per la dichiarazione: var, let o const.

#### Hoisting con var

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

#### Hoisting con let e const e la Temporal Dead Zone (TDZ)

Anche le variabili dichiarate con let e const vengono "sollevate", ma si comportano in modo molto più sicuro e prevedibile grazie alla Temporal Dead Zone (TDZ).

La TDZ è una "zona temporale" che inizia all'inizio dello scope della variabile e termina nel punto esatto in cui la variabile viene dichiarata nel codice. Durante questo intervallo, la variabile esiste ma è in uno stato inaccessibile. Qualsiasi tentativo di leggere o scrivere la variabile all'interno della TDZ provocherà un ReferenceError.

##### Comportamento di let

```javascript
console.log(eta); // ❌ ReferenceError: Cannot access 'eta' before initialization
let eta = 25;
console.log(eta); // 25
```

##### Comportamento di const

const segue le stesse regole di let per quanto riguarda la TDZ. La differenza principale è che una const deve essere inizializzata contestualmente alla sua dichiarazione e non può essere riassegnata.

```javascript
console.log(PI); // ❌ ReferenceError: Cannot access 'PI' before initialization
const PI = 3.14159;
console.log(PI); // 3.14159
```

In sintesi, la TDZ impedisce di usare una variabile prima che sia stata dichiarata, eliminando la fonte di errori tipica dell'hoisting di var e promuovendo un codice più pulito e robusto.

```javascript
/*
 * Esempi completi di hoisting con var, let e const
 */

// ===== VAR HOISTING =====
function esempioVar() {
  console.log("Inizio funzione");
  console.log(messaggio); // undefined - NON un errore!

  var messaggio = "Ciao da var";

  console.log(messaggio); // "Ciao da var"
}

// Il codice sopra viene interpretato così:
function esempioVarInterpretato() {
  var messaggio; // dichiarazione sollevata in cima

  console.log("Inizio funzione");
  console.log(messaggio); // undefined

  messaggio = "Ciao da var"; // assegnazione

  console.log(messaggio); // "Ciao da var"
}

// ===== LET/CONST E TEMPORAL DEAD ZONE =====
function esempioLet() {
  console.log("Inizio funzione");

  // ⚠️ TDZ inizia qui - 'nome' esiste ma non è accessibile

  // console.log(nome); // ❌ ReferenceError!

  let nome = "Mario"; // TDZ finisce qui

  console.log(nome); // ✅ "Mario"
}

function esempioConst() {
  // ⚠️ TDZ per LIMITE

  // console.log(LIMITE); // ❌ ReferenceError!

  const LIMITE = 100; // TDZ finisce qui

  console.log(LIMITE); // ✅ 100

  // LIMITE = 200; // ❌ TypeError: Assignment to constant variable
}

/*
 * Hoisting in blocchi di codice
 */
function confrontoScope() {
  // VAR - function scope
  if (true) {
    var x = 10;
  }
  console.log(x); // ✅ 10 - var è accessibile fuori dal blocco

  // LET - block scope
  if (true) {
    let y = 20;
  }
  // console.log(y); // ❌ ReferenceError - let ha block scope
}

/*
 * Esempio pratico: loop con var vs let
 */

// Problema comune con var
for (var i = 0; i < 3; i++) {
  setTimeout(function () {
    console.log("var i:", i); // Stampa 3, 3, 3
  }, 100);
}
// i è ancora accessibile qui!
console.log("Dopo loop var:", i); // 3

// Soluzione con let
for (let j = 0; j < 3; j++) {
  setTimeout(function () {
    console.log("let j:", j); // Stampa 0, 1, 2 (corretto!)
  }, 100);
}
// console.log(j); // ❌ ReferenceError - j non è definito fuori dal loop

/*
 * Hoisting di funzioni vs variabili
 */

// Le funzioni vengono completamente "sollevate"
saluta(); // ✅ "Ciao!" - funziona!

function saluta() {
  console.log("Ciao!");
}

// Le function expression seguono le regole delle variabili
// salutaConVar(); // ❌ TypeError: salutaConVar is not a function
var salutaConVar = function () {
  console.log("Ciao da var");
};

// salutaConLet(); // ❌ ReferenceError: Cannot access before initialization
let salutaConLet = function () {
  console.log("Ciao da let");
};

/*
 * Best practice: dichiarare sempre all'inizio dello scope
 */
function buonaPratica() {
  // Dichiarare tutte le variabili all'inizio
  let nome = "Mario";
  let eta = 30;
  const SCONTO = 0.1;

  // Poi usarle
  console.log(nome, eta, SCONTO);
}
```

### 4.4 Scope (Ambito)

**Tipo**: Nuovo Topic

Uno dei paradigmi fondamentali di quasi tutti i linguaggi di programmazione è la capacità di **memorizzare valori in variabili**, per poi recuperarli o modificarli in un secondo momento. Questa capacità di gestire i valori nelle variabili è ciò che conferisce a un programma uno **stato** (state). Senza questo concetto, un programma potrebbe eseguire solo compiti molto limitati e poco interessanti.

L'introduzione delle variabili in un programma solleva però delle **domande cruciali**: dove "vivono" queste variabili? In altre parole, dove vengono memorizzate? E, soprattutto, come fa il programma a trovarle quando ne ha bisogno?

Queste domande evidenziano la necessità di un insieme di regole ben definite, e questo **insieme di regole prende il nome di Scope** (ambito).

#### Cos'è lo Scope

In programmazione, lo **scope** (tecnicamente **lexical scope** o ambito lessicale) definisce il **contesto in cui una variabile è "visibile"** e quindi accessibile. Si può pensare allo scope come all'inventario di un negozio: un commesso può vendere solo i prodotti presenti nel suo magazzino, non quelli di un altro negozio. Allo stesso modo, il codice può accedere solo alle variabili definite nel suo scope o in uno scope esterno (un "magazzino" più grande che lo contiene).

```javascript
function negozioA() {
  let prodottoA = "Laptop";
  console.log(prodottoA); // ✅ Accessibile (stesso scope)
  // console.log(prodottoB);  // ❌ Non accessibile (scope diverso)
}

function negozioB() {
  let prodottoB = "Mouse";
  console.log(prodottoB); // ✅ Accessibile
}
```

**Concetto chiave**: Lo scope determina quali variabili sono accessibili in un determinato punto del codice.

#### Metafora: I Tre Attori

Per comprendere a fondo il concetto di Scope, è utile immaginarlo come il risultato di una **conversazione tra tre attori principali** che collaborano per elaborare un programma JavaScript. Ognuno ha un ruolo ben preciso.

Il "cast" di questi personaggi è il seguente:

- **Engine (Motore)** → È il **responsabile principale** dell'intero processo. Gestisce la compilazione e l'esecuzione del codice JavaScript dall'inizio alla fine. Potremmo vederlo come il "capo" che coordina tutte le operazioni.

- **Compiler (Compilatore)** → È uno stretto **collaboratore dell'Engine**. Si occupa di tutto il lavoro "sporco" di analizzare il codice (parsing) e generare la versione eseguibile (code-generation), come discusso in precedenza nella sezione sulla compilazione.

- **Scope** → È un altro **amico dell'Engine**. Il suo compito è quello di **collezionare e mantenere una lista** di tutte le variabili (o più in generale, gli "identificatori") che sono state dichiarate nel programma. Inoltre, applica un **insieme rigoroso di regole** per stabilire come e dove queste variabili siano accessibili dal codice in esecuzione in un dato momento. È in pratica il "guardiano" delle variabili.

```javascript
// Esempio di conversazione tra gli attori
let nome = "Mario"; // Compiler: "Scope, ho trovato 'nome', registrala!"
// Scope: "Ok, registrata nello scope globale"

console.log(nome); // Engine: "Scope, hai una variabile chiamata 'nome'?"
// Scope: "Sì, eccola: 'Mario'"
```

**Principio fondamentale**: Per capire veramente come funziona JavaScript, è necessario iniziare a pensare come pensano l'Engine e i suoi collaboratori, ponendosi le stesse domande che si pongono loro durante l'elaborazione del codice.

#### Scope Globale vs Scope Locale

In JavaScript, esistono principalmente **due tipi di scope**:

- **Scope Globale (Global Scope)** → Una variabile dichiarata al di fuori di qualsiasi funzione si trova nello **scope globale**. È accessibile da qualsiasi punto del programma, sia all'interno che all'esterno delle funzioni.

- **Scope Locale (Local Scope)** → Ogni funzione crea il proprio **scope locale**. Una variabile dichiarata al suo interno è accessibile solo all'interno di quella funzione.

```javascript
// Scope Globale
let variabileGlobale = "Accessibile ovunque";

function miaFunzione() {
  // Scope Locale (funzione)
  let variabileLocale = "Accessibile solo qui";

  console.log(variabileGlobale); // ✅ Può accedere allo scope esterno
  console.log(variabileLocale); // ✅ Può accedere al proprio scope
}

miaFunzione();
// console.log(variabileLocale);  // ❌ Errore! Fuori scope
console.log(variabileGlobale); // ✅ Scope globale accessibile
```

**Regola fondamentale**: Il codice interno può accedere allo scope esterno, ma l'esterno **non può** accedere allo scope interno.

```javascript
let globale = 100;

function esempio() {
  let locale = 50;
  console.log(globale); // ✅ 100 (accede allo scope globale)
  console.log(locale); // ✅ 50 (accede allo scope locale)
}

esempio();
console.log(globale); // ✅ 100
// console.log(locale);  // ❌ ReferenceError: locale is not defined
```

#### Scope Annidati e Catena degli Scope

Gli scope possono essere **annidati** l'uno dentro l'altro. Le regole dello **scope lessicale** stabiliscono che il codice in uno scope più interno può accedere alle variabili degli scope più esterni, ma **non viceversa**. Questo meccanismo, che permette di "risalire" gli scope alla ricerca di una variabile, è chiamato **catena degli scope** (scope chain).

```javascript
let a = "globale";

function esterna() {
  let b = "esterna";

  function interna() {
    let c = "interna";

    // interna può accedere a tutte le variabili degli scope esterni
    console.log(a); // ✅ "globale"
    console.log(b); // ✅ "esterna"
    console.log(c); // ✅ "interna"
  }

  interna();
  console.log(a); // ✅ "globale"
  console.log(b); // ✅ "esterna"
  // console.log(c);  // ❌ ReferenceError: c is not defined
}

esterna();
console.log(a); // ✅ "globale"
// console.log(b);  // ❌ ReferenceError: b is not defined
// console.log(c);  // ❌ ReferenceError: c is not defined
```

In questo esempio, la funzione `interna` può "vedere" la variabile `a` perché si trova in uno scope esterno, ma `esterna` non può vedere `c`, che è confinata localmente all'interno di `interna`.

**Importante**: Se si tenta di accedere a una variabile in uno scope dove non è disponibile, si ottiene un **ReferenceError**.

```javascript
function test() {
  console.log(variabileInesistente); // ❌ ReferenceError
}
```

La **scope chain** funziona come una ricerca a "risalita": quando JavaScript cerca una variabile, parte dallo scope corrente e, se non la trova, sale di livello fino allo scope globale. Se non la trova nemmeno lì, genera un errore.

#### Il Pericolo delle Variabili Globali Accidentali

Un comportamento **pericoloso** di JavaScript (in modalità non-stretta) si verifica quando si assegna un valore a una variabile che **non è stata formalmente dichiarata** con `var`, `let` o `const`. In questo caso, JavaScript risale la catena degli scope fino in cima e, non trovando alcuna dichiarazione, **crea automaticamente una nuova variabile nello scope globale**.

```javascript
function esempio() {
  x = 10; // ❌ Nessuna dichiarazione (var/let/const)
  // JavaScript risale la scope chain fino in cima
  // Non trova 'x' dichiarata da nessuna parte
  // Crea AUTOMATICAMENTE 'x' nello scope globale
}

esempio();
console.log(x); // 10 (variabile globale accidentale!)
```

Questa è considerata una **pessima pratica** perché "inquina" lo scope globale e può portare a **bug difficili da tracciare**, dove parti diverse del codice modificano involontariamente la stessa variabile globale.

```javascript
let x = 100; // Variabile globale intenzionale

function funzioneA() {
  x = 200; // ✅ OK, modifica x globale (intenzionale)
}

function funzioneB() {
  y = 50; // ❌ Crea y globale (accidentale!)
}

funzioneA();
console.log(x); // 200

funzioneB();
console.log(y); // 50 (variabile globale accidentale)
```

La **regola fondamentale** è: **dichiara sempre formalmente le tue variabili** con `let`, `const` o `var`. L'uso dello **"strict mode"** (`"use strict"`, che vedremo più avanti) aiuta a prevenire questo problema, trasformando questi casi in errori.

```javascript
"use strict";

function test() {
  x = 10; // ❌ ReferenceError: x is not defined
  // Strict mode impedisce la creazione automatica
}

// Soluzione corretta
function testCorretto() {
  let x = 10; // ✅ Dichiarazione esplicita
}
```

#### Block Scope con let e const

Mentre `var` crea uno **scope a livello di funzione**, le parole chiave moderne `let` e `const` introducono il concetto di **Block Scope**. Una variabile dichiarata con `let` o `const` è **confinata al blocco di codice `{...}`** in cui è definita (ad esempio un `if`, un ciclo `for` o anche un blocco autonomo).

```javascript
if (true) {
  let bloccoScoped = "Visibile solo nel blocco";
  const COSTANTE = 42;
  var funzioneScoped = "Visibile anche fuori";
}

// console.log(bloccoScoped);  // ❌ Errore con let
// console.log(COSTANTE);      // ❌ Errore con const
console.log(funzioneScoped); // ✅ var ignora block scope
```

- **`let` e `const`** → Rispettano il **block scope** (blocchi `{}`)
- **`var`** → Rispetta solo il **function scope**, ignora i blocchi

```javascript
function esempio() {
  if (true) {
    let x = 10;
    var y = 20;
  }

  // console.log(x);  // ❌ ReferenceError (fuori block scope)
  console.log(y); // ✅ 20 (var ignora blocchi, scope di funzione)
}

// Blocco autonomo
{
  let messaggio = "Solo qui";
  const PI = 3.14;
  console.log(messaggio); // ✅ Accessibile
}
// console.log(messaggio);  // ❌ ReferenceError
```

Block scope permette un **controllo più preciso** sulla visibilità delle variabili, rendendo il codice più sicuro e prevedibile.

#### Shadowing (Variabili Ombra)

Lo **shadowing** si verifica quando una variabile dichiarata in uno **scope locale** ha lo stesso nome di una variabile in uno **scope più esterno**. In questo caso, la variabile locale **"nasconde"** o **"mette in ombra"** (shadows) quella esterna. All'interno dello scope locale, qualsiasi riferimento a quel nome di variabile utilizzerà la **versione locale**.

```javascript
let x = 10; // Scope globale

function esempio() {
  let x = 20; // Scope locale, "shadows" la x globale

  console.log(x); // 20 (usa la x locale)
}

esempio();
console.log(x); // 10 (usa la x globale, non modificata)
```

**Shadowing annidato** - Lo shadowing può verificarsi a più livelli:

```javascript
let nome = "Globale";

function esterna() {
  let nome = "Esterna"; // Shadows globale
  console.log(nome); // "Esterna"

  function interna() {
    let nome = "Interna"; // Shadows esterna (e globale)
    console.log(nome); // "Interna"
  }

  interna();
  console.log(nome); // "Esterna" (non modificata)
}

esterna();
console.log(nome); // "Globale" (non modificata)
```

**Shadowing con blocchi** - Anche i blocchi `{}` con `let`/`const` creano shadowing:

```javascript
let x = 100;

if (true) {
  let x = 200; // Shadows x esterna
  console.log(x); // 200
}

console.log(x); // 100
```

**Importante**: Non puoi ri-dichiarare la stessa variabile con `let`/`const` nello stesso scope, ma puoi farlo in scope diversi (shadowing).

```javascript
let y = 10;
// let y = 20;  // ❌ SyntaxError: già dichiarata nello stesso scope

{
  let y = 20; // ✅ OK, diverso scope (shadowing)
  console.log(y); // 20
}
console.log(y); // 10
```

---

## 5. Operatori

**Tipo**: Nuovo Topic

Gli operatori (operators) sono simboli speciali che eseguono azioni su variabili e valori. Permettono di effettuare calcoli, assegnare valori, confrontare dati e combinare condizioni logiche.

### Operatori di Assegnamento (Assignment)

L'operatore di assegnamento base è `=`. La sua funzione è memorizzare il valore dell'espressione a destra all'interno della variabile a sinistra.

Esistono anche gli operatori di assegnamento composto (compound assignment), come `+=` o `*=`, che combinano un'operazione matematica con un assegnamento, rendendo il codice più sintetico.

```javascript
/*
 * Operatori di assegnamento
 */

// Assegnamento base
let x = 10;

// Assegnamento composto
let punteggio = 100;
punteggio += 50; // equivale a: punteggio = punteggio + 50
console.log(punteggio); // 150

let quantita = 20;
quantita *= 3; // equivale a: quantita = quantita * 3
console.log(quantita); // 60

let valore = 100;
valore -= 25; // valore = valore - 25
console.log(valore); // 75

let dividendo = 50;
dividendo /= 5; // dividendo = dividendo / 5
console.log(dividendo); // 10
```

### Operatori Matematici (Arithmetic)

Eseguono le classiche operazioni aritmetiche. I principali sono:

- `+` (Addizione e concatenazione di stringhe)
- `-` (Sottrazione)
- `*` (Moltiplicazione)
- `/` (Divisione)
- `%` (Resto o remainder)
- `**` (Esponenziazione)
- `++` (Incremento di 1) e `--` (Decremento di 1)

```javascript
/*
 * Operatori matematici
 */

// Addizione e concatenazione
let somma = 5 + 3; // 8
let testo = "Hello" + " " + "World"; // "Hello World"
let mix = "Il numero è " + 42; // "Il numero è 42"

// Sottrazione, moltiplicazione, divisione
let differenza = 10 - 4; // 6
let prodotto = 6 * 7; // 42
let quoziente = 20 / 4; // 5

// Resto (remainder)
let resto = 17 % 5; // 2 (17 diviso 5 fa 3 con resto 2)
let pari = 10 % 2; // 0 (numero pari)
let dispari = 11 % 2; // 1 (numero dispari)

// Esponenziazione
let potenza = 2 ** 3; // 8 (2 elevato alla 3)
let quadrato = 5 ** 2; // 25

// Incremento e decremento
let contatore = 0;
contatore++; // contatore diventa 1
contatore++; // contatore diventa 2
console.log(contatore); // 2

let countdown = 10;
countdown--; // countdown diventa 9
console.log(countdown); // 9

// Pre-incremento vs Post-incremento
let a = 5;
let b = a++; // b = 5, poi a diventa 6
console.log(a, b); // 6, 5

let c = 5;
let d = ++c; // c diventa 6, poi d = 6
console.log(c, d); // 6, 6
```

### Operatori di Confronto ed Uguaglianza (Comparison & Equality)

Gli operatori di confronto sono essenziali per la logica condizionale, poiché restituiscono un valore booleano (true o false) basato sulla relazione tra due valori. Si dividono principalmente in operatori di uguaglianza e di disuguaglianza (o relazionali).

#### Uguaglianza → == vs ===

La differenza tra `==` (uguaglianza lasca) e `===` (uguaglianza stretta) è uno dei punti più discussi in JavaScript.

- **=== (Uguaglianza Stretta)** → Questo operatore si comporta in modo molto prevedibile. Confronta i due valori e restituisce true solo se sono dello stesso tipo e hanno lo stesso valore. Non esegue alcuna conversione di tipo. Per questa ragione, è spesso la scelta raccomandata per evitare sorprese.

- **== (Uguaglianza Lasca)** → Questo operatore è più flessibile. Se i due valori confrontati sono di tipo diverso, tenta di convertirne uno o entrambi (un processo chiamato coercizione) per farli corrispondere prima di effettuare il confronto.

Sebbene molti sviluppatori evitino `==` per la sua presunta imprevedibilità, se compreso, è uno strumento potente. Ecco delle semplici regole per decidere quando usarlo in sicurezza:

- Evitare `==` se uno dei due valori potrebbe essere `true` o `false`.
- Evitare `==` se uno dei due valori potrebbe essere `0`, `""` (stringa vuota) o `[]` (array vuoto).
- In tutti gli altri casi, usare `==` è sicuro e può migliorare la leggibilità del codice.

Gli operatori di non uguaglianza, `!=` (lasca) e `!==` (stretta), seguono le stesse identiche logiche dei loro corrispettivi.

```javascript
/*
 * Confronto: == vs ===
 */

// === Uguaglianza stretta (stesso tipo e valore)
console.log(5 === 5); // true
console.log(5 === "5"); // false (numero vs stringa)
console.log(true === 1); // false (booleano vs numero)
console.log(null === undefined); // false (tipi diversi)

// == Uguaglianza lasca (con coercizione)
console.log(5 == "5"); // true (stringa convertita a numero)
console.log(true == 1); // true (true convertito a 1)
console.log(false == 0); // true (false convertito a 0)
console.log(null == undefined); // true (caso speciale)
console.log("" == 0); // true (stringa vuota convertita a 0)

// Quando == può essere ingannevole
console.log(false == ""); // true
console.log(false == []); // true
console.log("" == 0); // true
console.log(0 == []); // true
// ❌ Evitare == con: true, false, 0, "", []

// Casi sicuri per ==
let input = "42";
if (input == 42) {
  // Sicuro: confronto stringa/numero
  console.log("Input valido");
}

let valore = null;
if (valore == null) {
  // Sicuro: cattura sia null che undefined
  console.log("Valore non definito");
}

// Operatori di non uguaglianza
console.log(5 !== "5"); // true (tipi diversi)
console.log(5 != "5"); // false (valori uguali dopo coercizione)
```

#### Confronto tra Oggetti e Array

Quando si confrontano valori non primitivi come oggetti o array, sia `==` che `===` si comportano allo stesso modo: controllano se le due variabili puntano allo stesso riferimento in memoria, non se il loro contenuto è identico.

```javascript
/*
 * Confronto di oggetti e array
 */

// Array con stesso contenuto ma riferimenti diversi
let arr1 = [1, 2, 3];
let arr2 = [1, 2, 3];
let arr3 = arr1; // stesso riferimento di arr1

console.log(arr1 === arr2); // false (riferimenti diversi)
console.log(arr1 === arr3); // true (stesso riferimento)
console.log(arr1 == arr2); // false (riferimenti diversi anche con ==)

// Oggetti con stesso contenuto ma riferimenti diversi
let obj1 = { nome: "Mario" };
let obj2 = { nome: "Mario" };
let obj3 = obj1; // stesso riferimento di obj1

console.log(obj1 === obj2); // false (riferimenti diversi)
console.log(obj1 === obj3); // true (stesso riferimento)

/*
 * Per confrontare il contenuto, serve un confronto profondo
 */
function arrayUguali(a, b) {
  if (a.length !== b.length) return false;
  for (let i = 0; i < a.length; i++) {
    if (a[i] !== b[i]) return false;
  }
  return true;
}

console.log(arrayUguali([1, 2, 3], [1, 2, 3])); // true
```

#### Disuguaglianza (Operatori Relazionali)

Gli operatori `<`, `>`, `<=` e `>=` vengono usati per i confronti di disuguaglianza. A differenza degli operatori di uguaglianza, non esiste una versione "stretta" che eviti la coercizione.

Il loro comportamento dipende dal tipo di valori confrontati:

- Se entrambi i valori sono stringhe, il confronto avviene in ordine alfabetico (lessicografico).
- In quasi tutti gli altri casi, JavaScript tenta di convertire entrambi i valori in numeri prima di confrontarli.

Un'insidia comune si presenta quando un valore non può essere convertito in un numero valido, risultando in NaN (Not a Number). Per specifica, NaN non è né maggiore, né minore, né uguale a nessun altro valore.

```javascript
/*
 * Operatori relazionali
 */

// Confronto numerico
console.log(10 > 5); // true
console.log(3 <= 3); // true
console.log(7 < 2); // false

// Confronto di stringhe (lessicografico)
console.log("apple" < "banana"); // true
console.log("zebra" > "aardvark"); // true
console.log("10" < "9"); // true (confronto carattere per carattere: "1" < "9")

// Coercizione numerica
console.log("42" > 10); // true (stringa "42" convertita a numero 42)
console.log("100" < 50); // false (stringa "100" → numero 100)

// Problemi con NaN
let risultato = "ciao" - 5; // NaN (operazione non valida)
console.log(risultato > 0); // false
console.log(risultato < 0); // false
console.log(risultato == risultato); // false
console.log(isNaN(risultato)); // true ✅ modo corretto per verificare NaN

// Altri casi speciali
console.log(null > 0); // false
console.log(null == 0); // false
console.log(null >= 0); // true (⚠️ null convertito a 0)

console.log(undefined > 0); // false
console.log(undefined < 0); // false
console.log(undefined == 0); // false
```

### Operatori Logici (Logical)

Combinano espressioni booleane.

- `&&` (AND) → true solo se entrambe le condizioni sono vere.
- `||` (OR) → true se almeno una condizione è vera.
- `!` (NOT) → Inverte un valore booleano (true diventa false e viceversa).

Questi operatori usano il cortocircuito (short-circuit evaluation): `&&` si ferma se la prima condizione è falsa, mentre `||` si ferma se la prima è vera. Questo permette di scrivere codice più efficiente e conciso.

```javascript
/*
 * Operatori logici
 */

// && (AND logico)
console.log(true && true); // true
console.log(true && false); // false
console.log(false && true); // false

let eta = 25;
let haPatente = true;
if (eta >= 18 && haPatente) {
  console.log("Può guidare");
}

// || (OR logico)
console.log(true || false); // true
console.log(false || true); // true
console.log(false || false); // false

let isWeekend = true;
let isFestivo = false;
if (isWeekend || isFestivo) {
  console.log("Non si lavora");
}

// ! (NOT logico)
console.log(!true); // false
console.log(!false); // true

let piove = false;
if (!piove) {
  console.log("Si può uscire senza ombrello");
}

// Short-circuit evaluation
let utente = null;
let nomeUtente = utente && utente.nome; // null (si ferma a utente)
console.log(nomeUtente); // null

let valoreDefault = "" || "Valore predefinito"; // "Valore predefinito"
console.log(valoreDefault);

// Combinazioni complesse
let temperatura = 25;
let soleggiato = true;
let weekend = true;

if ((temperatura > 20 && soleggiato) || weekend) {
  console.log("È una bella giornata!");
}

// Uso pratico: prevenire errori
function saluta(persona) {
  // Evita errore se persona è null/undefined
  let nome = persona && persona.nome;
  console.log("Ciao " + (nome || "ospite"));
}

saluta({ nome: "Mario" }); // "Ciao Mario"
saluta(null); // "Ciao ospite"
```

### Operatore Condizionale (Ternario)

L'operatore ternario (`? :`) è una scorciatoia per un'istruzione if-else. La sua sintassi è:

`condizione ? valore_se_vero : valore_se_falso`

```javascript
/*
 * Operatore ternario
 */

// Esempio base
let eta = 20;
let tipo = eta >= 18 ? "adulto" : "minore";
console.log(tipo); // "adulto"

// Equivalente a:
let tipoAlt;
if (eta >= 18) {
  tipoAlt = "adulto";
} else {
  tipoAlt = "minore";
}

// Uso in espressioni
let punteggio = 85;
console.log("Hai " + (punteggio >= 60 ? "superato" : "fallito") + " l'esame");

// Ternari annidati (usare con cautela)
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

// Uso pratico con valori di default
function saluta(nome) {
  let messaggio = nome ? "Ciao " + nome : "Ciao ospite";
  return messaggio;
}

console.log(saluta("Mario")); // "Ciao Mario"
console.log(saluta()); // "Ciao ospite"

// In assegnamenti condizionali
let isPremium = true;
let sconto = isPremium ? 0.2 : 0.1;
console.log("Sconto applicato: " + sconto * 100 + "%");
```

### Operatore di Coalescenza Nullish (??)

Questo operatore restituisce il valore a destra solo se quello a sinistra è `null` o `undefined`. È perfetto per assegnare valori di default, perché a differenza di `||`, non scarta valori falsy validi come `0` o una stringa vuota `""`.

```javascript
/*
 * Operatore di Coalescenza Nullish (??)
 */

// Problema con || (scarta valori falsy validi)
let contatore = 0;
let valore1 = contatore || 10; // 10 (0 è falsy, usa il default)
console.log(valore1); // 10 ❌ Ma 0 è un valore valido!

// Soluzione con ?? (controlla solo null/undefined)
let valore2 = contatore ?? 10; // 0 (0 non è null/undefined)
console.log(valore2); // 0 ✅ Corretto!

// Altri casi
let testo = "";
console.log(testo || "default"); // "default" (stringa vuota è falsy)
console.log(testo ?? "default"); // "" (stringa vuota è valida)

let numero = 0;
console.log(numero || 100); // 100
console.log(numero ?? 100); // 0

let valoreMancante = null;
console.log(valoreMancante ?? "N/D"); // "N/D"

let valoreInesistente = undefined;
console.log(valoreInesistente ?? "Non definito"); // "Non definito"

// Uso pratico in funzioni
function configura(opzioni) {
  // Permette timeout: 0 (valore valido)
  let timeout = opzioni.timeout ?? 3000;
  let maxRetry = opzioni.maxRetry ?? 3;
  let messaggio = opzioni.messaggio ?? "Caricamento...";

  console.log({ timeout, maxRetry, messaggio });
}

configura({ timeout: 0 }); // { timeout: 0, maxRetry: 3, messaggio: "Caricamento..." }
configura({}); // { timeout: 3000, maxRetry: 3, messaggio: "Caricamento..." }
```

### L'idioma del Doppio NOT (!!)

`!!` non è un operatore, ma un modo di usare l'operatore `!` due volte per convertire esplicitamente qualsiasi valore nel suo equivalente booleano. È una tecnica per verificare se un valore è truthy (cioè si comporta come true) o falsy (false, 0, "", null, undefined, NaN).

```javascript
/*
 * Doppio NOT (!!) per conversione booleana
 */

// Valori truthy convertiti a true
console.log(!!"Hello"); // true
console.log(!!42); // true
console.log(!![]); // true (array vuoto è truthy)
console.log(!!{}); // true (oggetto vuoto è truthy)
console.log(!!" "); // true (stringa con spazio è truthy)

// Valori falsy convertiti a false
console.log(!!false); // false
console.log(!!0); // false
console.log(!!""); // false (stringa vuota)
console.log(!!null); // false
console.log(!!undefined); // false
console.log(!!NaN); // false

// Come funziona
let valore = "testo";
console.log(!valore); // false (primo NOT: da truthy a false)
console.log(!!valore); // true (secondo NOT: da false a true)

// Uso pratico: verificare esistenza
function haValore(x) {
  return !!x; // converte a booleano
}

console.log(haValore("test")); // true
console.log(haValore("")); // false
console.log(haValore(0)); // false
console.log(haValore(42)); // true
console.log(haValore(null)); // false

// Alternativa più esplicita
function haValoreAlt(x) {
  return Boolean(x); // stesso risultato di !!x
}

// In condizioni (!! è ridondante perché if converte automaticamente)
let input = "dati";
if (input) {
  // ✅ Preferibile
  console.log("Ha input");
}
if (!!input) {
  // Funziona ma !! è superfluo qui
  console.log("Ha input");
}

// Utile per assegnamenti o return espliciti
let isLoggedIn = !!localStorage.getItem("userId");
```

### Precedenza degli Operatori (Operator Precedence)

La precedenza stabilisce l'ordine in cui gli operatori vengono eseguiti in un'espressione. Ad esempio, la moltiplicazione ha la precedenza sull'addizione. Per controllare l'ordine di valutazione si usano le parentesi `()`, che hanno la priorità più alta.

```javascript
/*
 * Precedenza degli operatori
 */

// Senza parentesi (precedenza naturale)
let risultato1 = 2 + 3 * 4; // 14 (prima 3*4=12, poi 2+12=14)
console.log(risultato1);

// Con parentesi (controllo esplicito)
let risultato2 = (2 + 3) * 4; // 20 (prima 2+3=5, poi 5*4=20)
console.log(risultato2);

// Precedenza comune (dal più alto al più basso):
// () → ++ -- → ** → * / % → + - → < > <= >= → == === != !== → && → || → ? : → =

// Esempi di precedenza
console.log(10 + 5 * 2); // 20 (moltiplicazione prima)
console.log(10 - 3 + 2); // 9 (stessa precedenza, da sinistra a destra)
console.log(2 ** (3 ** 2)); // 512 (esponenziazione da destra: 3**2=9, poi 2**9=512)

// Confronti e logica
let a = 5;
let b = 10;
console.log(a < 10 && b > 5); // true
console.log((a < 10 && b > 5) || false); // true (AND prima di OR)
console.log(a < 10 && (b > 5 || false)); // true (parentesi cambiano l'ordine)

// Caso complesso
let x = 3;
let y = 4;
let z = x + y * 2 > 10 ? "Grande" : "Piccolo";
// Ordine: y*2 → x+8 → 11>10 → true → "Grande"
console.log(z); // "Grande"

// Best practice: usare parentesi per chiarezza
let prezzoFinale = (prezzo + tasse) * (1 - sconto);
// Più leggibile di: prezzo + tasse * 1 - sconto
```

---
