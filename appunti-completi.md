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
```

```javascript
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

- **L'interpretazione** (interpreting) consiste nel tradurre ed eseguire il codice sorgente (source code) riga per riga, ogni volta che il programma viene avviato.

- **La compilazione** (compiling) traduce l'intero programma in anticipo. Quando il programma viene eseguito, è la versione già compilata (in linguaggio macchina) ad essere avviata.

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

Il codice non viene scritto solo per il computer, ma anche e soprattutto per gli esseri umani (altri sviluppatori o il "te stesso" del futuro). Per questo, è fondamentale scrivere codice che sia non solo funzionante, ma anche chiaro e comprensibile.

I commenti sono porzioni di testo inserite nel codice che vengono completamente ignorate dal motore JavaScript. Il loro unico scopo è fornire spiegazioni a chi legge il codice.

#### Principi per un Buon Uso dei Commenti

- **Perché, non cosa** → Un buon commento dovrebbe spiegare perché una certa scelta è stata fatta, non cosa fa il codice. Il "cosa" dovrebbe essere reso evidente da un codice scritto in modo chiaro (es. nomi di variabili e funzioni significativi). Un commento può spiegare il come solo se il codice è particolarmente complesso o insolito.

- **Il giusto equilibrio** → Un codice senza commenti è incompleto. Al contrario, troppi commenti (es. uno per ogni riga) sono spesso sintomo di un codice scritto male e poco leggibile.

#### Tipi di Commenti in JavaScript

Esistono due sintassi principali per inserire commenti.

- **Commento su Riga Singola (//)** - Tutto ciò che segue `//` fino alla fine della riga viene considerato un commento. È ideale per note brevi, posizionate sopra un'istruzione o alla fine di una riga.

```javascript
// Questo è un commento su singola riga
let nome = "Mario"; // Commento a fine riga

// Più commenti consecutivi
// possono essere usati per
// spiegazioni più lunghe
```

- **Commento Multiriga (/_ ... _/)** - Tutto ciò che si trova tra `/*` e `*/` è un commento, anche se si estende su più righe. È utile per spiegazioni più lunghe.

```javascript
/*
 * Questo è un commento
 * che si estende su
 * più righe
 */

let risultato = calcola(/* parametro */ valore);
```

**Commenti di Documentazione (JSDoc)** - Un tipo speciale di commento multiriga è il JSDoc, che inizia con `/**` e termina con `*/`. Segue una sintassi strutturata per descrivere funzioni, classi e variabili in modo formale. Questi commenti sono estremamente utili perché possono essere letti da strumenti automatici per generare documentazione o per fornire suggerimenti intelligenti negli editor di codice.

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
```

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

---

### 2.7 Switch

Quando si ha la necessità di confrontare una singola variabile o espressione con una serie di valori specifici, una lunga catena di `if...else if` può diventare verbosa.

In questi scenari, l'istruzione **switch** offre un'alternativa più pulita e strutturata. La sua logica è: "valuta questa espressione e, in base al suo valore, esegui il blocco di codice corrispondente".

La sua struttura si basa su:

- **`case`** → Un'etichetta che rappresenta un possibile valore per l'espressione.
- **`break`** → Un'istruzione che interrompe l'esecuzione dello switch. È fondamentale per evitare che il codice "cada" (fall through) nel caso successivo.
- **`default`** → Un caso opzionale che viene eseguito se nessuno dei case precedenti corrisponde al valore dell'espressione.

```javascript
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

#### Raggruppare i case

Una caratteristica utile dello switch è la possibilità di raggruppare più case per eseguire lo stesso blocco di codice, omettendo deliberatamente il `break`.

```javascript
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
```

In questo esempio, se `giorno` è `"Sabato"`, l'esecuzione "cade" fino al blocco di codice del caso `"Domenica"` ed esegue `console.log("È il weekend!")`.

### 2.8 Cicli (Loops)

I cicli (loops) sono strutture fondamentali in programmazione che permettono di eseguire un blocco di codice ripetutamente, finché una determinata condizione rimane vera. Ogni esecuzione del blocco di codice all'interno di un ciclo è chiamata iterazione (iteration). I cicli sono essenziali per automatizzare compiti ripetitivi.

#### Il Ciclo while

Il ciclo `while` è una delle forme più semplici di ciclo. La sua logica è: "mentre questa condizione è vera, continua a eseguire il blocco di codice". La condizione viene controllata prima di ogni iterazione. Se la condizione risulta falsa fin dall'inizio, il blocco di codice non verrà mai eseguito.

```javascript
// Sintassi
while (condizione) {
  // codice eseguito finché condizione è true
}

// Esempio: contare da 1 a 5
let i = 1;

while (i <= 5) {
  console.log(i);
  i++;
}
```

#### Il Ciclo do...while

Il ciclo `do...while` è molto simile al `while`, ma con una differenza cruciale: la condizione viene controllata dopo ogni iterazione. Questo garantisce che il blocco di codice venga eseguito almeno una volta, anche se la condizione iniziale è falsa.

```javascript
// Sintassi
do {
  // codice eseguito almeno una volta
} while (condizione);

// Esempio
let numero = 10;

do {
  console.log("Numero:", numero);
  numero++;
} while (numero < 5);

// Output: "Numero: 10"
// Il blocco viene eseguito una volta, poi la condizione (10 < 5) è falsa
```

#### Il Ciclo for

Quando il numero di iterazioni è noto in anticipo o si deve contare, il ciclo `for` è spesso la scelta più chiara e compatta. La sua sintassi concentra in un'unica riga tre parti fondamentali:

- **Inizializzazione** → Un'espressione eseguita una sola volta prima dell'inizio del ciclo (es. `let i = 0`).
- **Condizione** → Un'espressione valutata prima di ogni iterazione. Se diventa falsa, il ciclo termina (es. `i < 10`).
- **Aggiornamento** → Un'espressione eseguita alla fine di ogni iterazione (es. `i++`).

```javascript
// Sintassi
for (inizializzazione; condizione; aggiornamento) {
  // codice eseguito ad ogni iterazione
}

// Esempio: contare da 0 a 4
for (let i = 0; i < 5; i++) {
  console.log(i);
}

// Output: 0, 1, 2, 3, 4
```

#### Il Ciclo for...of

Introdotto in ES6, il ciclo `for...of` è il modo moderno e più leggibile per iterare sugli elementi di una struttura iterabile, come un array o una stringa. Ad ogni iterazione, la variabile del ciclo assume il valore dell'elemento corrente.

```javascript
// Sintassi
for (let elemento of iterabile) {
  // lavora con elemento
}

// Esempio: iterare su array
let frutti = ["mela", "banana", "arancia"];

for (let frutto of frutti) {
  console.log(frutto);
}

// Output: "mela", "banana", "arancia"
```

#### Il Ciclo for...in

Il ciclo `for...in` è specifico per iterare sulle proprietà enumerabili di un oggetto. Ad ogni iterazione, la variabile del ciclo assume il nome (la chiave) della proprietà corrente, come stringa.

```javascript
// Sintassi
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

È importante notare che `for...in` non è raccomandato per iterare sugli array, perché potrebbe includere proprietà inaspettate e non garantisce l'ordine degli elementi. Per gli array, `for...of` è la scelta corretta.

#### Interrompere un Ciclo: break

A volte è necessario interrompere un ciclo prima che la sua condizione diventi falsa. Per questo si usa l'istruzione `break`. Appena il programma incontra `break`, esce immediatamente dal ciclo e continua l'esecuzione dal codice successivo.

```javascript
// Uso di break
for (let i = 0; i < 10; i++) {
  if (i === 5) {
    break; // Interrompe il ciclo quando i è 5
  }
  console.log(i);
}

// Output: 0, 1, 2, 3, 4
// (il ciclo si ferma, NON stampa 5, 6, 7, 8, 9)
```

### 2.9 Strict Mode ("Modalità Stretta")

Introdotta in ECMAScript 5 (ES5), la strict mode ("modalità stretta") è una funzionalità che permette di attivare un insieme di regole più restrittive per il codice JavaScript. L'obiettivo è rendere il codice più sicuro, robusto e meno incline a errori comuni, trasformando "errori silenziosi" in errori espliciti che bloccano l'esecuzione.

L'uso dello strict mode è considerato una best practice per tutti i programmi JavaScript moderni, per diverse ragioni:

- **Sicurezza** → Previene pratiche rischiose, come la creazione accidentale di variabili globali.
- **Ottimizzazione** → Un codice che aderisce allo strict mode è generalmente più facile da ottimizzare per i motori JavaScript.
- **Futuro del Linguaggio** → Rappresenta la direzione in cui il linguaggio si sta evolvendo. Abituarsi a scrivere codice in modalità stretta facilita l'adozione delle future funzionalità di JavaScript.

#### Come Attivare lo Strict Mode

Per attivare lo strict mode, è sufficiente inserire la direttiva `"use strict";` (una semplice stringa) all'inizio di un file o di una funzione. La sua posizione ne determina l'ambito di applicazione.

- **A livello di file (globale)** → Se inserita all'inizio di un file, l'intera sceneggiatura verrà eseguita in modalità stretta.

```javascript
"use strict";

// Tutto il codice in questo file è in strict mode
let nome = "Mario";
x = 10; // ❌ ReferenceError: x is not defined
```

- **A livello di funzione** → Se inserita all'inizio del corpo di una funzione, solo quella funzione (e tutte le funzioni annidate al suo interno) verrà eseguita in modalità stretta.

```javascript
function modalitaStretta() {
  "use strict";
  // Solo questa funzione è in strict mode
  y = 5; // ❌ ReferenceError: y is not defined
}

function modalitaNormale() {
  // Questa funzione NON è in strict mode
  z = 10; // ✅ Funziona (crea variabile globale)
}
```

#### Un Esempio Chiave: Prevenire le Globali Accidentali

Uno dei benefici più importanti dello strict mode è che impedisce la creazione implicita di variabili globali. In modalità non-stretta, assegnare un valore a una variabile non dichiarata crea una nuova variabile nello scope globale. In strict mode, questo comportamento è vietato e genera un ReferenceError.

```javascript
// Modalità non-stretta (comportamento pericoloso)
function nonStrictMode() {
  contatore = 0; // ❌ Crea variabile GLOBALE accidentalmente
  contatore++;
}

nonStrictMode();
console.log(contatore); // 1 (variabile globale!)

// Strict mode (comportamento sicuro)
function strictMode() {
  "use strict";
  contatore = 0; // ❌ ReferenceError: contatore is not defined
  contatore++;
}

strictMode(); // Errore bloccato subito
```

Questo costringe lo sviluppatore a dichiarare sempre esplicitamente le proprie variabili (con `let`, `const` o `var`), prevenendo bug difficili da tracciare.

Se l'attivazione dello strict mode causa problemi nel tuo programma, non è un motivo per evitarlo. Al contrario, è un segnale che il tuo codice contiene delle "cattive pratiche" che devono essere corrette. Affrontare questi problemi rende il codice più affidabile e allineato agli standard moderni.

---

## 3. Tipi e Dati

### 3.1 Valori e Tipi (Values & Types)

In un programma, i dati vengono rappresentati in modi diversi a seconda dello scopo per cui vengono usati. Queste diverse rappresentazioni sono chiamate tipi (types). JavaScript definisce alcuni tipi di dati primitivi e fondamentali (built-in types) per gestire le informazioni e sono:

- **string** (per il testo)
- **number** (per i valori numerici)
- **boolean** (per i valori logici true/false)
- **null** e **undefined** (per rappresentare l'assenza di valore)
- **object** (per strutture di dati complesse)
- **symbol** (un tipo speciale introdotto in ES6 per creare identificatori unici)

#### L'Operatore typeof

Per determinare il tipo di un valore durante l'esecuzione del programma, JavaScript fornisce l'operatore `typeof`. Questo operatore unario esamina un valore e restituisce una stringa che ne descrive il tipo.

```javascript
let nome = "Mario";
console.log(typeof nome); // "string"

let eta = 30;
console.log(typeof eta); // "number"

let isAttivo = true;
console.log(typeof isAttivo); // "boolean"

let utente = { nome: "Mario" };
console.log(typeof utente); // "object"

let valoreNullo = null;
console.log(typeof valoreNullo); // "object" (anomalia storica di JavaScript)

let nonDefinito;
console.log(typeof nonDefinito); // "undefined"

let simbolo = Symbol("id");
console.log(typeof simbolo); // "symbol"
```

È importante notare che `typeof` agisce sul valore contenuto nella variabile in quel momento, non sulla variabile stessa.

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

### 3.3 Conversione tra Tipi: Coercizione (Coercion)

Spesso è necessario convertire un valore da un tipo a un altro. Ad esempio, un number deve diventare una string per essere visualizzato, o una string inserita in un form deve diventare un number per essere usata in un calcolo. Questo processo di conversione in JavaScript è chiamato **coercizione** (coercion).

Esistono due tipi di coercizione: **esplicita** e **implicita**.

#### Coercizione Esplicita (Explicit Coercion)

Si ha una coercizione esplicita quando il programmatore chiede deliberatamente di convertire un tipo. Si usano costrutti del linguaggio fatti apposta per questo scopo, come la funzione `Number()`. L'intenzione è chiara e il risultato prevedibile.

```javascript
let a = "42";
let b = Number(a);

console.log(a); // "42"
console.log(b); // 42
```

#### Coercizione Implicita (Implicit Coercion)

La coercizione implicita avviene automaticamente quando JavaScript incontra un'operazione tra tipi diversi. L'esempio più comune è l'uso dell'operatore di uguaglianza lasca (`==`).

Quando si confrontano due valori di tipo diverso con `==`, JavaScript tenta di "aiutare" convertendone uno per farli corrispondere, prima di eseguire il confronto.

```javascript
let a = "99.99";
let b = 99.99;

console.log(a == b); // true
```

In questo caso, JavaScript converte implicitamente la stringa `"99.99"` nel numero `99.99` e poi confronta `99.99` con `99.99`, ottenendo `true`.

#### La Controversia sulla Coercizione Implicita

La coercizione implicita è uno degli argomenti più controversi in JavaScript.

**La critica comune** è che molti sviluppatori la considerano una fonte di bug e confusione. Poiché le sue regole non sono sempre intuitive, il consiglio diffuso è di evitarla completamente, preferendo sempre l'operatore di uguaglianza stretta (`===`), che non esegue coercizione.

**Evitarla a priori** d'altro canto significa non padroneggiare completamente il linguaggio.

---

### 3.4 Valori Truthy e Falsy

In JavaScript, quando un valore non booleano viene usato in un contesto che si aspetta un booleano (come la condizione di un `if` o l'operando di un operatore logico), il linguaggio lo converte implicitamente in `true` o `false`. Questo processo è chiamato **coercizione booleana**, e i valori vengono classificati come **truthy** o **falsy** in base al risultato.

#### Valori Falsy

I valori **falsy** sono quelli che, quando forzati a diventare booleani, si convertono in `false`. La lista dei valori falsy è breve e ben definita:

- `false`
- `0` (zero)
- `""` (stringa vuota)
- `null`
- `undefined`
- `NaN` (Not a Number)

Qualsiasi valore che non rientra in questa lista è considerato **truthy**.

#### Valori Truthy

Un valore **truthy** è qualsiasi valore che, quando convertito in booleano, diventa `true`. Questo include praticamente tutto il resto:

- Stringhe non vuote (es. `"ciao"`, `"false"`)
- Numeri diversi da zero (es. `42`, `-1`)
- Array, anche se vuoti (`[]`)
- Oggetti, anche se vuoti (`{}`)
- Funzioni

È importante notare che anche un **array vuoto** o un **oggetto vuoto** sono **truthy**. Questo può a volte generare confusione.

#### Utilizzo Pratico

La conoscenza dei valori truthy e falsy permette di scrivere codice più conciso e leggibile, specialmente nelle istruzioni condizionali. Ad esempio, invece di controllare se una variabile non è `null` o `undefined`, si può semplicemente usare la variabile stessa come condizione.

```javascript
let nomeUtente = "Mario";

if (nomeUtente) {
  console.log("Benvenuto, " + nomeUtente);
} else {
  console.log("Nome non fornito");
}
```

In questo esempio, se `nomeUtente` contiene una stringa non vuota (un valore truthy), la condizione è vera. Se invece contiene una stringa vuota o `null` (valori falsy), la condizione è falsa e viene eseguito il blocco `else`.

---

### 3.5 Boxing e Metodi dei Primitivi

In JavaScript, anche i tipi primitivi (string, number, boolean) possono esporre metodi e proprietà utili per manipolarli, nonostante non siano oggetti. Questo avviene grazie al meccanismo del **boxing**.

```javascript
let testo = "javascript";
console.log(testo.toUpperCase()); // "JAVASCRIPT"

let numero = 3.14159;
console.log(numero.toFixed(2)); // "3.14"
```

#### Il Meccanismo del "Boxing"

Potrebbe sembrare strano che un valore primitivo, come una semplice stringa, possa avere dei metodi come un oggetto. Questo è possibile grazie a un meccanismo automatico chiamato **boxing**.

Quando si tenta di accedere a una proprietà o a un metodo su un valore primitivo (es. `a.toUpperCase()`), JavaScript "avvolge" temporaneamente il valore primitivo in un oggetto corrispondente (un oggetto `String` per una string, un `Number` per un number, etc.). Questo oggetto "wrapper" contiene i metodi. Una volta che il metodo è stato eseguito, l'oggetto temporaneo viene scartato.

Questo processo è completamente trasparente per lo sviluppatore. La regola generale è **preferire sempre l'uso dei valori primitivi** e lasciare che JavaScript gestisca il boxing quando necessario.

#### Conversione Esplicita dei Tipi (Explicit Coercion)

Oltre a questi metodi integrati, JavaScript fornisce strumenti specifici per convertire esplicitamente un valore da un tipo a un altro.

**Convertire in Number**

Per trasformare una stringa o un altro valore in un numero, si possono usare diversi approcci.

- **Operatore Unario +** → È il modo più moderno e conciso per forzare la conversione di una stringa in un numero.

```javascript
let a = "42";
console.log(+a); // 42
```

- **parseInt() e parseFloat()** → Queste funzioni analizzano una stringa e restituiscono un numero. `parseInt()` estrae solo la parte intera, mentre `parseFloat()` gestisce anche i decimali.

```javascript
let b = parseInt("99.99");
console.log(b); // 99

let c = parseFloat("99.99");
console.log(c); // 99.99
```

**Convertire in String**

Per trasformare un numero o un booleano in una stringa, ci sono due metodi principali.

- **La funzione String()** → Questa è una funzione globale sicura che funziona con qualsiasi valore, inclusi `null` e `undefined`, senza generare errori.

```javascript
let a = 42;
console.log(String(a)); // "42"
```

- **Il metodo .toString()** → Questo è un metodo disponibile su quasi tutti gli oggetti e valori primitivi. Tuttavia, chiamarlo su `null` o `undefined` provocherà un errore, perché questi valori non hanno metodi.

```javascript
let b = 42;
console.log(b.toString()); // "42"

// null.toString(); // ❌ TypeError
```

Per questo motivo, **String() è generalmente la scelta più robusta e sicura** per la conversione a stringa.

---

### 3.6 Oggetti (Objects)

Il tipo object è uno dei più potenti e versatili in JavaScript. Un oggetto è un valore composto, una sorta di contenitore che raggruppa dati e funzionalità correlate. Questi dati sono organizzati come una collezione di proprietà (properties), dove ogni proprietà è una coppia chiave-valore. La chiave è un nome (una stringa), e il valore può essere di qualsiasi tipo: un numero, una stringa, un booleano, un'altra funzione o persino un altro oggetto.

```javascript
/*
 * Creazione di oggetti
 */

// Oggetto semplice con proprietà di diversi tipi
let persona = {
  nome: "Mario",
  cognome: "Rossi",
  eta: 30,
  citta: "Roma",
  isAttivo: true,
};

console.log(persona);
// { nome: 'Mario', cognome: 'Rossi', eta: 30, citta: 'Roma', isAttivo: true }

// Oggetto con proprietà annidate e array
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
  mostraInfo: function () {
    // funzione come proprietà
    console.log(`${this.nome} - €${this.prezzo}`);
  },
};

console.log(prodotto.specifiche.processore); // "Intel i7"
prodotto.mostraInfo(); // "Laptop - €899.99"
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

- **Bracket Notation (Notazione a Parentesi Quadre)** → Si usa il nome dell'oggetto seguito da parentesi quadre [] che contengono il nome della proprietà come stringa. Questa notazione è indispensabile in due casi:
  - Quando il nome della proprietà contiene spazi o caratteri speciali.
  - Quando il nome della proprietà è memorizzato in una variabile.

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

let campo = "eta";
console.log(persona[campo]); // 30

// Esempio pratico con variabile
function ottieniValore(obj, chiave) {
  return obj[chiave]; // bracket notation con parametro
}

console.log(ottieniValore(persona, "nome")); // "Mario"
console.log(ottieniValore(persona, "eta")); // 30
```

#### Manipolare le Proprietà

Le proprietà di un oggetto possono essere aggiunte, modificate o eliminate dinamicamente. Per eliminare una proprietà si usa l'operatore delete.

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

- **Oggetti "Dictionary" (o "Slow")** → Quando si altera la forma di un oggetto in modo imprevedibile, ad esempio aggiungendo o eliminando proprietà dinamicamente (specialmente con delete), il motore non può più fare affidamento sulla hidden class. L'ottimizzazione salta e l'oggetto viene declassato a una struttura più lenta, simile a un dizionario o una hash map. L'accesso alle proprietà diventa più lento perché il motore deve cercare la chiave in un dizionario invece di accedere a una posizione di memoria fissa.

In sintesi, usare delete è funzionale, ma può avere un costo in termini di performance perché trasforma un oggetto da "fast" a "slow".

```javascript
/*
 * Oggetti ottimizzati (fast) vs non ottimizzati (slow)
 */

// ✅ FAST - Struttura prevedibile
let persona1 = { nome: "Mario", eta: 30 };
let persona2 = { nome: "Luigi", eta: 25 };
let persona3 = { nome: "Anna", eta: 28 };
// Tutti e tre condividono la stessa hidden class (nome, eta)
// Accesso alle proprietà estremamente veloce

// ❌ SLOW - Struttura mutata con delete
let utente = { id: 1, nome: "Mario", email: "mario@example.com" };
delete utente.email; // L'oggetto diventa "dictionary mode"
// Adesso l'accesso a utente.nome è più lento

// ❌ SLOW - Aggiunta di proprietà in ordine diverso
let obj1 = {};
obj1.a = 1;
obj1.b = 2;

let obj2 = {};
obj2.b = 2; // ordine diverso
obj2.a = 1;
// obj1 e obj2 non possono condividere la stessa hidden class
```

#### Alternative Moderne e Immutabili a delete

Per evitare le penalità di performance e seguire un approccio più moderno e "immutabile" (cioè creare un nuovo oggetto con le modifiche desiderate invece di alterare l'originale), esistono tecniche migliori per "rimuovere" una proprietà.

**Destrutturazione con Rest Syntax (...)**

Questo è il metodo più comune e leggibile. Si "estrae" la proprietà che si vuole rimuovere e si raccolgono tutte le altre in un nuovo oggetto usando l'operatore rest (...).

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
// L'originale rimane intatto! ✅

// Rimuovere più proprietà
let { email: _, eta: __, ...personaMinima } = persona;
console.log(personaMinima);
// { nome: 'Mario', cognome: 'Rossi' }
```

**Object.entries, filter, e Object.fromEntries**

Questo approccio è più verboso ma molto potente, specialmente se la logica di filtraggio è complessa.

- Object.entries(persona) → Converte l'oggetto in un array di coppie [chiave, valore]. [['nome', 'Mario'], ['cognome', 'Rossi'], ...] → questa è una matrice.
- .filter() → Filtra questo array, tenendo solo le coppie che non corrispondono alla chiave da rimuovere.
- Object.fromEntries() → Riconverte l'array filtrato in un nuovo oggetto.

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

Un concetto fondamentale è che le variabili non contengono direttamente l'oggetto, ma un riferimento (reference) alla sua posizione in memoria. Questo significa che due variabili diverse possono puntare allo stesso oggetto.

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
```

Di conseguenza, due oggetti creati separatamente, anche se con le stesse identiche proprietà, non saranno mai uguali (===), perché sono due entità distinte in memoria.

```javascript
/*
 * Oggetti con le stesse proprietà NON sono uguali
 */
let auto1 = { marca: "Fiat", modello: "500" };
let auto2 = { marca: "Fiat", modello: "500" };

console.log(auto1 === auto2); // false (due oggetti diversi in memoria)
console.log(auto1 == auto2); // false (stesso comportamento)

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

#### Sottotipi di Oggetto: Array e Funzioni

In JavaScript, anche gli array e le funzioni sono, a un livello più profondo, dei tipi speciali di oggetti. Hanno funzionalità aggiuntive (come l'accesso agli elementi tramite indice per gli array o la possibilità di essere invocate per le funzioni), ma ereditano le caratteristiche di base degli oggetti.

```javascript
/*
 * Array e funzioni come oggetti
 */

// Array è un sottotipo di oggetto
let numeri = [10, 20, 30];

console.log(typeof numeri); // "object"
console.log(Array.isArray(numeri)); // true (verifica specifica per array)

// Gli array hanno proprietà come gli oggetti
numeri.descrizione = "Lista di numeri";
console.log(numeri.descrizione); // "Lista di numeri"

// Funzione è anche un sottotipo di oggetto
function saluta(nome) {
  return `Ciao ${nome}`;
}

console.log(typeof saluta); // "function" (tipo speciale)
console.log(saluta instanceof Object); // true (è un oggetto)

// Le funzioni possono avere proprietà
saluta.versione = "1.0";
saluta.autore = "Mario";
console.log(saluta.versione); // "1.0"
console.log(saluta.autore); // "Mario"

// Differenza: le funzioni sono "callable" (invocabili)
console.log(saluta("Anna")); // "Ciao Anna"

// Gli oggetti regolari non sono invocabili
let obj = { nome: "Test" };
// obj(); // ❌ TypeError: obj is not a function
```

### 3.7 Array

Un array in JavaScript è una struttura dati, un tipo speciale di oggetto, progettato per contenere una collezione ordinata di elementi. A differenza degli oggetti generici, dove i valori sono associati a chiavi testuali (nomi di proprietà), in un array i valori sono posizionati in base a un indice numerico.

L'indicizzazione parte da 0 per il primo elemento. Questo significa che per accedere agli elementi si usano le parentesi quadre [] con il numero della posizione desiderata.

```javascript
/*
 * Creazione e accesso agli array
 */

// Creazione di un array
let frutti = ["mela", "banana", "arancia"];
//           [  0  ,    1    ,     2     ]  ← indici

// Accesso agli elementi tramite indice
console.log(frutti[0]); // "mela" (primo elemento)
console.log(frutti[1]); // "banana" (secondo elemento)
console.log(frutti[2]); // "arancia" (terzo elemento)

// Proprietà length
console.log(frutti.length); // 3 (numero di elementi)

// Array con diversi tipi di dati
let misto = [42, "testo", true, null, { nome: "Mario" }, [1, 2, 3]];
console.log(misto[0]); // 42
console.log(misto[1]); // "testo"
console.log(misto[4]); // { nome: "Mario" }
console.log(misto[5][1]); // 2 (accesso a elemento di array annidato)

// Modificare elementi
frutti[1] = "pera";
console.log(frutti); // ["mela", "pera", "arancia"]

// Aggiungere elementi tramite indice
frutti[3] = "kiwi";
console.log(frutti); // ["mela", "pera", "arancia", "kiwi"]
```

#### Array come Oggetti Speciali

Sebbene typeof restituisca "object" per un array, è importante usarlo per il suo scopo specifico: gestire liste di dati ordinate numericamente. Ogni array ha una proprietà length che viene aggiornata automaticamente e indica il numero di elementi contenuti.

```javascript
/*
 * Array come oggetti speciali
 */

let numeri = [10, 20, 30];

// typeof restituisce "object"
console.log(typeof numeri); // "object"

// Verifica specifica per array
console.log(Array.isArray(numeri)); // true
console.log(Array.isArray({ a: 1 })); // false

// Proprietà length aggiornata automaticamente
console.log(numeri.length); // 3
numeri.push(40);
console.log(numeri.length); // 4

// Gli array sono oggetti, quindi possono avere proprietà
numeri.descrizione = "Lista di numeri";
console.log(numeri.descrizione); // "Lista di numeri"
// Ma questo è sconsigliato! Usa array per dati indicizzati

// Confronto array vs oggetto
let arrayDati = ["Mario", 30, "Roma"]; // ✅ Lista ordinata
let oggettoDati = { nome: "Mario", eta: 30, citta: "Roma" }; // ✅ Proprietà nominate

console.log(arrayDati[0]); // "Mario" (accesso per indice)
console.log(oggettoDati.nome); // "Mario" (accesso per nome)
```

La regola generale è: usare gli array per collezioni di dati a cui si accede tramite un indice numerico e gli oggetti per strutture di dati a cui si accede tramite nomi di proprietà significativi.

#### Metodi Comuni degli Array

Gli array dispongono di numerosi metodi integrati (built-in methods) che semplificano la manipolazione dei dati.

**Aggiungere e Rimuovere Elementi**

Esistono metodi specifici per aggiungere o rimuovere elementi all'inizio o alla fine di un array.

- **push()** → Aggiunge uno o più elementi alla fine dell'array.

```javascript
let numeri = [1, 2, 3];
numeri.push(4);
console.log(numeri); // [1, 2, 3, 4]

numeri.push(5, 6);
console.log(numeri); // [1, 2, 3, 4, 5, 6]

// push() restituisce la nuova lunghezza
let lunghezza = numeri.push(7);
console.log(lunghezza); // 7
```

- **pop()** → Rimuove l'ultimo elemento dall'array e lo restituisce.

```javascript
let numeri = [1, 2, 3];
let ultimo = numeri.pop();
console.log(ultimo); // 3
console.log(numeri); // [1, 2]

// Rimuovere più elementi
numeri.pop();
console.log(numeri); // [1]
```

- **unshift()** → Aggiunge uno o più elementi all'inizio dell'array.

```javascript
let numeri = [2, 3];
numeri.unshift(1);
console.log(numeri); // [1, 2, 3]

numeri.unshift(-1, 0);
console.log(numeri); // [-1, 0, 1, 2, 3]

// unshift() restituisce la nuova lunghezza
let lunghezza = numeri.unshift(-2);
console.log(lunghezza); // 6
```

- **shift()** → Rimuove il primo elemento dall'array e lo restituisce.

```javascript
let numeri = [1, 2, 3];
let primo = numeri.shift();
console.log(primo); // 1
console.log(numeri); // [2, 3]

// Rimuovere più elementi
numeri.shift();
console.log(numeri); // [3]
```

**Iterare e Trasformare**

Questi metodi, spesso chiamati "higher-order functions", permettono di eseguire operazioni su ogni elemento dell'array, spesso creando un nuovo array come risultato.

- **forEach()** → Esegue una funzione per ogni elemento dell'array. Non restituisce un nuovo array.

```javascript
let numeri = [1, 2, 3, 4, 5];

// Stampare ogni elemento
numeri.forEach(function (numero) {
  console.log(numero);
});
// Output: 1, 2, 3, 4, 5

// Con indice e array completo
numeri.forEach(function (numero, indice, array) {
  console.log(`Indice ${indice}: ${numero}`);
});

// Modificare elementi (l'array originale viene modificato)
let valori = [1, 2, 3];
valori.forEach(function (numero, indice, arr) {
  arr[indice] = numero * 2;
});
console.log(valori); // [2, 4, 6]
```

- **map()** → Crea un nuovo array contenente i risultati di una funzione applicata a ogni elemento dell'array originale.

```javascript
let numeri = [1, 2, 3, 4, 5];

// Raddoppiare ogni numero
let doppi = numeri.map(function (n) {
  return n * 2;
});
console.log(doppi); // [2, 4, 6, 8, 10]
console.log(numeri); // [1, 2, 3, 4, 5] (originale intatto)

// Trasformare oggetti
let persone = [
  { nome: "Mario", eta: 30 },
  { nome: "Luigi", eta: 25 },
];

let nomi = persone.map(function (persona) {
  return persona.nome;
});
console.log(nomi); // ["Mario", "Luigi"]
```

- **filter()** → Crea un nuovo array contenente solo gli elementi che superano un test (una funzione che restituisce true).

```javascript
let numeri = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// Filtrare numeri pari
let pari = numeri.filter(function (n) {
  return n % 2 === 0;
});
console.log(pari); // [2, 4, 6, 8, 10]

// Filtrare numeri maggiori di 5
let maggiori = numeri.filter(function (n) {
  return n > 5;
});
console.log(maggiori); // [6, 7, 8, 9, 10]

// Filtrare oggetti
let persone = [
  { nome: "Mario", eta: 30 },
  { nome: "Luigi", eta: 17 },
  { nome: "Anna", eta: 25 },
];

let adulti = persone.filter(function (persona) {
  return persona.eta >= 18;
});
console.log(adulti); // [{ nome: "Mario", eta: 30 }, { nome: "Anna", eta: 25 }]
```

- **reduce()** → Applica una funzione a ogni elemento per "ridurre" l'array a un singolo valore (es. una somma, un oggetto).

```javascript
let numeri = [1, 2, 3, 4, 5];

// Somma di tutti gli elementi
let somma = numeri.reduce(function (accumulatore, valore) {
  return accumulatore + valore;
}, 0); // 0 è il valore iniziale
console.log(somma); // 15

// Prodotto di tutti gli elementi
let prodotto = numeri.reduce(function (acc, val) {
  return acc * val;
}, 1);
console.log(prodotto); // 120

// Trovare il valore massimo
let max = numeri.reduce(function (acc, val) {
  return val > acc ? val : acc;
});
console.log(max); // 5

// Contare occorrenze
let frutti = ["mela", "banana", "mela", "arancia", "banana", "mela"];
let conteggio = frutti.reduce(function (acc, frutto) {
  acc[frutto] = (acc[frutto] || 0) + 1;
  return acc;
}, {});
console.log(conteggio); // { mela: 3, banana: 2, arancia: 1 }
```

**Altri Metodi Utili**

- **slice()** → Restituisce una copia superficiale (shallow copy) di una porzione dell'array in un nuovo array, senza modificare l'originale.

```javascript
let numeri = [1, 2, 3, 4, 5];

// Estrarre una porzione (da indice start a end, escluso)
let porzione = numeri.slice(1, 4);
console.log(porzione); // [2, 3, 4] (indici 1, 2, 3)
console.log(numeri); // [1, 2, 3, 4, 5] (originale intatto)

// slice() senza parametri copia tutto l'array
let copia = numeri.slice();
console.log(copia); // [1, 2, 3, 4, 5]

// Indici negativi (contano dalla fine)
let ultimi = numeri.slice(-2);
console.log(ultimi); // [4, 5]
```

- **splice()** → Modifica il contenuto di un array rimuovendo, sostituendo o aggiungendo elementi direttamente nell'array originale.

```javascript
let numeri = [1, 2, 3, 4, 5];

// Rimuovere 2 elementi a partire dall'indice 1
let rimossi = numeri.splice(1, 2);
console.log(rimossi); // [2, 3] (elementi rimossi)
console.log(numeri); // [1, 4, 5] (array modificato)

// Aggiungere elementi senza rimuovere (count = 0)
numeri = [1, 2, 3, 4, 5];
numeri.splice(2, 0, 10, 20);
console.log(numeri); // [1, 2, 10, 20, 3, 4, 5]

// Sostituire elementi
numeri = [1, 2, 3, 4, 5];
numeri.splice(2, 1, 99);
console.log(numeri); // [1, 2, 99, 4, 5] (sostituisce 3 con 99)
```

- **includes()** → Controlla se un array include un certo elemento, restituendo true o false.

```javascript
let frutti = ["mela", "banana", "arancia"];

console.log(frutti.includes("banana")); // true
console.log(frutti.includes("pera")); // false

// Con numeri
let numeri = [1, 2, 3, 4, 5];
console.log(numeri.includes(3)); // true
console.log(numeri.includes(10)); // false

// Specificare l'indice di partenza
console.log(numeri.includes(3, 3)); // false (cerca da indice 3 in poi)
```

- **find()** → Restituisce il primo elemento dell'array che soddisfa una condizione.

```javascript
let numeri = [5, 12, 8, 130, 44];

// Trovare il primo numero maggiore di 10
let trovato = numeri.find(function (n) {
  return n > 10;
});
console.log(trovato); // 12

// Se nessun elemento soddisfa la condizione, restituisce undefined
let nonTrovato = numeri.find(function (n) {
  return n > 200;
});
console.log(nonTrovato); // undefined

// Con oggetti
let persone = [
  { nome: "Mario", eta: 30 },
  { nome: "Luigi", eta: 25 },
  { nome: "Anna", eta: 28 },
];

let persona = persone.find(function (p) {
  return p.nome === "Luigi";
});
console.log(persona); // { nome: "Luigi", eta: 25 }
```

### 3.8 Funzioni (Functions)

In JavaScript, una funzione è un blocco di codice riutilizzabile, progettato per eseguire un compito specifico. Permette di organizzare il codice in pezzi logici, evitando di ripetere le stesse istruzioni più volte.

```javascript
/*
 * Funzioni base
 */

// Dichiarazione di funzione
function saluta() {
  console.log("Ciao!");
}

// Chiamata della funzione
saluta(); // "Ciao!"

// Funzione con parametri
function somma(a, b) {
  return a + b;
}

let risultato = somma(5, 3);
console.log(risultato); // 8

// Funzione che stampa vs funzione che restituisce
function stampa(messaggio) {
  console.log(messaggio); // side effect
  // non ha return, quindi restituisce undefined
}

function restituisci(valore) {
  return valore * 2; // restituisce un valore
}

let x = stampa("Test"); // stampa "Test"
console.log(x); // undefined

let y = restituisci(10);
console.log(y); // 20
```

#### Anatomia di una Funzione

Una funzione è composta da alcuni elementi chiave. La sua dichiarazione (declaration) avviene tipicamente usando la parola chiave function, seguita da un nome, una lista di parametri (parameters) tra parentesi (), e un corpo (body) racchiuso tra parentesi graffe {}.

```javascript
/*
 * Anatomia di una funzione
 */

// function keyword → nome → parametri → corpo
function calcolaAreaRettangolo(larghezza, altezza) {
  let area = larghezza * altezza;
  return area;
}

// Chiamata: nome → argomenti
let areaStanza = calcolaAreaRettangolo(5, 3);
console.log(areaStanza); // 15

/*
 * Elementi chiave
 */

function esempio(parametro1, parametro2) {
  // ↑ Parametri: variabili che ricevono i valori
  // Corpo della funzione
  let risultato = parametro1 + parametro2;
  return risultato; // Return: valore restituito
} // ← fine del corpo

let valore = esempio(10, 20); // 10 e 20 sono argomenti
console.log(valore); // 30
```

I parametri sono come delle variabili locali che ricevono i valori (chiamati argomenti, arguments) passati alla funzione quando viene eseguita.

```javascript
/*
 * Parametri vs Argomenti
 */

function moltiplica(x, y) {
  // x e y sono PARAMETRI (nella definizione)
  return x * y;
}

let prodotto = moltiplica(4, 7); // 4 e 7 sono ARGOMENTI (nella chiamata)
console.log(prodotto); // 28

// Più argomenti del previsto: gli extra vengono ignorati
function somma(a, b) {
  return a + b;
}
console.log(somma(1, 2, 3, 4)); // 3 (solo 1 e 2 vengono usati)

// Meno argomenti del previsto: i parametri mancanti sono undefined
function somma3(a, b, c) {
  return a + b + c;
}
console.log(somma3(1, 2)); // NaN (1 + 2 + undefined)

// Parametri con valori di default (ES6+)
function salutaConDefault(nome = "Ospite") {
  return "Ciao, " + nome + "!";
}
console.log(salutaConDefault()); // "Ciao, Ospite!"
console.log(salutaConDefault("Mario")); // "Ciao, Mario!"
```

L'istruzione return permette a una funzione di restituire un valore al codice che l'ha chiamata, terminando la sua esecuzione. Se return non è presente, la funzione restituisce implicitamente undefined.

```javascript
/*
 * Return in azione
 */

function calcolaSconto(prezzo, percentuale) {
  let sconto = (prezzo * percentuale) / 100;
  return sconto; // restituisce il valore
  console.log("Questa riga non viene mai eseguita"); // irraggiungibile
}

let scontoApplicato = calcolaSconto(100, 20);
console.log(scontoApplicato); // 20

// Return anticipato per uscire dalla funzione
function categoriaEta(eta) {
  if (eta < 18) {
    return "Minorenne"; // esce subito
  }
  if (eta < 65) {
    return "Adulto";
  }
  return "Senior";
}

console.log(categoriaEta(15)); // "Minorenne"
console.log(categoriaEta(30)); // "Adulto"
console.log(categoriaEta(70)); // "Senior"

// Funzione senza return
function stampaMessaggio(msg) {
  console.log(msg);
  // nessun return esplicito
}

let risultato = stampaMessaggio("Ciao"); // stampa "Ciao"
console.log(risultato); // undefined (return implicito)
```

#### Funzioni come Oggetti (First-Class Citizens)

Un concetto fondamentale in JavaScript è che le funzioni sono un tipo speciale di oggetto. Questo significa che, come qualsiasi altro oggetto, possono essere assegnate a variabili, passate come argomenti ad altre funzioni e, soprattutto, possono avere delle proprietà.

L'operatore typeof riconosce questa natura speciale restituendo la stringa "function".

```javascript
/*
 * Funzioni come oggetti
 */

// Assegnare una funzione a una variabile
const miaSomma = function (a, b) {
  return a + b;
};

console.log(miaSomma(3, 4)); // 7
console.log(typeof miaSomma); // "function"

// Le funzioni possono avere proprietà!
function contatore() {
  contatore.volte = (contatore.volte || 0) + 1;
  console.log("Chiamata #" + contatore.volte);
}

contatore(); // "Chiamata #1"
contatore(); // "Chiamata #2"
contatore(); // "Chiamata #3"
console.log(contatore.volte); // 3 (proprietà della funzione)

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

console.log(doppio(5)); // 10 (5 * 2)
console.log(triplo(5)); // 15 (5 * 3)

// Array di funzioni
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

Questa caratteristica rende le funzioni "cittadini di prima classe" (first-class citizens) nel linguaggio, conferendo loro un'enorme flessibilità.

#### Chiamare una Funzione

Per eseguire il codice all'interno di una funzione, bisogna chiamarla (call o invoke) usando il suo nome seguito dalle parentesi (). Se la funzione accetta parametri, gli argomenti vengono passati all'interno delle parentesi.

```javascript
/*
 * Chiamare una funzione
 */

function saluta() {
  console.log("Ciao!");
}

// Chiamata senza argomenti
saluta(); // "Ciao!"
saluta(); // può essere chiamata più volte

// Con argomenti
function benvenuto(nome, momento) {
  console.log("Buon" + momento + ", " + nome + "!");
}

benvenuto("Mario", "giorno"); // "Buongiorno, Mario!"
benvenuto("Anna", "asera"); // "Buonasera, Anna!"

// Funzioni annidate (chiamate dentro altre funzioni)
function calcolaComplesso() {
  function somma(a, b) {
    return a + b;
  }

  function moltiplica(a, b) {
    return a * b;
  }

  let risultato = moltiplica(somma(2, 3), 4); // (2+3) * 4
  return risultato;
}

console.log(calcolaComplesso()); // 20

// Chiamate multiple in cascata
function raddoppia(n) {
  return n * 2;
}

console.log(raddoppia(raddoppia(raddoppia(5)))); // 40 (5 → 10 → 20 → 40)
```

#### Hoisting: Dichiarazione vs. Esecuzione

Il motore JavaScript elabora il codice in due fasi. Durante la prima fase, di analisi (parsing), "solleva" (un processo chiamato hoisting) le dichiarazioni di funzione in cima al loro contesto. Questo significa che è possibile chiamare una funzione dichiarata con function prima che appaia nel codice, senza generare errori.

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
// console.log(quadrato(5));               ← eseguita dopo

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
 * Confronto pratico
 */

// FUNCTION DECLARATION (viene sollevata)
saluta1(); // ✅ "Ciao da declaration"

function saluta1() {
  console.log("Ciao da declaration");
}

// FUNCTION EXPRESSION (NON viene sollevata)
// saluta2(); // ❌ ReferenceError!

const saluta2 = function () {
  console.log("Ciao da expression");
};

saluta2(); // ✅ "Ciao da expression"

/*
 * Arrow function (ES6) - NON sollevate
 */

// saluta3(); // ❌ Errore!

const saluta3 = () => {
  console.log("Ciao da arrow");
};

saluta3(); // ✅ "Ciao da arrow"
```

Questo comportamento non si applica alle variabili dichiarate con let o const, che non possono essere usate prima della loro dichiarazione. (Temporal Dead Zone - TDZ)

#### Esecuzione Diretta vs. Indiretta

Esiste una differenza fondamentale tra eseguire una funzione immediatamente e passare un riferimento ad essa per un'esecuzione futura.

- **Esecuzione Diretta** → Usare le parentesi () dopo il nome della funzione ne provoca l'esecuzione immediata.

- **Esecuzione Indiretta (Passare un Riferimento)** → Fornire solo il nome della funzione, senza parentesi, significa passare un riferimento ad essa. Questo è comune nella gestione degli eventi, dove si dice al browser di eseguire una certa funzione solo quando si verifica un evento (es. un click).

```javascript
/*
 * Esecuzione diretta vs indiretta
 */

function mostraMessaggio() {
  console.log("Ciao!");
}

// Esecuzione diretta (con parentesi)
mostraMessaggio(); // esegue subito, stampa "Ciao!"

// Passare un riferimento (senza parentesi)
let riferimento = mostraMessaggio; // NON esegue, assegna il riferimento
console.log(typeof riferimento); // "function"
riferimento(); // ora esegue, stampa "Ciao!"

/*
 * Uso comune: event listeners
 */

// ❌ SBAGLIATO - esegue immediatamente
// button.addEventListener('click', mostraMessaggio());
// La funzione si esegue subito, undefined viene passato al listener

// ✅ CORRETTO - passa il riferimento
// button.addEventListener('click', mostraMessaggio);
// La funzione verrà eseguita quando si verifica il click

/*
 * Esempio con setTimeout
 */

function avviso() {
  console.log("Tempo scaduto!");
}

// ✅ Passa il riferimento (esegue dopo 3 secondi)
setTimeout(avviso, 3000);

// ❌ Esecuzione immediata (sbagliato)
// setTimeout(avviso(), 3000);
// avviso() si esegue subito, undefined viene passato a setTimeout

/*
 * Quando serve passare argomenti
 */

function salutaPersona(nome) {
  console.log("Ciao, " + nome + "!");
}

// Soluzione: wrappare in una funzione arrow
setTimeout(() => salutaPersona("Mario"), 2000);

// Oppure usare una function expression
setTimeout(function () {
  salutaPersona("Luigi");
}, 2000);

/*
 * Esempio pratico con array methods
 */

let numeri = [1, 2, 3, 4, 5];

function raddoppia(n) {
  return n * 2;
}

// Passa il riferimento a map
let doppi = numeri.map(raddoppia); // NON raddoppia()!
console.log(doppi); // [2, 4, 6, 8, 10]
```

#### IIFE (Immediately Invoked Function Expressions)

Una IIFE (pronunciata "iffy") è una Espressione di Funzione Invocata Immediatamente. È un pattern di design in cui una funzione viene dichiarata e poi eseguita subito dopo la sua creazione.

La sintassi di una IIFE può sembrare insolita a prima vista, ma è molto logica. Si compone di due parti principali:

1. Un'espressione di funzione, tipicamente anonima, avvolta tra parentesi (). Le parentesi servono a indicare al motore JavaScript che si tratta di un'espressione e non di una dichiarazione di funzione standard.
2. Un secondo paio di parentesi () alla fine, che è l'operatore di chiamata che esegue la funzione immediatamente.

```javascript
/*
 * Sintassi IIFE
 */

// IIFE base
(function () {
  console.log("Questa funzione si esegue immediatamente!");
})();

// Struttura:  (espressione di funzione)(chiamata)
//              ^^^^^^^^^^^^^^^^^^^^^^^^  ^^

// IIFE con nome (opzionale, utile per debug)
(function iife() {
  console.log("IIFE con nome");
})();

// Sintassi alternativa (parentesi di chiamata dentro)
(function () {
  console.log("Sintassi alternativa");
})();

// Con arrow function (ES6+)
(() => {
  console.log("IIFE con arrow function");
})();
```

Il concetto è simile a chiamare una normale funzione nominata: in entrambi i casi, si ha un riferimento a una funzione seguito dalle parentesi di esecuzione ().

```javascript
/*
 * Confronto con funzione normale
 */

// Funzione normale
function saluta() {
  console.log("Ciao");
}
saluta(); // dichiarazione separata dalla chiamata

// IIFE: tutto in un'espressione
(function () {
  console.log("Ciao");
})(); // dichiarazione E chiamata insieme

// È come fare:
let temp = function () {
  console.log("Ciao");
};
temp(); // ma senza lasciare 'temp' nello scope
```

**Lo Scopo Principale → Creare uno Scope Privato**

Il vantaggio più grande di una IIFE è la sua capacità di creare uno scope privato. Poiché ogni funzione in JavaScript crea il proprio scope, tutte le variabili dichiarate all'interno di una IIFE sono confinate al suo interno e non "inquinano" lo scope circostante (globale o di un'altra funzione).

Questo era un pattern fondamentale prima dell'introduzione di let e const (che hanno lo scope di blocco), quando si usava var (che ha lo scope di funzione) e si voleva evitare di creare variabili globali accidentalmente.

```javascript
/*
 * IIFE per scope privato
 */

// ❌ Senza IIFE - variabile globale con var
var contatore = 0;
var incrementa = function () {
  contatore++;
};
console.log(contatore); // 0 (accessibile globalmente - inquinamento)

// ✅ Con IIFE - scope privato
(function () {
  var contatore = 0; // privato! Esiste solo dentro la IIFE

  function incrementa() {
    contatore++;
    console.log("Contatore:", contatore);
  }

  incrementa(); // "Contatore: 1"
  incrementa(); // "Contatore: 2"
})();

// console.log(contatore); // ❌ ReferenceError - non accessibile

/*
 * Evitare conflitti di nomi tra file
 */

// File1.js
(function () {
  var nome = "Mario";
  var id = 123;
  console.log("File 1:", nome, id);
})();

// File2.js
(function () {
  var nome = "Luigi"; // Nessun conflitto!
  var id = 456;
  console.log("File 2:", nome, id);
})();

/*
 * Pattern Module con IIFE (encapsulation)
 */

let modulo = (function () {
  // Variabili private (non accessibili dall'esterno)
  let contatore = 0;
  let segreto = "password123";

  // API pubblica (ritornata ed esposta)
  return {
    incrementa: function () {
      contatore++;
    },
    decrementa: function () {
      contatore--;
    },
    getValue: function () {
      return contatore;
    },
    // segreto NON è esposto
  };
})();

modulo.incrementa();
modulo.incrementa();
modulo.incrementa();
console.log(modulo.getValue()); // 3
console.log(modulo.segreto); // undefined (privato, non accessibile)
console.log(modulo.contatore); // undefined (privato, non accessibile)
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
})("Mario", 30); // argomenti passati subito

// Pattern comune: passare oggetti globali (window, document)
(function (global, doc) {
  console.log("Titolo pagina:", doc.title);
  global.miVariabile = "Valore globale";
})(window, document);

// Con jQuery era comune
(function ($) {
  // $ è jQuery, passato come parametro
  $(".elemento").hide();
})(jQuery);

/*
 * IIFE con return
 */

// Inizializzare una variabile con logica complessa
const risultato = (function () {
  let moltiplicatore = 5;
  let valoreBase = 10;
  let calcolo = moltiplicatore * valoreBase;
  return calcolo;
})();

console.log(risultato); // 50
// moltiplicatore e valoreBase non esistono più

// Esempio più elaborato: configurazione
const config = (function () {
  let ambiente = "produzione"; // variabile temporanea
  let apiUrl;

  if (ambiente === "sviluppo") {
    apiUrl = "http://localhost:3000/api";
  } else if (ambiente === "staging") {
    apiUrl = "https://staging-api.example.com";
  } else {
    apiUrl = "https://api.example.com";
  }

  // Restituisce solo ciò che serve
  return {
    ambiente: ambiente,
    apiUrl: apiUrl,
    version: "1.0.0",
    debug: ambiente === "sviluppo",
  };
})();

console.log(config.apiUrl); // "https://api.example.com"
console.log(config.debug); // false

/*
 * IIFE per inizializzazione complessa
 */

const utente = (function () {
  let nomeCompleto = "Mario Rossi";
  let parti = nomeCompleto.split(" ");
  let iniziali = parti[0][0] + parti[1][0];
  let username = (parti[0] + parti[1]).toLowerCase();

  return {
    nome: nomeCompleto,
    iniziali: iniziali,
    username: username,
    email: username + "@example.com",
  };
})();

console.log(utente);
// {
//   nome: 'Mario Rossi',
//   iniziali: 'MR',
//   username: 'mariorossi',
//   email: 'mariorossi@example.com'
// }
```

In questo esempio, la IIFE viene eseguita immediatamente, calcola il risultato e lo restituisce. Il valore restituito (50) viene quindi assegnato alla costante risultato. Le variabili moltiplicatore e valoreBase esistono solo durante l'esecuzione della IIFE e poi scompaiono.

### 3.9 Closure (Chiusura)

La Closure (o chiusura) è uno dei concetti più importanti e spesso meno compresi in JavaScript. Si può considerare come la capacità di una funzione di "ricordare" e continuare ad accedere al proprio scope (le sue variabili) anche dopo che la funzione ha terminato la sua esecuzione.

Questo meccanismo permette a una funzione interna di mantenere un riferimento vivo alle variabili della funzione esterna che la contiene.

Consideriamo questo esempio:

```javascript
/*
 * Esempio base di closure
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

1. Quando viene chiamata `makeAdder(1)`, si ottiene un riferimento alla sua funzione interna `add`, la quale "ricorda" che `x` è `1`. Questo riferimento viene assegnato alla variabile `plusOne`.

2. Quando viene chiamata `makeAdder(10)`, si ottiene un altro riferimento alla sua funzione interna `add`, che in questo caso "ricorda" che `x` è `10`. Questo nuovo riferimento viene assegnato a `plusTen`.

3. Quando si esegue `plusOne(3)`, la funzione aggiunge `3` (il suo parametro `y`) al valore `1` (la `x` che ha "ricordato"), restituendo `4`.

4. Quando si esegue `plusTen(13)`, la funzione aggiunge `13` (il suo `y`) al valore `10` (la `x` che ha "ricordato"), restituendo `23`.

In sostanza, ogni volta che `makeAdder` viene eseguita, viene creato un nuovo scope e la funzione `add` interna mantiene un collegamento a quello specifico scope. La closure è una delle tecniche più potenti e versatili della programmazione, e padroneggiarla è fondamentale per uno sviluppatore JavaScript.

```javascript
/*
 * Altri esempi di closure
 */

// Contatore privato con closure
function creaContatore() {
  let contatore = 0; // variabile privata

  return function () {
    contatore++;
    return contatore;
  };
}

let conta = creaContatore();
console.log(conta()); // 1
console.log(conta()); // 2
console.log(conta()); // 3

// Ogni istanza ha il suo contatore
let conta2 = creaContatore();
console.log(conta2()); // 1 (nuovo contatore)
console.log(conta()); // 4 (contatore precedente continua)

// Closure con più variabili
function creaSaluto(saluto) {
  return function (nome) {
    return saluto + ", " + nome + "!";
  };
}

let salutaItaliano = creaSaluto("Ciao");
let salutaInglese = creaSaluto("Hello");
let salutaSpagnolo = creaSaluto("Hola");

console.log(salutaItaliano("Mario")); // "Ciao, Mario!"
console.log(salutaInglese("John")); // "Hello, John!"
console.log(salutaSpagnolo("Carlos")); // "Hola, Carlos!"

// Closure in loop (problema classico con var)
for (var i = 1; i <= 3; i++) {
  setTimeout(function () {
    console.log(i); // stampa 4, 4, 4 (problema!)
  }, i * 1000);
}

// Soluzione con closure (IIFE)
for (var i = 1; i <= 3; i++) {
  (function (j) {
    setTimeout(function () {
      console.log(j); // stampa 1, 2, 3 (corretto!)
    }, j * 1000);
  })(i);
}

// Soluzione moderna con let (ha block scope)
for (let i = 1; i <= 3; i++) {
  setTimeout(function () {
    console.log(i); // stampa 1, 2, 3 (corretto!)
  }, i * 1000);
}

// Closure per memorizzare stato complesso
function creaCalcolatrice() {
  let memoria = 0;
  let storia = [];

  return {
    add: function (num) {
      memoria += num;
      storia.push(`+${num} = ${memoria}`);
      return memoria;
    },
    subtract: function (num) {
      memoria -= num;
      storia.push(`-${num} = ${memoria}`);
      return memoria;
    },
    reset: function () {
      memoria = 0;
      storia.push("reset");
      return memoria;
    },
    getStoria: function () {
      return storia.slice(); // copia dell'array
    },
  };
}

let calc = creaCalcolatrice();
calc.add(10); // 10
calc.add(5); // 15
calc.subtract(3); // 12
calc.reset(); // 0
console.log(calc.getStoria());
// ["+10 = 10", "+5 = 15", "-3 = 12", "reset"]

// Closure per configurazione
function creaLogger(prefisso) {
  let contatore = 0;

  return function (messaggio) {
    contatore++;
    console.log(`[${prefisso}] #${contatore}: ${messaggio}`);
  };
}

let loggerApp = creaLogger("APP");
let loggerDB = creaLogger("DB");

loggerApp("Applicazione avviata"); // [APP] #1: Applicazione avviata
loggerDB("Connessione al database"); // [DB] #1: Connessione al database
loggerApp("Utente loggato"); // [APP] #2: Utente loggato
loggerDB("Query eseguita"); // [DB] #2: Query eseguita
```

### 3.10 Module Pattern

L'uso più comune della closure in JavaScript è il Module Pattern. Questo pattern permette di definire dettagli implementativi privati (variabili e funzioni) che sono nascosti al mondo esterno, e allo stesso tempo di esporre un'interfaccia pubblica (public API) che può essere utilizzata per interagire con essi.

È una tecnica fondamentale per l'incapsulamento e l'organizzazione del codice.

Consideriamo il seguente esempio:

```javascript
/*
 * Module Pattern base
 */

function User() {
  // Variabili private (non accessibili dall'esterno)
  let username;
  let password;

  // Funzione privata (non accessibile dall'esterno)
  function doLogin(user, pw) {
    username = user;
    password = pw;
    console.log("Login effettuato per:", username);
  }

  // API pubblica (ciò che viene esposto)
  let publicAPI = {
    login: doLogin,
  };

  return publicAPI;
}

// Creiamo un'istanza del modulo
let fred = User();
fred.login("fred", "12Battery34!"); // Login effettuato per: fred

// Non possiamo accedere alle variabili private
console.log(fred.username); // undefined (privato!)
console.log(fred.password); // undefined (privato!)
// console.log(fred.doLogin); // undefined (privato!)

// Ogni istanza è indipendente
let john = User();
john.login("john", "password123");
// fred e john hanno stati privati separati
```

Analizziamo il funzionamento:

1. **Scope Esterno** → La funzione `User()` agisce come uno scope esterno che contiene le variabili `username` e `password`, e la funzione `doLogin()`. Questi elementi sono privati e non possono essere raggiunti direttamente dall'esterno.

2. **Creazione dell'Istanza** → Eseguendo `User()`, si crea un'istanza del modulo. Viene generato un nuovo scope e, di conseguenza, una nuova copia di tutte le variabili e funzioni interne. L'oggetto restituito, `publicAPI`, viene assegnato alla variabile `fred`. Se si eseguisse di nuovo `User()`, si otterrebbe una nuova istanza completamente separata da `fred`.

3. **Nota** → Si usa `User()` e non `new User()` perché `User` è una semplice funzione che funge da factory, non una classe da istanziare. L'uso di `new` in questo contesto sarebbe inappropriato.

4. **API Pubblica** → L'oggetto `publicAPI` contiene i metodi che si vogliono rendere pubblici. In questo caso, ha una sola proprietà, `login`, che è un riferimento alla funzione interna `doLogin()`.

5. **Il Ruolo della Closure** → Quando la funzione `User()` termina la sua esecuzione, le sue variabili interne (`username`, `password`) non vengono distrutte. Esse vengono "mantenute in vita" dalla closure creata dalla funzione `doLogin()`. Per questo motivo, quando si chiama `fred.login(...)`, la funzione `doLogin` può ancora accedere e modificare le variabili `username` e `password` definite nel suo scope genitore.

In sintesi, il Module Pattern sfrutta le closure per creare uno stato privato e un'interfaccia pubblica, un concetto chiave per scrivere codice robusto e manutenibile.

```javascript
/*
 * Module Pattern più completo
 */

function BankAccount(initialBalance) {
  // Variabili private
  let balance = initialBalance || 0;
  let transactionHistory = [];
  let accountNumber = Math.floor(Math.random() * 1000000);

  // Funzioni private (helper)
  function recordTransaction(type, amount) {
    transactionHistory.push({
      type: type,
      amount: amount,
      date: new Date(),
      balance: balance,
    });
  }

  function isValidAmount(amount) {
    return typeof amount === "number" && amount > 0;
  }

  // API pubblica
  return {
    deposit: function (amount) {
      if (!isValidAmount(amount)) {
        console.log("Importo non valido");
        return false;
      }
      balance += amount;
      recordTransaction("deposit", amount);
      console.log(`Depositati €${amount}. Saldo: €${balance}`);
      return true;
    },

    withdraw: function (amount) {
      if (!isValidAmount(amount)) {
        console.log("Importo non valido");
        return false;
      }
      if (amount > balance) {
        console.log("Fondi insufficienti");
        return false;
      }
      balance -= amount;
      recordTransaction("withdraw", amount);
      console.log(`Prelevati €${amount}. Saldo: €${balance}`);
      return true;
    },

    getBalance: function () {
      return balance;
    },

    getAccountNumber: function () {
      return accountNumber;
    },

    getHistory: function () {
      // Restituisce una copia per evitare modifiche esterne
      return transactionHistory.slice();
    },
  };
}

// Uso del modulo
let myAccount = BankAccount(1000);
console.log("Numero conto:", myAccount.getAccountNumber());

myAccount.deposit(500); // Depositati €500. Saldo: €1500
myAccount.withdraw(200); // Prelevati €200. Saldo: €1300
myAccount.withdraw(2000); // Fondi insufficienti

console.log("Saldo attuale:", myAccount.getBalance()); // 1300

// Variabili private non accessibili
console.log(myAccount.balance); // undefined
console.log(myAccount.accountNumber); // undefined
console.log(myAccount.recordTransaction); // undefined
```

```javascript
/*
 * Module Pattern con IIFE (Singleton)
 */

let AppConfig = (function () {
  // Stato privato
  let apiKey = "abc123xyz";
  let environment = "production";
  let debugMode = false;

  // Funzioni private
  function log(message) {
    if (debugMode) {
      console.log(`[CONFIG] ${message}`);
    }
  }

  // API pubblica
  return {
    getApiUrl: function () {
      if (environment === "development") {
        return "http://localhost:3000/api";
      }
      return "https://api.production.com";
    },

    setEnvironment: function (env) {
      if (env === "development" || env === "production") {
        environment = env;
        log(`Ambiente cambiato in: ${env}`);
      }
    },

    enableDebug: function () {
      debugMode = true;
      log("Debug mode attivato");
    },

    disableDebug: function () {
      debugMode = false;
    },

    // apiKey rimane privato, non esposto
  };
})();

// Uso del singleton
console.log(AppConfig.getApiUrl()); // https://api.production.com
AppConfig.enableDebug();
AppConfig.setEnvironment("development"); // [CONFIG] Ambiente cambiato in: development
console.log(AppConfig.getApiUrl()); // http://localhost:3000/api

// Stato privato non accessibile
console.log(AppConfig.apiKey); // undefined
console.log(AppConfig.environment); // undefined
```

```javascript
/*
 * Module Pattern con namespace
 */

let MyApp = MyApp || {};

MyApp.Utils = (function () {
  // Metodi privati
  function privateHelper() {
    return "Helper privato";
  }

  // API pubblica
  return {
    formatDate: function (date) {
      return date.toLocaleDateString("it-IT");
    },

    generateId: function () {
      return "id_" + Math.random().toString(36).substr(2, 9);
    },

    capitalize: function (str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    },
  };
})();

MyApp.Database = (function () {
  let data = {}; // storage privato

  return {
    save: function (key, value) {
      data[key] = value;
    },

    get: function (key) {
      return data[key];
    },

    remove: function (key) {
      delete data[key];
    },
  };
})();

// Uso dei moduli organizzati
console.log(MyApp.Utils.formatDate(new Date()));
let id = MyApp.Utils.generateId();
MyApp.Database.save(id, { nome: "Mario" });
console.log(MyApp.Database.get(id)); // { nome: "Mario" }
```

### 3.11 L'identificatore this

Un altro concetto spesso frainteso in JavaScript è la parola chiave `this`. Sebbene possa sembrare legata a paradigmi di programmazione orientata agli oggetti, in JavaScript il suo funzionamento è diverso.

Se una funzione contiene un riferimento a `this`, quel riferimento di solito punta a un oggetto. Tuttavia, l'oggetto a cui punta dipende da come la funzione è stata chiamata (call-site). È fondamentale capire che `this` non si riferisce alla funzione stessa, che è l'equivoco più comune.

```javascript
/*
 * Le quattro regole di this
 */

function foo() {
  console.log(this.bar);
}

var bar = "global";

var obj1 = {
  bar: "obj1",
  foo: foo,
};

var obj2 = {
  bar: "obj2",
};

// -------------------------
foo(); // "global" (default binding)
obj1.foo(); // "obj1" (implicit binding)
foo.call(obj2); // "obj2" (explicit binding)
new foo(); // undefined (new binding)
```

Esistono quattro regole principali che determinano il valore di `this`, illustrate nelle ultime quattro righe dell'esempio:

1. **Chiamata diretta (`foo()`)** → Quando una funzione viene chiamata direttamente, senza un contesto specifico, `this` viene associato all'oggetto globale (in un browser, `window`). Questo è noto come **default binding**. Di conseguenza, `this.bar` si risolve in `window.bar`, che ha il valore `"global"`. (In strict mode, `this` sarebbe `undefined` e l'accesso a `this.bar` genererebbe un errore).

2. **Chiamata come metodo (`obj1.foo()`)** → Quando una funzione viene chiamata come metodo di un oggetto, `this` punta all'oggetto stesso che contiene il metodo. Questo è l'**implicit binding**. In questo caso, `this` è `obj1`, quindi `this.bar` vale `"obj1"`.

3. **Chiamata esplicita (`foo.call(obj2)`)** → È possibile impostare esplicitamente il valore di `this` usando i metodi `.call()` o `.apply()`. Questo è l'**explicit binding**. Qui, `this` viene forzato a essere `obj2`, quindi `this.bar` vale `"obj2"`.

4. **Chiamata con new (`new foo()`)** → Quando una funzione viene usata come costruttore con la parola chiave `new`, `this` viene associato a un nuovo oggetto vuoto creato per l'occasione. Questo è il **new binding**. Poiché questo nuovo oggetto non ha una proprietà `bar`, `this.bar` risulta `undefined`.

In conclusione, per capire a cosa si riferisce `this`, è necessario esaminare il punto esatto in cui la funzione viene chiamata. Il contesto di quella chiamata determinerà il valore di `this` secondo una di queste quattro regole.

```javascript
/*
 * Esempi dettagliati delle quattro regole
 */

// 1. DEFAULT BINDING
function mostraNome() {
  console.log(this.nome);
}

var nome = "Globale";
mostraNome(); // "Globale" (this = window/global)

// In strict mode:
("use strict");
function mostraNomeStrict() {
  console.log(this); // undefined
  // console.log(this.nome); // ❌ TypeError
}
// mostraNomeStrict();

// 2. IMPLICIT BINDING
let persona = {
  nome: "Mario",
  saluta: function () {
    console.log("Ciao, sono " + this.nome);
  },
};

persona.saluta(); // "Ciao, sono Mario" (this = persona)

// Attenzione: perdita del binding
let saluto = persona.saluta;
saluto(); // "Ciao, sono Globale" (this = window, default binding!)

// Esempio con oggetti annidati
let obj = {
  livello: "obj",
  inner: {
    livello: "inner",
    mostra: function () {
      console.log(this.livello);
    },
  },
};

obj.inner.mostra(); // "inner" (this = obj.inner, non obj!)

// 3. EXPLICIT BINDING
function descrivi() {
  console.log(this.tipo + ": " + this.nome);
}

let animale1 = { tipo: "Cane", nome: "Fido" };
let animale2 = { tipo: "Gatto", nome: "Micio" };

descrivi.call(animale1); // "Cane: Fido"
descrivi.call(animale2); // "Gatto: Micio"

// call vs apply
function somma(a, b) {
  console.log(this.nome + " calcola: " + (a + b));
}

let utente = { nome: "Mario" };

somma.call(utente, 5, 3); // "Mario calcola: 8" (argomenti separati)
somma.apply(utente, [5, 3]); // "Mario calcola: 8" (argomenti in array)

// bind - crea una nuova funzione con this fisso
let salutaMario = persona.saluta.bind(persona);
salutaMario(); // "Ciao, sono Mario" (this è sempre persona)

setTimeout(persona.saluta, 1000); // "Ciao, sono Globale" (perde this)
setTimeout(persona.saluta.bind(persona), 1000); // "Ciao, sono Mario" (this fissato)

// 4. NEW BINDING
function Persona(nome, eta) {
  this.nome = nome;
  this.eta = eta;
  this.descrivi = function () {
    console.log(this.nome + " ha " + this.eta + " anni");
  };
}

let p1 = new Persona("Mario", 30);
let p2 = new Persona("Luigi", 25);

p1.descrivi(); // "Mario ha 30 anni"
p2.descrivi(); // "Luigi ha 25 anni"

console.log(p1.nome); // "Mario" (this era il nuovo oggetto)
```

```javascript
/*
 * Problemi comuni e soluzioni
 */

// Problema: callback perde this
let contatore = {
  count: 0,
  incrementa: function () {
    this.count++;
    console.log(this.count);
  },
};

contatore.incrementa(); // 1 (funziona)
// setTimeout(contatore.incrementa, 1000); // NaN (perde this)

// Soluzione 1: arrow function
setTimeout(() => contatore.incrementa(), 1000); // 2 (funziona)

// Soluzione 2: bind
setTimeout(contatore.incrementa.bind(contatore), 1000); // 3 (funziona)

// Soluzione 3: variabile self/that
let obj2 = {
  count: 0,
  incrementa: function () {
    let self = this; // salva riferimento
    setTimeout(function () {
      self.count++;
      console.log(self.count);
    }, 1000);
  },
};

// Arrow function NON ha proprio this (usa this del contesto)
let oggetto = {
  nome: "Test",
  metodoNormale: function () {
    console.log(this.nome); // "Test"
  },
  metodoArrow: () => {
    console.log(this.nome); // undefined (this è del contesto esterno)
  },
};

oggetto.metodoNormale(); // "Test"
oggetto.metodoArrow(); // undefined

// Arrow function utile in callback
let timer = {
  secondi: 0,
  avvia: function () {
    setInterval(() => {
      this.secondi++; // this è timer (arrow function)
      console.log(this.secondi);
    }, 1000);
  },
};

// timer.avvia(); // 1, 2, 3, ... (funziona!)
```

```javascript
/*
 * Precedenza delle regole (dalla più alta alla più bassa)
 */

function test() {
  console.log(this.valore);
}

let objA = { valore: "A", test: test };
let objB = { valore: "B" };

// 1. new ha la precedenza più alta
let istanza = new test(); // undefined (nuovo oggetto vuoto)

// 2. explicit binding ha precedenza su implicit
objA.test.call(objB); // "B" (call vince su oggetto)

// 3. implicit binding ha precedenza su default
objA.test(); // "A" (oggetto vince su globale)

// 4. default binding (più bassa)
test(); // undefined o errore in strict mode
```

### 3.12 Prototipi (Prototypes)

Il meccanismo dei prototipi (prototype) in JavaScript è un concetto fondamentale, anche se complesso. Funziona come un sistema di "fallback" per le proprietà degli oggetti.

Quando si cerca di accedere a una proprietà su un oggetto e questa non viene trovata, JavaScript utilizza automaticamente un riferimento interno al prototipo di quell'oggetto per cercare la proprietà su un altro oggetto collegato. Questo collegamento tra un oggetto e il suo prototipo viene stabilito al momento della creazione dell'oggetto.

Il modo più semplice per illustrare questo concetto è tramite la funzione Object.create().

```javascript
var foo = {
  a: 42,
};

// Crea `bar` e lo collega a `foo`
var bar = Object.create(foo);

console.log(bar.a); // 42
```

In questo esempio, la proprietà "a" non esiste direttamente sull'oggetto bar. Tuttavia, poiché "bar" è collegato tramite prototipo a "foo", JavaScript "risale" la catena dei prototipi, trova la proprietà "a" su "foo" e ne restituisce il valore. Questo processo è noto come delega (delegation).

Questo meccanismo viene spesso utilizzato (o, secondo alcuni, "abusato") per emulare il concetto di "classi" e "ereditarietà" tipico di altri linguaggi. Tuttavia, un approccio più naturale e in linea con la natura di JavaScript è il pattern della Behavior Delegation (delega del comportamento). Con questo pattern, gli oggetti vengono progettati intenzionalmente per delegare parti del loro comportamento ad altri oggetti a cui sono collegati, creando catene di oggetti che collaborano tra loro.

#### Riflessione sull'Uso dei Prototipi nello Sviluppo Moderno

Nello sviluppo front-end contemporaneo, specialmente utilizzando framework come Angular, React o Vue, è raro che uno sviluppatore si trovi a manipolare direttamente i prototipi degli oggetti. Questo porta a chiedersi quale sia la loro reale utilità pratica.

La risposta è che i prototipi vengono utilizzati costantemente, ma in modo implicito, poiché sono un dettaglio implementativo fondamentale del linguaggio, nascosto da livelli di astrazione più moderni.

#### L'Astrazione delle Classi ES6

Il motivo principale per cui non si interagisce più direttamente con i prototipi è l'introduzione della sintassi class in ECMAScript 2015 (ES6). Questa sintassi è in realtà solo zucchero sintattico (syntactic sugar) che astrae la manipolazione del prototipo.

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
```

Sotto il cofano, viene tradotto da JavaScript in un'operazione basata sui prototipi, simile a come si scriveva prima di ES6:

```javascript
// Pre-ES6
function Person(name) {
  this.name = name;
}
Person.prototype.greet = function () {
  console.log("Ciao, sono " + this.name);
};
```

Ogni volta che si definisce una classe e i suoi metodi, si sta quindi utilizzando il sistema dei prototipi.

#### Esempi di Uso Implicito dei Prototipi

L'interazione con la catena dei prototipi (prototype chain) avviene continuamente:

- **Metodi degli Array** → Metodi come .map(), .filter() o .forEach() non sono duplicati su ogni singolo array creato. Essi risiedono su Array.prototype e ogni istanza di array delega a questo prototipo l'esecuzione di tali metodi.

- **Metodi degli Oggetti** → Lo stesso principio si applica a metodi come .toString() o .hasOwnProperty(), che sono ereditati da Object.prototype.

- **Il DOM** → Ogni elemento del DOM è un oggetto che eredita metodi come .addEventListener() o .querySelector() da prototipi come HTMLElement.prototype e EventTarget.prototype.

#### Perché è Ancora Importante Conoscerli?

Comprendere il funzionamento dei prototipi rimane una competenza cruciale per uno sviluppatore JavaScript per diverse ragioni:

- **Debugging** → La conoscenza della catena prototipale aiuta a diagnosticare errori come TypeError: is not a function, permettendo di ispezionare quali metodi sono realmente disponibili su un oggetto e sui suoi prototipi.

- **Performance** → Capire che i metodi sul prototipo sono condivisi tra tutte le istanze di un oggetto chiarisce perché questo approccio sia efficiente in termini di memoria.

- **Comprensione di Librerie e Framework** → Molte librerie, specialmente quelle più datate o quelle ottimizzate per le massime prestazioni, possono manipolare i prototipi direttamente. Conoscerne i meccanismi permette di usarle con maggiore consapevolezza.

- **Polyfilling** → Per garantire la compatibilità con browser meno recenti, a volte è necessario implementare manualmente funzionalità moderne mancanti (un polyfill), operazione che spesso richiede di estendere il prototipo di oggetti nativi (es. Array.prototype).

In conclusione, sebbene la manipolazione diretta dei prototipi sia diventata rara nella pratica quotidiana, essi costituiscono il motore del sistema a oggetti di JavaScript. La loro comprensione è fondamentale per padroneggiare il linguaggio a un livello più profondo, andando oltre le astrazioni fornite dalla sintassi moderna.

#### Esempi di Codice

```javascript
/*
 * 1. Object.create() - Collegamento Base
 */

var animale = {
  tipo: "Animale",
  respira: function () {
    console.log(this.tipo + " sta respirando");
  },
};

// Crea un oggetto collegato ad 'animale'
var cane = Object.create(animale);
cane.tipo = "Cane";
cane.abbaia = function () {
  console.log("Bau bau!");
};

cane.respira(); // "Cane sta respirando" - delega a animale
cane.abbaia(); // "Bau bau!" - metodo proprio

// Verifica della catena prototipale
console.log(cane.hasOwnProperty("tipo")); // true - proprietà propria
console.log(cane.hasOwnProperty("respira")); // false - ereditata dal prototipo
```

```javascript
/*
 * 2. Catena dei Prototipi - Lookup Delegation
 */

var livello1 = {
  a: 1,
};

var livello2 = Object.create(livello1);
livello2.b = 2;

var livello3 = Object.create(livello2);
livello3.c = 3;

// JavaScript risale la catena finché non trova la proprietà
console.log(livello3.c); // 3 - trovata su livello3
console.log(livello3.b); // 2 - trovata su livello2 (prototipo)
console.log(livello3.a); // 1 - trovata su livello1 (prototipo del prototipo)
console.log(livello3.d); // undefined - non trovata in nessun livello

// Shadowing - proprietà con stesso nome
livello3.a = 100; // Non modifica livello1.a, crea nuova proprietà
console.log(livello3.a); // 100
console.log(livello1.a); // 1 - rimane invariato
```

```javascript
/*
 * 3. ES6 Class vs Prototype - Confronto
 */

// Sintassi ES6 Class
class VeicoloClass {
  constructor(marca, modello) {
    this.marca = marca;
    this.modello = modello;
  }

  descrizione() {
    return this.marca + " " + this.modello;
  }

  avvia() {
    return "Avvio del veicolo...";
  }
}

// Equivalente con Prototype (pre-ES6)
function VeicoloProto(marca, modello) {
  this.marca = marca;
  this.modello = modello;
}

VeicoloProto.prototype.descrizione = function () {
  return this.marca + " " + this.modello;
};

VeicoloProto.prototype.avvia = function () {
  return "Avvio del veicolo...";
};

// Utilizzo identico
var auto1 = new VeicoloClass("Fiat", "500");
var auto2 = new VeicoloProto("Fiat", "Panda");

console.log(auto1.descrizione()); // "Fiat 500"
console.log(auto2.descrizione()); // "Fiat Panda"

// Entrambi usano i prototipi sotto
console.log(auto1.descrizione === auto1.__proto__.descrizione); // true
console.log(auto2.descrizione === auto2.__proto__.descrizione); // true
```

```javascript
/*
 * 4. Array.prototype - Metodi Condivisi
 */

var numeri1 = [1, 2, 3];
var numeri2 = [4, 5, 6];

// I metodi NON sono duplicati - risiedono su Array.prototype
console.log(numeri1.map === numeri2.map); // true - stesso riferimento
console.log(numeri1.filter === Array.prototype.filter); // true

// Ogni array delega al prototipo
console.log(numeri1.hasOwnProperty("map")); // false - non è proprietà propria
console.log(Array.prototype.hasOwnProperty("map")); // true - sul prototipo

// Questo risparmia memoria: migliaia di array condividono gli stessi metodi
var arrayGrande = new Array(10000);
// Non contiene copie di map, filter, reduce, ecc.
// Tutte le chiamate delegano ad Array.prototype
```

```javascript
/*
 * 5. Object.prototype - Metodi Universali
 */

var persona = {
  nome: "Mario",
  eta: 30,
};

// toString() è ereditato da Object.prototype
console.log(persona.toString()); // "[object Object]"
console.log(persona.hasOwnProperty("toString")); // false

// hasOwnProperty() stesso è su Object.prototype
console.log(persona.hasOwnProperty("nome")); // true
console.log(Object.prototype.hasOwnProperty("hasOwnProperty")); // true

// Tutti gli oggetti hanno Object.prototype nella catena
var array = [];
var funzione = function () {};
var data = new Date();

console.log(array.hasOwnProperty); // ereditato da Object.prototype
console.log(funzione.hasOwnProperty); // ereditato da Object.prototype
console.log(data.hasOwnProperty); // ereditato da Object.prototype
```

```javascript
/*
 * 6. DOM - Catena Prototipale degli Elementi
 */

// Esempio concettuale (richiede ambiente browser)
/*
var button = document.querySelector('button');

// Catena prototipale del DOM:
// button (HTMLButtonElement instance)
//   └─> HTMLButtonElement.prototype
//       └─> HTMLElement.prototype
//           └─> Element.prototype
//               └─> Node.prototype
//                   └─> EventTarget.prototype
//                       └─> Object.prototype
//                           └─> null

// addEventListener() proviene da EventTarget.prototype
button.addEventListener('click', function() {
  console.log('Clicked!');
});

// querySelector() proviene da Element.prototype (con override in Document)
// innerHTML proviene da Element.prototype
// appendChild() proviene da Node.prototype

console.log(button.hasOwnProperty('addEventListener')); // false
console.log(EventTarget.prototype.hasOwnProperty('addEventListener')); // true
*/
```

```javascript
/*
 * 7. Polyfill - Estendere Prototipi Nativi
 */

// Polyfill per Array.prototype.includes (per browser vecchi)
if (!Array.prototype.includes) {
  Array.prototype.includes = function (searchElement, fromIndex) {
    // Verifica che this sia un oggetto
    if (this == null) {
      throw new TypeError('"this" è null o undefined');
    }

    var array = Object(this);
    var length = parseInt(array.length) || 0;

    // Nessun elemento da cercare
    if (length === 0) {
      return false;
    }

    var startIndex = parseInt(fromIndex) || 0;
    var currentIndex;

    if (startIndex >= 0) {
      currentIndex = startIndex;
    } else {
      // Indice negativo: parte dalla fine
      currentIndex = length + startIndex;
      if (currentIndex < 0) {
        currentIndex = 0;
      }
    }

    // Cerca l'elemento
    while (currentIndex < length) {
      var currentElement = array[currentIndex];

      // Gestisce NaN (NaN === NaN è false, ma dovrebbe trovarlo)
      if (
        searchElement === currentElement ||
        (searchElement !== searchElement && currentElement !== currentElement)
      ) {
        return true;
      }

      currentIndex++;
    }

    return false;
  };
}

// Ora tutti gli array hanno includes(), anche in browser vecchi
var frutti = ["mela", "banana", "arancia"];
console.log(frutti.includes("banana")); // true
console.log(frutti.includes("uva")); // false
```

```javascript
/*
 * 8. Debugging - Ispezionare la Catena Prototipale
 */

var obj = {
  nome: "Test",
};

// Ottenere il prototipo di un oggetto
var proto = Object.getPrototypeOf(obj);
console.log(proto); // Object.prototype
console.log(proto === Object.prototype); // true

// Verifica se un oggetto è nel prototipo di un altro
console.log(Object.prototype.isPrototypeOf(obj)); // true

// Creare oggetto senza prototipo (per dizionari puri)
var dizionarioPuro = Object.create(null);
console.log(Object.getPrototypeOf(dizionarioPuro)); // null
// dizionarioPuro.toString(); // ❌ Errore! Non ha metodi ereditati

// Elencare proprietà proprie vs ereditate
var animale = {
  respira: true,
};

var gatto = Object.create(animale);
gatto.miagola = true;

console.log("--- Proprietà proprie ---");
for (var prop in gatto) {
  if (gatto.hasOwnProperty(prop)) {
    console.log(prop + ": " + gatto[prop]); // "miagola: true"
  }
}

console.log("--- Tutte le proprietà (incluse ereditate) ---");
for (var prop in gatto) {
  console.log(prop + ": " + gatto[prop]);
  // "miagola: true"
  // "respira: true"
}

// Object.keys() restituisce solo proprietà proprie
console.log(Object.keys(gatto)); // ["miagola"]
```

```javascript
/*
 * 9. Behavior Delegation Pattern
 */

// Invece di simulare classi/ereditarietà, delegare comportamento

var Controller = {
  errors: [],
  mostraErrori: function () {
    console.log("Errori: " + this.errors.join(", "));
  },
  aggiungiErrore: function (msg) {
    this.errors.push(msg);
  },
};

// LoginController delega a Controller
var LoginController = Object.create(Controller);

LoginController.errors = [];
LoginController.login = function (username, password) {
  if (!username) {
    this.aggiungiErrore("Username mancante");
  }
  if (!password) {
    this.aggiungiErrore("Password mancante");
  }

  if (this.errors.length === 0) {
    console.log("Login riuscito per " + username);
  } else {
    this.mostraErrori();
  }
};

LoginController.login("", ""); // "Errori: Username mancante, Password mancante"

// RegisterController delega a Controller
var RegisterController = Object.create(Controller);

RegisterController.errors = [];
RegisterController.register = function (username, password, email) {
  if (!email) {
    this.aggiungiErrore("Email mancante");
  }
  if (password.length < 8) {
    this.aggiungiErrore("Password troppo corta");
  }

  if (this.errors.length === 0) {
    console.log("Registrazione riuscita per " + username);
  } else {
    this.mostraErrori();
  }
};

RegisterController.register("mario", "123", ""); // "Errori: Email mancante, Password troppo corta"

// Ogni controller ha il proprio stato (errors) ma delega metodi comuni (mostraErrori, aggiungiErrore)
```

```javascript
/*
 * 10. Performance - Memoria Condivisa
 */

// ❌ INEFFICIENTE: metodi duplicati per ogni istanza
function PersonaInefficient(nome) {
  this.nome = nome;

  // Ogni istanza ha la sua COPIA della funzione
  this.saluta = function () {
    console.log("Ciao, sono " + this.nome);
  };
}

var p1 = new PersonaInefficient("Alice");
var p2 = new PersonaInefficient("Bob");

console.log(p1.saluta === p2.saluta); // false - funzioni diverse!
// Con 1000 persone, ci sono 1000 copie della funzione saluta

// ✅ EFFICIENTE: metodo sul prototipo, condiviso
function PersonaEfficiente(nome) {
  this.nome = nome;
}

PersonaEfficiente.prototype.saluta = function () {
  console.log("Ciao, sono " + this.nome);
};

var p3 = new PersonaEfficiente("Charlie");
var p4 = new PersonaEfficiente("Diana");

console.log(p3.saluta === p4.saluta); // true - stessa funzione!
// Con 1000 persone, c'è UNA SOLA copia della funzione saluta su prototype

// Risparmio memoria significativo con molte istanze
var mille = [];
for (var i = 0; i < 1000; i++) {
  mille.push(new PersonaEfficiente("Persona" + i));
}
// Tutte le 1000 istanze condividono PersonaEfficiente.prototype.saluta
```

---

## 4. Variabili

Un programma ha bisogno di "ricordare" dei valori che possono cambiare durante la sua esecuzione. Per fare ciò, si utilizzano le variabili: contenitori simbolici a cui viene assegnato un nome e che possono contenere dati. La funzione primaria delle variabili è gestire lo stato (state) del programma, ovvero tenere traccia dei valori mentre cambiano.

### Dichiarazione → let, const e var

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

#### Esempi di Codice

```javascript
/*
 * 1. Dichiarazione e uso base delle variabili
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
 * 2. Gestione dello stato del programma
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
 * 3. Differenza tra var, let e const (scope)
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

### Tipizzazione Dinamica (Dynamic Typing)

JavaScript è un linguaggio a tipizzazione dinamica. Questo significa che una variabile non è legata a un tipo di dato specifico. La stessa variabile può contenere un number in un momento, e una string in un momento successivo. Questa flessibilità permette di usare una singola variabile per rappresentare un valore che cambia forma nel corso del programma.

#### Esempi di Codice

```javascript
/*
 * 1. Tipizzazione dinamica - Cambio di tipo
 */

let valore = 42; // Number
console.log(typeof valore); // "number"

valore = "Ciao"; // String
console.log(typeof valore); // "string"

valore = true; // Boolean
console.log(typeof valore); // "boolean"

valore = { nome: "Mario" }; // Object
console.log(typeof valore); // "object"

valore = [1, 2, 3]; // Array (tipo object)
console.log(typeof valore); // "object"

valore = function () {
  return 42;
}; // Function
console.log(typeof valore); // "function"
```

```javascript
/*
 * 2. Esempio pratico - Variabile che cambia tipo durante l'esecuzione
 */

function elaboraDato(input) {
  let risultato;

  if (typeof input === "number") {
    risultato = input * 2; // risultato è un number
    console.log("Doppio:", risultato);
  } else if (typeof input === "string") {
    risultato = input.toUpperCase(); // risultato è una string
    console.log("Maiuscolo:", risultato);
  } else if (typeof input === "boolean") {
    risultato = input ? "Vero" : "Falso"; // risultato è una string
    console.log("Testo:", risultato);
  } else {
    risultato = null; // risultato è null
    console.log("Tipo non supportato");
  }

  return risultato;
}

elaboraDato(10); // "Doppio: 20"
elaboraDato("hello"); // "Maiuscolo: HELLO"
elaboraDato(true); // "Testo: Vero"
```

```javascript
/*
 * 3. Conversioni implicite (coercion)
 */

// JavaScript converte automaticamente i tipi quando necessario
let numero = 5;
let testo = "10";

// Concatenazione: numero viene convertito in stringa
console.log(numero + testo); // "510"

// Sottrazione: testo viene convertito in numero
console.log(testo - numero); // 5

// Confronto  con conversione
console.log("5" == 5); // true - uguaglianza con conversione
console.log("5" === 5); // false - uguaglianza stretta (tipo diverso)
```

```javascript
/*
 * 4. Array che contiene tipi misti
 */

let collezione = [42, "testo", true, { nome: "Mario" }, [1, 2, 3], null];

for (let item of collezione) {
  console.log(item, "->", typeof item);
}
// 42 -> number
// testo -> string
// true -> boolean
// { nome: 'Mario' } -> object
// [1, 2, 3] -> object
// null -> object (peculiarità di JavaScript)
```

```javascript
/*
 * 5. Vantaggi e svantaggi della tipizzazione dinamica
 */

// ✅ Vantaggio: Flessibilità
function stampa(valore) {
  console.log(valore); // Accetta qualsiasi tipo
}

stampa(42);
stampa("Hello");
stampa([1, 2, 3]);

// ⚠️ Svantaggio: Errori a runtime
function somma(a, b) {
  return a + b;
}

console.log(somma(5, 10)); // 15 - OK
console.log(somma("5", 10)); // "510" - concatenazione invece di somma!
console.log(somma(5, null)); // 5 - null diventa 0
console.log(somma(5, undefined)); // NaN - undefined non è convertibile

// ✅ Soluzione: Validazione esplicita
function sommaValidata(a, b) {
  if (typeof a !== "number" || typeof b !== "number") {
    throw new Error("Entrambi i parametri devono essere numeri");
  }
  return a + b;
}

console.log(sommaValidata(5, 10)); // 15
// console.log(sommaValidata("5", 10)); // Errore!
```

---

### Nomi delle Variabili e Identificatori

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
```

#### Convenzioni e Buone Pratiche

Oltre alle regole sintattiche, la comunità JavaScript segue delle convenzioni per scrivere codice più pulito e comprensibile:

- **Nomi Descrittivi** → Scegliere nomi che spieghino chiaramente lo scopo della variabile (es. prezzoUnitario invece di p). Evitare abbreviazioni ambigue.

- **Notazione camelCase** → È la convenzione standard in JavaScript. Si inizia con una lettera minuscola e si usa la maiuscola per l'inizio di ogni parola successiva, senza spazi (es. nomeUtente, calcolaPrezzoFinale).

- **Plurali per le Collezioni** → Usare un nome plurale per gli array o altre collezioni di dati, per indicare che contengono più elementi (es. utenti, prodotti).

#### Esempi di Codice

```javascript
/*
 * 1. Nomi descrittivi vs abbreviazioni
 */

// ❌ Nomi poco descrittivi
let p = 10;
let q = 5;
let t = p * q;

// ✅ Nomi descrittivi
let prezzoUnitario = 10;
let quantita = 5;
let totale = prezzoUnitario * quantita;
```

```javascript
/*
 * 2. Convenzioni di naming
 */

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
```

```javascript
/*
 * 3. Esempio completo con buone pratiche
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

  svuotaCarrello() {
    this._articoli = [];
  }

  getNumeroArticoli() {
    return this._articoli.length;
  }
}

// Utilizzo
const carrelloAcquisti = new GestoreCarrello();
carrelloAcquisti.aggiungiArticolo("Laptop", 999, 1);
carrelloAcquisti.aggiungiArticolo("Mouse", 29, 2);

console.log("Articoli:", carrelloAcquisti.getNumeroArticoli()); // 2
console.log("Totale:", carrelloAcquisti.calcolaTotaleCarrello()); // 1057
```

```javascript
/*
 * 4. Esempi di identificatori validi e creativi
 */

// Simboli speciali permessi
let $ = "jQuery style";
let _ = "Lodash style";
let $element = "riferimento elemento";
let _internal = "private by convention";

// Numeri dopo il primo carattere
let variabile1 = "prima";
let variabile2 = "seconda";
let temp123 = "temporanea";

// Unicode characters (non comuni ma validi)
let città = "Roma";
let età = 25;
let 名前 = "nome in giapponese"; // valido ma sconsigliato
```

```javascript
/*
 * 5. Parole riservate - Lista completa di esempi
 */

// Elenco delle principali parole riservate da evitare:
const ESEMPI_PAROLE_RISERVATE = [
  // Keywords
  "break",
  "case",
  "catch",
  "class",
  "const",
  "continue",
  "debugger",
  "default",
  "delete",
  "do",
  "else",
  "export",
  "extends",
  "finally",
  "for",
  "function",
  "if",
  "import",
  "in",
  "instanceof",
  "let",
  "new",
  "return",
  "super",
  "switch",
  "this",
  "throw",
  "try",
  "typeof",
  "var",
  "void",
  "while",
  "with",
  "yield",

  // Literals
  "null",
  "true",
  "false",
];

// Ma possono essere usate come proprietà
let syntax = {
  if: "conditional",
  for: "loop",
  class: "definition",
  return: "value",
};

console.log(syntax.if); // "conditional"
console.log(syntax["for"]); // "loop"
```

---

### Hoisting delle Variabili

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

#### Esempi di Codice

```javascript
/*
 * 1. VAR HOISTING - Dichiarazione sollevata, valore undefined
 */

function esempioVar() {
  console.log("Inizio funzione");
  console.log(messaggio); // undefined - NON un errore!

  var messaggio = "Ciao da var";

  console.log(messaggio); // "Ciao da var"
}

esempioVar();

// Il codice sopra viene interpretato così dal motore:
function esempioVarInterpretato() {
  var messaggio; // dichiarazione sollevata in cima

  console.log("Inizio funzione");
  console.log(messaggio); // undefined

  messaggio = "Ciao da var"; // assegnazione

  console.log(messaggio); // "Ciao da var"
}
```

```javascript
/*
 * 2. LET/CONST E TEMPORAL DEAD ZONE (TDZ)
 */

function esempioLet() {
  console.log("Inizio funzione");

  // ⚠️ TDZ inizia qui - 'nome' esiste ma non è accessibile

  // console.log(nome); // ❌ ReferenceError: Cannot access 'nome' before initialization

  let nome = "Mario"; // TDZ finisce qui

  console.log(nome); // ✅ "Mario"
}

function esempioConst() {
  // ⚠️ TDZ per LIMITE

  // console.log(LIMITE); // ❌ ReferenceError: Cannot access 'LIMITE' before initialization

  const LIMITE = 100; // TDZ finisce qui

  console.log(LIMITE); // ✅ 100

  // LIMITE = 200; // ❌ TypeError: Assignment to constant variable
}
```

```javascript
/*
 * 3. Hoisting in blocchi di codice
 */

function confrontoScope() {
  // VAR - function scope
  if (true) {
    var x = 10;
  }
  console.log(x); // ✅ 10 - var è accessibile fuori dal blocco

  // LET - block scope + TDZ
  if (true) {
    let y = 20;
  }
  // console.log(y); // ❌ ReferenceError - let ha block scope
}
```

```javascript
/*
 * 4. Esempio pratico: loop con var vs let
 */

// Problema comune con var
console.log("=== Loop con VAR ===");
for (var i = 0; i < 3; i++) {
  setTimeout(function () {
    console.log("var i:", i); // Stampa 3, 3, 3 (problema!)
  }, 100);
}
// i è ancora accessibile qui!
console.log("Dopo loop var, i =", i); // 3

// Soluzione con let
console.log("=== Loop con LET ===");
for (let j = 0; j < 3; j++) {
  setTimeout(function () {
    console.log("let j:", j); // Stampa 0, 1, 2 (corretto!)
  }, 100);
}
// console.log(j); // ❌ ReferenceError - j non è definito fuori dal loop
```

```javascript
/*
 * 5. Hoisting di funzioni vs variabili
 */

// Le FUNCTION DECLARATIONS vengono completamente "sollevate"
saluta(); // ✅ "Ciao!" - funziona anche prima della dichiarazione!

function saluta() {
  console.log("Ciao!");
}

// Le FUNCTION EXPRESSIONS seguono le regole delle variabili

// Con var: dichiarazione sollevata, valore undefined
// salutaConVar(); // ❌ TypeError: salutaConVar is not a function
var salutaConVar = function () {
  console.log("Ciao da var");
};
salutaConVar(); // ✅ Ora funziona

// Con let/const: TDZ
// salutaConLet(); // ❌ ReferenceError: Cannot access 'salutaConLet' before initialization
let salutaConLet = function () {
  console.log("Ciao da let");
};
salutaConLet(); // ✅ Ora funziona
```

```javascript
/*
 * 6. TDZ con parametri di default
 */

// ❌ TDZ anche con parametri
function parametriConTDZ(a = b, b = 2) {
  // b è nella TDZ quando viene valutato 'a'
  return a + b;
}

// parametriConTDZ(); // ❌ ReferenceError: Cannot access 'b' before initialization

// ✅ Ordine corretto
function parametriCorretti(b = 2, a = b) {
  // b è già dichiarato quando viene valutato 'a'
  return a + b;
}

console.log(parametriCorretti()); // 4
```

```javascript
/*
 * 7. Multiple var declarations - Altra stranezza
 */

var nome = "Mario";
var nome = "Luigi"; // ✅ Nessun errore con var!
console.log(nome); // "Luigi"

let cognome = "Rossi";
// let cognome = "Bianchi"; // ❌ SyntaxError: Identifier 'cognome' has already been declared
```

```javascript
/*
 * 8. Best practice: dichiarare sempre all'inizio dello scope
 */

function buonaPratica() {
  // ✅ Dichiarare tutte le variabili all'inizio dello scope
  let nome = "Mario";
  let eta = 30;
  const SCONTO = 0.1;
  let prezzoFinale;

  // Poi usarle
  console.log(`${nome} ha ${eta} anni`);

  prezzoFinale = 100 - 100 * SCONTO;
  console.log("Prezzo finale:", prezzoFinale);
}
```

```javascript
/*
 * 9. TDZ in azione - Visualizzazione
 */

function visualizzaTDZ() {
  // inizio TDZ per 'valore'
  console.log("Prima della dichiarazione");

  {
    // inizio TDZ per 'blocco'

    // console.log(blocco); // ❌ ReferenceError

    let blocco = "dentro"; // fine TDZ per 'blocco'
    console.log(blocco); // ✅ "dentro"
  }

  let valore = 42; // fine TDZ per 'valore'
  console.log(valore); // ✅ 42
}

visualizzaTDZ();
```

```javascript
/*
 * 10. Confronto riepilogativo
 */

console.log("=== CONFRONTO VAR vs LET/CONST ===");

// VAR
console.log(varTest); // undefined (hoisted)
var varTest = "var value";

// LET
// console.log(letTest); // ❌ ReferenceError (TDZ)
let letTest = "let value";

// CONST
// console.log(constTest); // ❌ ReferenceError (TDZ)
const constTest = "const value";

// Block scope
{
  var varBlock = "var in block";
  let letBlock = "let in block";
  const constBlock = "const in block";
}

console.log(varBlock); // ✅ "var in block" (function scoped)
// console.log(letBlock); // ❌ ReferenceError (block scoped)
// console.log(constBlock); // ❌ ReferenceError (block scoped)
```

---

### 4.4 Scope (Ambito)

**Tipo**: Nuovo Topic

Uno dei paradigmi fondamentali di quasi tutti i linguaggi di programmazione è la capacità di memorizzare valori in variabili, per poi recuperarli o modificarli in un secondo momento. Questa capacità di gestire i valori nelle variabili è ciò che conferisce a un programma uno stato (state). Senza questo concetto, un programma potrebbe eseguire solo compiti molto limitati e poco interessanti.

L'introduzione delle variabili in un programma solleva però delle domande cruciali: dove "vivono" queste variabili? In altre parole, dove vengono memorizzate? E, soprattutto, come fa il programma a trovarle quando ne ha bisogno?

Queste domande evidenziano la necessità di un insieme di regole ben definite, e questo insieme di regole prende il nome di Scope (ambito).

In programmazione, lo scope (tecnicamente lexical scope o ambito lessicale) definisce il contesto in cui una variabile è "visibile" e quindi accessibile. Si può pensare allo scope come all'inventario di un negozio: un commesso può vendere solo i prodotti presenti nel suo magazzino, non quelli di un altro negozio. Allo stesso modo, il codice può accedere solo alle variabili definite nel suo scope o in uno scope esterno (un "magazzino" più grande che lo contiene).

```javascript
// Esempio di visibilità delle variabili in scope diversi
function negozioA() {
  let prodottoA = "Laptop";
  console.log(prodottoA); // ✅ Accessibile (stesso scope)
  // console.log(prodottoB);  // ❌ Non accessibile (scope diverso)
}

function negozioB() {
  let prodottoB = "Mouse";
  console.log(prodottoB); // ✅ Accessibile
  // console.log(prodottoA);  // ❌ Non accessibile (scope diverso)
}

negozioA(); // Output: "Laptop"
negozioB(); // Output: "Mouse"
```

#### Metafora per comprendere lo scope

Per comprendere a fondo il concetto di Scope, è utile immaginarlo come il risultato di una conversazione tra tre attori principali che collaborano per elaborare un programma JavaScript. Ognuno ha un ruolo ben preciso.

Il cast di questi "personaggi" è il seguente:

- **Engine (Motore)** → È il responsabile principale dell'intero processo. Gestisce la compilazione e l'esecuzione del codice JavaScript dall'inizio alla fine. Potremmo vederlo come il "capo" che coordina tutte le operazioni.

- **Compiler (Compilatore)** → È uno stretto collaboratore dell'Engine. Si occupa di tutto il lavoro "sporco" di analizzare il codice (parsing) e generare la versione eseguibile (code-generation), come discusso in precedenza.

- **Scope** → È un altro amico dell'Engine. Il suo compito è quello di collezionare e mantenere una lista di tutte le variabili (o più in generale, gli "identificatori") che sono state dichiarate nel programma. Inoltre, applica un insieme rigoroso di regole per stabilire come e dove queste variabili siano accessibili dal codice in esecuzione in un dato momento. È in pratica il "guardiano" delle variabili.

Per capire veramente come funziona JavaScript, è necessario iniziare a pensare come pensano l'Engine e i suoi collaboratori, ponendosi le stesse domande che si pongono loro durante l'elaborazione del codice.

```javascript
// Simulazione della conversazione tra Engine, Compiler e Scope

// 1. FASE DI COMPILAZIONE
// Compiler analizza: let nome = "Mario";
// Compiler: "Scope, ho trovato una dichiarazione per l'identificatore 'nome'"
// Scope: "Ok, l'ho registrata nello scope globale"

let nome = "Mario";

// 2. FASE DI ESECUZIONE
// Engine esegue: console.log(nome);
// Engine: "Scope, hai una variabile chiamata 'nome'?"
// Scope: "Sì! Eccola: 'Mario'"
console.log(nome); // Output: "Mario"

// 3. VARIABILE NON DICHIARATA
// Engine: "Scope, hai una variabile chiamata 'cognome'?"
// Scope: "No, non la trovo"
// Engine: "Allora genero un ReferenceError"
// console.log(cognome);  // ❌ ReferenceError: cognome is not defined
```

#### Scope Globale e Scope Locale

In JavaScript, esistono principalmente due tipi di scope:

- **Scope Globale (Global Scope)** → Una variabile dichiarata al di fuori di qualsiasi funzione si trova nello scope globale. È accessibile da qualsiasi punto del programma, sia all'interno che all'esterno delle funzioni.

- **Scope Locale (Local Scope)** → Ogni funzione crea il proprio scope locale. Una variabile dichiarata al suo interno è accessibile solo all'interno di quella funzione.

```javascript
// SCOPE GLOBALE
let varGlobale = "Sono visibile ovunque";
const PI = 3.14;

function calcolaArea(raggio) {
  // SCOPE LOCALE della funzione calcolaArea
  let area = PI * raggio * raggio; // ✅ Può accedere a PI (scope esterno)
  let messaggio = "Area calcolata"; // Solo qui dentro

  console.log(varGlobale); // ✅ Può accedere allo scope globale
  console.log(area); // ✅ Può accedere al proprio scope locale

  return area;
}

function altrafunzione() {
  // SCOPE LOCALE di altrafunzione
  let altroMessaggio = "Altro scope";

  console.log(varGlobale); // ✅ Può accedere allo scope globale
  // console.log(area);  // ❌ ReferenceError: area appartiene a calcolaArea
  // console.log(messaggio);  // ❌ ReferenceError: messaggio appartiene a calcolaArea
}

console.log(varGlobale); // ✅ Accessibile (scope globale)
console.log(PI); // ✅ Accessibile (scope globale)
// console.log(area);  // ❌ ReferenceError: area è locale a calcolaArea
// console.log(messaggio);  // ❌ ReferenceError: messaggio è locale a calcolaArea

calcolaArea(5); // Output: "Sono visibile ovunque" e calcola l'area
```

```javascript
// Esempio pratico: contatore con scope
let contatoreGlobale = 0; // Tutti possono modificarlo

function incrementaGlobale() {
  contatoreGlobale++; // Modifica la variabile globale
  console.log("Globale:", contatoreGlobale);
}

function incrementaLocale() {
  let contatoreLocale = 0; // Variabile locale (riparte da 0 ogni volta)
  contatoreLocale++;
  console.log("Locale:", contatoreLocale);
}

incrementaGlobale(); // Globale: 1
incrementaGlobale(); // Globale: 2
incrementaGlobale(); // Globale: 3

incrementaLocale(); // Locale: 1
incrementaLocale(); // Locale: 1 (riparte sempre da 0!)
incrementaLocale(); // Locale: 1
```

#### Scope Annidato (Nested Scope)

Lo Scope non è quasi mai un singolo "universo"; al contrario, gli scope sono spesso annidati l'uno dentro l'altro, proprio come un blocco di codice o una funzione possono essere contenuti all'interno di un altro blocco o funzione.

Questo annidamento crea una catena di scope (o scope chain). Quando l'Engine ha bisogno di trovare una variabile e non la trova nello scope corrente, il suo comportamento è molto prevedibile:

1. Inizia la ricerca nello scope in cui si trova in quel momento.
2. Se non trova la variabile, "sale" di un livello e cerca nello scope immediatamente esterno che lo contiene.
3. Continua questo processo, salendo di livello in livello, finché non trova la variabile o finché non raggiunge lo scope più esterno di tutti: lo scope globale (global scope).
4. Se arriva allo scope globale e ancora non ha trovato la variabile, la ricerca si ferma.

```javascript
// Esempio base di ricerca nella scope chain
let a = 10; // Scope globale

function foo() {
  // 'a' non è dichiarato qui, ma foo può accedervi
  console.log(a + b); // Cerca 'a' (trova nel globale) e 'b' (trova nel globale)
}

let b = 20; // Scope globale
foo(); // Output: 30
```

Quando viene eseguita la riga `console.log(a + b)`, l'Engine ha bisogno di trovare il valore di `b`. La ricerca RHS (Right-Hand Side) per `b` non può essere soddisfatta all'interno della funzione `foo`, perché `b` non è stato dichiarato lì.

Ecco la conversazione che ne deriva tra Engine e i vari Scope:

- **Engine** → "Ehi, Scope di foo, conosci per caso b? Ho una ricerca RHS per lui."
- **Scope di foo** → "No, mai sentito. Prova più in alto."
- **Engine** → (Sale di un livello) "Ehi, Scope fuori da foo... ah, sei lo Scope globale, perfetto. Conosci b? Ho una ricerca RHS."
- **Scope globale** → "Sì, certo. Eccolo qui."

```javascript
// Esempio dettagliato della conversazione Engine-Scope
let nome = "Mario"; // Dichiarato nello scope globale

function saluta() {
  // Engine cerca 'nome':
  // 1. Engine: "Scope di saluta, hai 'nome'?"
  // 2. Scope di saluta: "No"
  // 3. Engine: "Scope globale, hai 'nome'?"
  // 4. Scope globale: "Sì! Ecco: 'Mario'"

  let messaggio = "Ciao"; // Dichiarato nello scope di saluta

  function completaSaluto() {
    // Engine cerca 'messaggio':
    // 1. Engine: "Scope di completaSaluto, hai 'messaggio'?"
    // 2. Scope di completaSaluto: "No"
    // 3. Engine: "Scope di saluta, hai 'messaggio'?"
    // 4. Scope di saluta: "Sì! Ecco: 'Ciao'"

    // Engine cerca 'nome':
    // 1. Scope di completaSaluto → No
    // 2. Scope di saluta → No
    // 3. Scope globale → Sì!

    console.log(messaggio + ", " + nome); // "Ciao, Mario"
  }

  completaSaluto();
}

saluta();
```

La regola per attraversare gli scope annidati è quindi molto semplice: l'Engine parte dallo scope corrente e, se non trova ciò che cerca, continua a salire lungo la catena degli scope, un livello alla volta, fino a raggiungere la cima (lo scope globale).

```javascript
// Scope chain con 3 livelli di annidamento
let a = "livello globale";

function esterna() {
  let b = "livello esterna";

  function interna() {
    let c = "livello interna";

    // interna può accedere a TUTTI gli scope esterni (scope chain)
    console.log(a); // ✅ "livello globale" (risale di 2 livelli)
    console.log(b); // ✅ "livello esterna" (risale di 1 livello)
    console.log(c); // ✅ "livello interna" (stesso scope)
  }

  interna();

  // esterna può accedere al globale, ma NON a interna
  console.log(a); // ✅ "livello globale"
  console.log(b); // ✅ "livello esterna"
  // console.log(c);  // ❌ ReferenceError: c is not defined
}

esterna();

// Lo scope globale NON può accedere agli scope interni
console.log(a); // ✅ "livello globale"
// console.log(b);  // ❌ ReferenceError: b is not defined
// console.log(c);  // ❌ ReferenceError: c is not defined
```

#### La Metafora dell'Edificio

Per visualizzare meglio il processo di risoluzione dello scope annidato, possiamo usare la metafora di un edificio a più piani.

Immaginiamo che questo edificio rappresenti l'insieme delle regole dello scope del nostro programma:

- Il **primo piano** (il piano terra) rappresenta lo scope corrente in cui ci troviamo in un dato momento dell'esecuzione.
- L'**ultimo piano** dell'edificio rappresenta lo scope globale.

Quando l'Engine deve risolvere una ricerca (sia LHS che RHS) per una variabile, il processo è simile a questo:

1. Inizia a cercare la variabile al piano corrente.
2. Se non la trova, prende l'ascensore e sale al piano successivo (lo scope immediatamente esterno) e cerca lì.
3. Continua a salire, piano dopo piano, ripetendo la ricerca.
4. Una volta raggiunto l'ultimo piano (lo scope globale), o trova finalmente quello che sta cercando, oppure no. In ogni caso, la sua ricerca termina lì. Non può andare oltre.

```javascript
// METAFORA DELL'EDIFICIO: Codice con 4 "piani"
// Piano 4 (Roof/Globale)
let piano4 = "Attico - Scope Globale";

function entraNelPalazzo() {
  // Piano 3
  let piano3 = "Terzo piano";

  function scendiAlSecondo() {
    // Piano 2
    let piano2 = "Secondo piano";

    function scendiAlPrimo() {
      // Piano 1 (Ground Floor)
      let piano1 = "Piano terra";

      // Dal piano terra, l'Engine può salire fino all'attico
      console.log(piano1); // ✅ Piano corrente
      console.log(piano2); // ✅ Sale di 1 piano
      console.log(piano3); // ✅ Sale di 2 piani
      console.log(piano4); // ✅ Sale di 3 piani (attico/globale)
    }

    scendiAlPrimo();

    // Dal secondo piano:
    console.log(piano2); // ✅ Piano corrente
    console.log(piano3); // ✅ Sale di 1 piano
    console.log(piano4); // ✅ Sale di 2 piani
    // console.log(piano1);  // ❌ Non può SCENDERE al piano terra
  }

  scendiAlSecondo();
}

entraNelPalazzo();
```

```javascript
// Esempio pratico: ricerca con fallback multipli
let configGlobale = {
  tema: "chiaro",
  lingua: "it",
};

function applicazione() {
  let configApp = {
    tema: "scuro", // Override del tema globale
  };

  function componente() {
    let configComponente = {
      animazioni: true,
    };

    function mostraImpostazioni() {
      // L'Engine cerca ogni proprietà risalendo la scope chain:

      // 1. Cerca 'animazioni' nello scope corrente → Non trovato
      // 2. Sale a 'componente' scope → ✅ Trovato!
      console.log("Animazioni:", configComponente.animazioni);

      // 1. Cerca 'tema' nello scope corrente → Non trovato
      // 2. Sale a 'componente' → Non trovato
      // 3. Sale a 'applicazione' → ✅ Trovato!
      console.log("Tema:", configApp.tema); // "scuro"

      // 1. Cerca 'lingua' nello scope corrente → Non trovato
      // 2. Sale a 'componente' → Non trovato
      // 3. Sale a 'applicazione' → Non trovato
      // 4. Sale allo scope globale → ✅ Trovato!
      console.log("Lingua:", configGlobale.lingua); // "it"
    }

    mostraImpostazioni();
  }

  componente();
}

applicazione();
// Output:
// Animazioni: true
// Tema: scuro
// Lingua: it
```

```javascript
// La scope chain si ferma al globale
function livello1() {
  let x = 10;

  function livello2() {
    // JavaScript cerca 'x':
    // 1. Cerca nello scope corrente (livello2) → Non trovato
    // 2. Risale al livello superiore (livello1) → ✅ Trovato!
    console.log(x); // 10

    // JavaScript cerca 'y':
    // 1. Cerca nello scope corrente (livello2) → Non trovato
    // 2. Risale al livello superiore (livello1) → Non trovato
    // 3. Risale allo scope globale → Non trovato
    // 4. ❌ ReferenceError: y is not defined
    // console.log(y);
  }

  livello2();
}

livello1();
```

```javascript
// Esempio pratico: scope chain con calcoli
let tassaGlobale = 0.22; // 22% IVA

function calcolaPrezzoFinale(prezzoBase) {
  let margine = 1.3; // 30% di margine

  function applicaTassa() {
    // applicaTassa può accedere a:
    // - tassaGlobale (scope globale, 2 livelli sopra)
    // - margine (scope di calcolaPrezzoFinale, 1 livello sopra)
    // - prezzoBase (parametro di calcolaPrezzoFinale, 1 livello sopra)

    let prezzoConMargine = prezzoBase * margine;
    let prezzoFinale = prezzoConMargine * (1 + tassaGlobale);

    return prezzoFinale;
  }

  return applicaTassa();
}

console.log(calcolaPrezzoFinale(100)); // 158.6
// Calcolo: 100 * 1.3 = 130 → 130 * 1.22 = 158.6
```

#### Il Pericolo delle Variabili Globali Accidentali

Un comportamento pericoloso di JavaScript (in modalità non-stretta) si verifica quando si assegna un valore a una variabile che non è stata formalmente dichiarata con var, let o const. In questo caso, JavaScript risale la catena degli scope fino in cima e, non trovando alcuna dichiarazione, crea una nuova variabile nello scope globale.

```javascript
// PERICOLO: Variabile globale accidentale
function esempio() {
  x = 10; // ❌ Nessuna dichiarazione (var/let/const)
  // JavaScript cerca 'x' nella scope chain:
  // 1. Non trova 'x' nello scope locale
  // 2. Non trova 'x' nello scope globale
  // 3. CREA AUTOMATICAMENTE 'x' nello scope globale
}

esempio();
console.log(x); // 10 ← Variabile globale creata accidentalmente!
console.log(window.x); // 10 (in ambienti browser)
```

```javascript
// Esempio del problema reale
function calcolaSconto(prezzo) {
  sconto = prezzo * 0.1; // ❌ Dimenticato 'let'
  return prezzo - sconto;
}

function calcolaTassa(prezzo) {
  sconto = prezzo * 0.05; // ❌ Dimenticato 'let', SOVRASCRIVE la stessa globale!
  return prezzo + sconto;
}

let totale1 = calcolaSconto(100); // sconto = 10 (globale)
console.log(totale1); // 90

let totale2 = calcolaTassa(100); // sconto = 5 (SOVRASCRIVE la globale!)
console.log(totale2); // 105

console.log(sconto); // 5 (variabile globale inquinata)
```

```javascript
// SOLUZIONE: Usare 'let' o 'const'
function calcolaScontoCorretto(prezzo) {
  let sconto = prezzo * 0.1; // ✅ Dichiarazione esplicita
  return prezzo - sconto;
}

function calcolaTassaCorretto(prezzo) {
  let sconto = prezzo * 0.05; // ✅ Scope locale, NON interferisce
  return prezzo + sconto;
}

let totale1 = calcolaScontoCorretto(100);
let totale2 = calcolaTassaCorretto(100);
// console.log(sconto);  // ❌ ReferenceError: sconto is not defined (come dovrebbe essere!)
```

Questa è considerata una pessima pratica perché "inquina" lo scope globale e può portare a bug difficili da tracciare, dove parti diverse del codice modificano involontariamente la stessa variabile globale.

La regola fondamentale è: dichiara sempre formalmente le tue variabili. L'uso dello "strict mode" (che vedremo più avanti) aiuta a prevenire questo problema, trasformando questi casi in errori.

```javascript
// STRICT MODE previene le variabili globali accidentali
"use strict";

function test() {
  y = 20; // ❌ ReferenceError: y is not defined
  // Strict mode IMPEDISCE la creazione automatica
}

// test();  // Errore!

// Soluzione corretta
function testCorretto() {
  let y = 20; // ✅ Dichiarazione esplicita
  console.log(y);
}

testCorretto(); // 20
```

#### Block Scope: let e const

Mentre var crea uno scope a livello di funzione, le parole chiave moderne let e const introducono il concetto di Block Scope. Una variabile dichiarata con let o const è confinata al blocco di codice {...} in cui è definita (ad esempio un if, un ciclo for o anche un blocco autonomo).

```javascript
// DIFFERENZA tra var, let e const rispetto al block scope

// Esempio 1: Blocco IF
if (true) {
  var varVariable = "var ignora i blocchi";
  let letVariable = "let rispetta i blocchi";
  const constVariable = "const rispetta i blocchi";
}

console.log(varVariable); // ✅ "var ignora i blocchi"
// console.log(letVariable);  // ❌ ReferenceError
// console.log(constVariable);  // ❌ ReferenceError

// Esempio 2: Blocco FOR
for (var i = 0; i < 3; i++) {
  // var è visibile FUORI dal loop
}
console.log(i); // ✅ 3 (var ignora block scope)

for (let j = 0; j < 3; j++) {
  // let è confinato AL loop
}
// console.log(j);  // ❌ ReferenceError

// Esempio 3: Blocco AUTONOMO
{
  var x = 10;
  let y = 20;
  const z = 30;
  console.log(x, y, z); // 10 20 30
}

console.log(x); // ✅ 10 (var ignora blocchi)
// console.log(y);  // ❌ ReferenceError
// console.log(z);  // ❌ ReferenceError
```

```javascript
// Problema pratico con VAR nei loop
console.log("--- Problema con VAR ---");
for (var i = 0; i < 3; i++) {
  setTimeout(function () {
    console.log("var:", i); // Stampa sempre 3!
  }, 100);
}
// Output dopo 100ms: "var: 3" "var: 3" "var: 3"
// Perché? 'i' è condivisa (function scope)

console.log("--- Soluzione con LET ---");
for (let j = 0; j < 3; j++) {
  setTimeout(function () {
    console.log("let:", j); // Stampa 0, 1, 2
  }, 100);
}
// Output dopo 100ms: "let: 0" "let: 1" "let: 2"
// Perché? Ogni iterazione ha il suo 'j' (block scope)
```

```javascript
// Block scope nelle funzioni
function testScope() {
  if (true) {
    var functionScoped = "Visibile in tutta la funzione";
    let blockScoped = "Visibile solo nel blocco if";
  }

  console.log(functionScoped); // ✅ "Visibile in tutta la funzione"
  // console.log(blockScoped);  // ❌ ReferenceError

  {
    let altroBlocco = "Solo qui";
    const COSTANTE = 42;
  }

  // console.log(altroBlocco);  // ❌ ReferenceError
  // console.log(COSTANTE);  // ❌ ReferenceError
}

testScope();
```

#### Shadowing

Lo shadowing si verifica quando una variabile dichiarata in uno scope locale ha lo stesso nome di una variabile in uno scope più esterno. In questo caso, la variabile locale "nasconde" o "mette in ombra" (shadows) quella esterna. All'interno dello scope locale, qualsiasi riferimento a quel nome di variabile utilizzerà la versione locale.

```javascript
// SHADOWING BASE
let x = "globale";

function esempio() {
  let x = "locale"; // "Shadows" la x globale
  console.log(x); // "locale" (usa la versione locale)
}

esempio();
console.log(x); // "globale" (la x globale NON è stata modificata)
```

```javascript
// SHADOWING MULTI-LIVELLO
let nome = "Scope Globale";

function livello1() {
  let nome = "Scope Livello 1"; // Shadows globale
  console.log("Livello 1:", nome); // "Scope Livello 1"

  function livello2() {
    let nome = "Scope Livello 2"; // Shadows livello1 (e globale)
    console.log("Livello 2:", nome); // "Scope Livello 2"

    function livello3() {
      let nome = "Scope Livello 3"; // Shadows livello2, livello1 e globale
      console.log("Livello 3:", nome); // "Scope Livello 3"
    }

    livello3();
    console.log("Dopo livello3:", nome); // "Scope Livello 2" (non modificato)
  }

  livello2();
  console.log("Dopo livello2:", nome); // "Scope Livello 1" (non modificato)
}

livello1();
console.log("Globale:", nome); // "Scope Globale" (non modificato)

/* Output:
Livello 1: Scope Livello 1
Livello 2: Scope Livello 2
Livello 3: Scope Livello 3
Dopo livello3: Scope Livello 2
Dopo livello2: Scope Livello 1
Globale: Scope Globale
*/
```

```javascript
// SHADOWING con BLOCCHI (let/const)
let valore = 100;

if (true) {
  let valore = 200; // Shadows valore esterna nel blocco if
  console.log("Nel blocco if:", valore); // 200

  {
    let valore = 300; // Shadows anche questa nel blocco più interno
    console.log("Nel blocco interno:", valore); // 300
  }

  console.log("Di nuovo nel blocco if:", valore); // 200
}

console.log("Fuori dai blocchi:", valore); // 100
```

```javascript
// SHADOWING: Errore comune da evitare
let contatore = 0;

function incrementa() {
  let contatore = 10; // ❌ Shadows! NON modifica quella globale
  contatore++;
  console.log("Dentro funzione:", contatore); // 11
}

incrementa();
console.log("Fuori funzione:", contatore); // 0 (NON modificata!)

// Soluzione: NON usare let se vuoi modificare quella esterna
function incrementaCorretto() {
  contatore++; // ✅ Modifica quella globale
  console.log("Dentro funzione:", contatore);
}

incrementaCorretto(); // 1
console.log("Fuori funzione:", contatore); // 1
```

```javascript
// REGOLA: Non puoi ri-dichiarare con let/const nello STESSO scope
let y = 10;
// let y = 20;  // ❌ SyntaxError: Identifier 'y' has already been declared

// Ma puoi farlo in SCOPE DIVERSI (shadowing)
{
  let y = 20; // ✅ OK, è uno scope diverso (shadowing)
  console.log(y); // 20

  {
    let y = 30; // ✅ OK, altro scope ancora
    console.log(y); // 30
  }

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
// ASSEGNAMENTO BASE
let x = 10; // Assegna il valore 10 alla variabile x
let nome = "Mario"; // Assegna la stringa "Mario" alla variabile nome
let attivo = true; // Assegna il booleano true

// OPERATORI DI ASSEGNAMENTO COMPOSTO
let punteggio = 100;
punteggio += 50; // Equivale a: punteggio = punteggio + 50
console.log(punteggio); // 150

let quantita = 20;
quantita *= 3; // Equivale a: quantita = quantita * 3
console.log(quantita); // 60

let budget = 1000;
budget -= 250; // Equivale a: budget = budget - 250
console.log(budget); // 750

let totale = 100;
totale /= 4; // Equivale a: totale = totale / 4
console.log(totale); // 25

let resto = 17;
resto %= 5; // Equivale a: resto = resto % 5
console.log(resto); // 2

let base = 2;
base **= 3; // Equivale a: base = base ** 3
console.log(base); // 8
```

```javascript
// ESEMPI PRATICI
function calcolaCarrello(prezzoIniziale, scontoPercentuale, tasse) {
  let totale = prezzoIniziale;

  // Applica sconto
  totale -= (totale * scontoPercentuale) / 100;

  // Aggiungi tasse
  totale += (totale * tasse) / 100;

  return totale;
}

console.log(calcolaCarrello(100, 10, 22)); // 98.78

// Contatori
let visitatori = 0;
visitatori += 1; // Incrementa di 1
visitatori += 5; // Incrementa di 5
console.log(visitatori); // 6

// Concatenazione di stringhe
let messaggio = "Benvenuto";
messaggio += " ";
messaggio += "utente!";
console.log(messaggio); // "Benvenuto utente!"
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
// ADDIZIONE
let somma = 5 + 3; // 8
let totale = 10 + 20 + 30; // 60

// CONCATENAZIONE DI STRINGHE (+ con stringhe)
let saluto = "Ciao" + " " + "mondo"; // "Ciao mondo"
let messaggio = "Il risultato è: " + 42; // "Il risultato è: 42"
let mix = "Ho " + 5 + " mele"; // "Ho 5 mele"
let attenzione = 5 + 5 + " mele"; // "10 mele" (prima calcola 5+5, poi concatena)

// SOTTRAZIONE
let differenza = 10 - 4; // 6
let negativo = 5 - 10; // -5

// MOLTIPLICAZIONE
let prodotto = 6 * 7; // 42
let doppio = 15 * 2; // 30

// DIVISIONE
let quoziente = 20 / 4; // 5
let meta = 9 / 2; // 4.5 (JavaScript restituisce decimali)
let infinito = 5 / 0; // Infinity

// RESTO (REMAINDER) %
let resto = 17 % 5; // 2 (17 = 5*3 + 2)
let restoDue = 20 % 3; // 2 (20 = 3*6 + 2)

// Uso pratico: verificare pari/dispari
let numero = 10;
if (numero % 2 === 0) {
  console.log("Pari"); // ✅
} else {
  console.log("Dispari");
}

// ESPONENZIAZIONE **
let quadrato = 5 ** 2; // 25 (5 elevato alla 2)
let cubo = 2 ** 3; // 8 (2 elevato alla 3)
let potenza = 10 ** 6; // 1000000
```

```javascript
// INCREMENTO ++ e DECREMENTO --
let contatore = 0;
contatore++; // contatore diventa 1 (post-incremento)
contatore++; // contatore diventa 2
console.log(contatore); // 2

let countdown = 10;
countdown--; // countdown diventa 9 (post-decremento)
countdown--; // countdown diventa 8
console.log(countdown); // 8

// POST-INCREMENTO (a++) vs PRE-INCREMENTO (++a)
let a = 5;
let b = a++; // b riceve 5, poi a diventa 6
console.log(a); // 6
console.log(b); // 5

let c = 5;
let d = ++c; // c diventa 6, poi d riceve 6
console.log(c); // 6
console.log(d); // 6

// POST-DECREMENTO (a--) vs PRE-DECREMENTO (--a)
let x = 10;
let y = x--; // y riceve 10, poi x diventa 9
console.log(x, y); // 9, 10

let m = 10;
let n = --m; // m diventa 9, poi n riceve 9
console.log(m, n); // 9, 9
```

```javascript
// ESEMPI PRATICI
function calcolaArea(raggio) {
  return 3.14 * raggio ** 2; // area = π * r²
}
console.log(calcolaArea(5)); // 78.5

function convertiTemperatura(celsius) {
  return (celsius * 9) / 5 + 32; // Formula C° → F°
}
console.log(convertiTemperatura(25)); // 77

// Ciclo con incremento
for (let i = 0; i < 5; i++) {
  console.log("Iterazione:", i);
}
// Output: 0, 1, 2, 3, 4

// Alternanza con modulo
for (let i = 0; i < 6; i++) {
  if (i % 2 === 0) {
    console.log(i + " è pari");
  } else {
    console.log(i + " è dispari");
  }
}
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
// === UGUAGLIANZA STRETTA (confronta tipo E valore)
console.log(5 === 5); // true (stesso tipo, stesso valore)
console.log(5 === "5"); // false (numero vs stringa)
console.log(true === 1); // false (booleano vs numero)
console.log(false === 0); // false (booleano vs numero)
console.log(null === undefined); // false (tipi diversi)
console.log("ciao" === "ciao"); // true

// == UGUAGLIANZA LASCA (converte i tipi prima di confrontare)
console.log(5 == "5"); // true (stringa "5" convertita a numero 5)
console.log(true == 1); // true (true convertito a 1)
console.log(false == 0); // true (false convertito a 0)
console.log(null == undefined); // true (caso speciale ES1)
console.log("" == 0); // true (stringa vuota convertita a 0)
console.log(" " == 0); // true (stringa con solo spazi → 0)

// CASI INGANNEVOLI con == (da evitare)
console.log(false == ""); // true ⚠️
console.log(false == []); // true ⚠️
console.log("" == 0); // true ⚠️
console.log(0 == []); // true ⚠️
console.log("0" == []); // false ⚠️
console.log([] == []); // false (riferimenti diversi)

// ❌ Evita == quando coinvolti: true, false, 0, "", []
```

```javascript
// QUANDO == È SICURO E UTILE
// Caso 1: Confrontare stringhe e numeri (intenzionale)
let input = "42";
if (input == 42) {
  // ✅ Sicuro: confronta valore
  console.log("Input valido");
}

// Caso 2: Verificare null O undefined con una sola condizione
let valore = null;
if (valore == null) {
  // ✅ Cattura sia null che undefined
  console.log("Valore non definito");
}
// Equivalente ma più prolisso:
if (valore === null || valore === undefined) {
  console.log("Valore non definito");
}

function processaDato(dato) {
  // Controlla se dato è null o undefined
  if (dato == null) {
    return "Dato mancante";
  }
  return "Dato presente: " + dato;
}

console.log(processaDato(null)); // "Dato mancante"
console.log(processaDato(undefined)); // "Dato mancante"
console.log(processaDato(0)); // "Dato presente: 0" (0 è valido!)
console.log(processaDato("")); // "Dato presente: " (stringa vuota valida!)
```

```javascript
// OPERATORI DI NON UGUAGLIANZA
// !== (non uguale stretta)
console.log(5 !== "5"); // true (tipi diversi)
console.log(5 !== 5); // false

// != (non uguale lasca)
console.log(5 != "5"); // false (5 == "5" è true, quindi != è false)
console.log(5 != 6); // true

// ESEMPI PRATICI
function validaEta(eta) {
  // Usa === per controllo rigoroso
  if (eta === "") {
    return "Età non inserita";
  }
  if (typeof eta !== "number") {
    return "Età deve essere un numero";
  }
  if (eta < 0 || eta > 120) {
    return "Età non valida";
  }
  return "Età valida";
}

console.log(validaEta(25)); // "Età valida"
console.log(validaEta("25")); // "Età deve essere un numero"
console.log(validaEta("")); // "Età non inserita"

// Confronto sicuro con ===
let password = "12345";
let confermaPassword = "12345";
if (password === confermaPassword) {
  console.log("Password confermata");
}
```

#### Confronto tra Oggetti e Array

Quando si confrontano valori non primitivi come oggetti o array, sia `==` che `===` si comportano allo stesso modo: controllano se le due variabili puntano allo stesso riferimento in memoria, non se il loro contenuto è identico.

```javascript
// ARRAY: confronto per riferimento, non per contenuto
let arr1 = [1, 2, 3];
let arr2 = [1, 2, 3];
let arr3 = arr1; // arr3 punta allo stesso array di arr1

console.log(arr1 === arr2); // false (array diversi in memoria)
console.log(arr1 === arr3); // true (stesso riferimento)
console.log(arr1 == arr2); // false (anche == confronta riferimenti)

// Modifica tramite riferimento
arr3.push(4);
console.log(arr1); // [1, 2, 3, 4] (arr1 modificato!)
console.log(arr3); // [1, 2, 3, 4] (arr3 è lo stesso array)

// OGGETTI: stesso comportamento degli array
let obj1 = { nome: "Mario", eta: 30 };
let obj2 = { nome: "Mario", eta: 30 };
let obj3 = obj1; // obj3 punta allo stesso oggetto

console.log(obj1 === obj2); // false (oggetti diversi)
console.log(obj1 === obj3); // true (stesso riferimento)
console.log(obj1 == obj2); // false (anche == confronta riferimenti)

// Modifica tramite riferimento
obj3.eta = 31;
console.log(obj1.eta); // 31 (obj1 modificato!)
```

```javascript
// PER CONFRONTARE IL CONTENUTO: serve logica personalizzata

// Confronto array semplice
function arrayUguali(a, b) {
  if (a.length !== b.length) return false;
  for (let i = 0; i < a.length; i++) {
    if (a[i] !== b[i]) return false;
  }
  return true;
}

console.log(arrayUguali([1, 2, 3], [1, 2, 3])); // true
console.log(arrayUguali([1, 2, 3], [1, 2, 4])); // false

// Confronto oggetti semplice (solo proprietà dirette)
function oggettiUguali(a, b) {
  let keysA = Object.keys(a);
  let keysB = Object.keys(b);

  if (keysA.length !== keysB.length) return false;

  for (let key of keysA) {
    if (a[key] !== b[key]) return false;
  }
  return true;
}

let persona1 = { nome: "Luigi", eta: 25 };
let persona2 = { nome: "Luigi", eta: 25 };
let persona3 = { nome: "Luigi", eta: 26 };

console.log(oggettiUguali(persona1, persona2)); // true
console.log(oggettiUguali(persona1, persona3)); // false

// Uso di JSON.stringify (attenzione: non affidabile al 100%)
let a = { x: 1, y: 2 };
let b = { y: 2, x: 1 }; // stesse proprietà, ordine diverso

console.log(JSON.stringify(a) === JSON.stringify(b)); // false ⚠️
// L'ordine delle chiavi può variare!
```

#### Disuguaglianza (Operatori Relazionali)

Gli operatori `<`, `>`, `<=` e `>=` vengono usati per i confronti di disuguaglianza. A differenza degli operatori di uguaglianza, non esiste una versione "stretta" che eviti la coercizione.

Il loro comportamento dipende dal tipo di valori confrontati:

- Se entrambi i valori sono stringhe, il confronto avviene in ordine alfabetico (lessicografico).
- In quasi tutti gli altri casi, JavaScript tenta di convertire entrambi i valori in numeri prima di confrontarli.

Un'insidia comune si presenta quando un valore non può essere convertito in un numero valido, risultando in NaN (Not a Number). Per specifica, NaN non è né maggiore, né minore, né uguale a nessun altro valore.

```javascript
// CONFRONTO NUMERICO
console.log(10 > 5); // true
console.log(3 < 8); // true
console.log(7 >= 7); // true (maggiore o uguale)
console.log(4 <= 3); // false

let eta = 18;
if (eta >= 18) {
  console.log("Maggiorenne");
}

let punteggio = 75;
if (punteggio > 60) {
  console.log("Promosso");
}

// CONFRONTO LESSICOGRAFICO (stringhe)
console.log("apple" < "banana"); // true (a < b in alfabeto)
console.log("zebra" > "aardvark"); // true (z > a)
console.log("Mario" < "Luigi"); // false (M > L)
console.log("cane" < "cani"); // true ("cane" è prefisso di "cani")

// Attenzione: confronto carattere per carattere
console.log("10" < "9"); // true ⚠️ ("1" < "9" come caratteri)
console.log("100" < "20"); // true ⚠️ ("1" < "2")
```

```javascript
// COERCIZIONE NUMERICA (stringa → numero)
console.log("42" > 10); // true (stringa "42" convertita a numero 42)
console.log("100" < 50); // false (stringa "100" → numero 100)
console.log("5" >= 5); // true

// Confronto misto: almeno un numero → converte tutto a numero
console.log(5 > "3"); // true (stringa "3" → numero 3)
console.log(10 <= "20"); // true

// CASI SPECIALI E PROBLEMI
// Problema 1: NaN
let risultato = "ciao" - 5; // NaN (operazione non valida)
console.log(risultato); // NaN
console.log(risultato > 0); // false
console.log(risultato < 0); // false
console.log(risultato >= 0); // false
console.log(risultato <= 0); // false
console.log(risultato == risultato); // false (NaN !== NaN)
console.log(isNaN(risultato)); // true ✅ Modo corretto per verificare NaN

// Problema 2: null
console.log(null > 0); // false (null → 0, ma 0 > 0 è false)
console.log(null == 0); // false (null == solo null o undefined)
console.log(null >= 0); // true ⚠️ (null → 0, e 0 >= 0 è true)

// Problema 3: undefined
console.log(undefined > 0); // false (undefined → NaN)
console.log(undefined < 0); // false
console.log(undefined >= 0); // false
console.log(undefined == 0); // false
```

```javascript
// ESEMPI PRATICI
function classificaPunteggio(punti) {
  if (punti >= 90) {
    return "Eccellente";
  } else if (punti >= 70) {
    return "Buono";
  } else if (punti >= 60) {
    return "Sufficiente";
  } else {
    return "Insufficiente";
  }
}

console.log(classificaPunteggio(95)); // "Eccellente"
console.log(classificaPunteggio(75)); // "Buono"
console.log(classificaPunteggio(50)); // "Insufficiente"

// Ordinamento alfabetico
let nomi = ["Zebra", "Mario", "Anna", "Luigi"];
nomi.sort();
console.log(nomi); // ["Anna", "Luigi", "Mario", "Zebra"]

// Verifica range
function èInRange(valore, min, max) {
  return valore >= min && valore <= max;
}

console.log(èInRange(5, 1, 10)); // true
console.log(èInRange(15, 1, 10)); // false

// Validazione età
function puòGuidare(eta) {
  if (typeof eta !== "number" || isNaN(eta)) {
    return false;
  }
  return eta >= 18 && eta <= 100;
}

console.log(puòGuidare(25)); // true
console.log(puòGuidare(15)); // false
console.log(puòGuidare("venti")); // false
```

### Operatori Logici (Logical)

Combinano espressioni booleane.

- `&&` (AND) → true solo se entrambe le condizioni sono vere.
- `||` (OR) → true se almeno una condizione è vera.
- `!` (NOT) → Inverte un valore booleano (true diventa false e viceversa).

Questi operatori usano il cortocircuito (short-circuit evaluation): `&&` si ferma se la prima condizione è falsa, mentre `||` si ferma se la prima è vera. Questo permette di scrivere codice più efficiente e conciso.

```javascript
// && (AND LOGICO) - true solo se TUTTI sono true
console.log(true && true); // true
console.log(true && false); // false
console.log(false && true); // false
console.log(false && false); // false

let eta = 25;
let haPatente = true;
if (eta >= 18 && haPatente) {
  console.log("Può guidare"); // ✅ Entrambe le condizioni vere
}

// Esempio pratico AND
function puòAccedere(utente) {
  return utente.attivo && utente.verificato && !utente.bannato;
}

let utente1 = { attivo: true, verificato: true, bannato: false };
let utente2 = { attivo: true, verificato: false, bannato: false };
console.log(puòAccedere(utente1)); // true
console.log(puòAccedere(utente2)); // false

// || (OR LOGICO) - true se ALMENO UNO è true
console.log(true || false); // true
console.log(false || true); // true
console.log(true || true); // true
console.log(false || false); // false

let isWeekend = true;
let isFestivo = false;
if (isWeekend || isFestivo) {
  console.log("Non si lavora"); // ✅ Almeno una condizione vera
}

// Esempio pratico OR
function haScontoSpeciale(cliente) {
  return cliente.èPremium || cliente.primoAcquisto || cliente.compleanno;
}

let cliente1 = { èPremium: false, primoAcquisto: true, compleanno: false };
let cliente2 = { èPremium: false, primoAcquisto: false, compleanno: false };
console.log(haScontoSpeciale(cliente1)); // true
console.log(haScontoSpeciale(cliente2)); // false
```

```javascript
// ! (NOT LOGICO) - Inverte il valore booleano
console.log(!true); // false
console.log(!false); // true
console.log(!!true); // true (doppio NOT torna al valore originale)

let piove = false;
if (!piove) {
  console.log("Si può uscire senza ombrello"); // ✅
}

let èConnesso = true;
if (!èConnesso) {
  console.log("Errore: nessuna connessione");
} else {
  console.log("Connesso"); // ✅
}

// NOT con valori non booleani
console.log(!""); // true (stringa vuota è falsy)
console.log(!0); // true (0 è falsy)
console.log(!"testo"); // false (stringa non vuota è truthy)
console.log(!null); // true
console.log(!undefined); // true
```

```javascript
// SHORT-CIRCUIT EVALUATION (cortocircuito)
// && si ferma al primo falsy
console.log(false && "qualsiasi cosa"); // false (non valuta il secondo)
console.log(true && "valore"); // "valore"
console.log(null && eseguiQualcosa()); // null (eseguiQualcosa() NON viene chiamata)

let utente = null;
let nomeUtente = utente && utente.nome; // null (si ferma a utente)
console.log(nomeUtente); // null (evita errore: Cannot read property 'nome' of null)

// || si ferma al primo truthy
console.log(true || "qualsiasi cosa"); // true (non valuta il secondo)
console.log(false || "valore"); // "valore"
console.log("" || "default"); // "default"
console.log(null || "fallback"); // "fallback"

// Usa || per valori di default (ma attenzione ai falsy validi!)
let nome = "";
let nomeVisualizzato = nome || "Ospite"; // "Ospite" (anche se "" potrebbe essere valido)
console.log(nomeVisualizzato);

let punteggio = 0;
let punteggioMostrato = punteggio || 100; // 100 ⚠️ (0 è falsy, ma valido!)
console.log(punteggioMostrato);
```

```javascript
// COMBINAZIONI COMPLESSE
let temperatura = 25;
let soleggiato = true;
let weekend = true;

// AND ha precedenza su OR
if ((temperatura > 20 && soleggiato) || weekend) {
  console.log("Bella giornata"); // ✅
}

// Equivalente a:
let èBelTempo = temperatura > 20 && soleggiato;
if (èBelTempo || weekend) {
  console.log("Bella giornata");
}

// Uso pratico: validazione form
function validaForm(form) {
  if (!form.nome || !form.email) {
    return "Nome ed email sono obbligatori";
  }
  if (form.eta && (form.eta < 0 || form.eta > 120)) {
    return "Età non valida";
  }
  if (form.password && form.password.length < 8) {
    return "Password troppo corta";
  }
  return "Form valido";
}

console.log(validaForm({ nome: "Mario", email: "m@test.it" })); // "Form valido"
console.log(validaForm({ nome: "Mario" })); // "Nome ed email sono obbligatori"
console.log(validaForm({ nome: "Mario", email: "m@test.it", eta: 150 })); // "Età non valida"

// Uso pratico: accesso sicuro alle proprietà
function ottieniCitta(persona) {
  return persona && persona.indirizzo && persona.indirizzo.citta;
}

let p1 = { nome: "Mario", indirizzo: { citta: "Roma", via: "X" } };
let p2 = { nome: "Luigi" };
let p3 = null;

console.log(ottieniCitta(p1)); // "Roma"
console.log(ottieniCitta(p2)); // undefined (si ferma a persona.indirizzo)
console.log(ottieniCitta(p3)); // null (si ferma a persona)
```

### Operatore Condizionale (Ternario)

L'operatore ternario (`? :`) è una scorciatoia per un'istruzione if-else. La sua sintassi è:

`condizione ? valore_se_vero : valore_se_falso`

```javascript
// ESEMPIO BASE
let eta = 20;
let tipo = eta >= 18 ? "adulto" : "minore";
console.log(tipo); // "adulto"

// Equivalente if-else:
let tipoAlt;
if (eta >= 18) {
  tipoAlt = "adulto";
} else {
  tipoAlt = "minore";
}
console.log(tipoAlt); // "adulto"

// USO IN ESPRESSIONI
let punteggio = 85;
console.log("Hai " + (punteggio >= 60 ? "superato" : "fallito") + " l'esame");
// Output: "Hai superato l'esame"

let nome = "Mario";
let saluto = "Ciao " + (nome ? nome : "ospite");
console.log(saluto); // "Ciao Mario"

// IN ASSEGNAMENTI
let isWeekend = true;
let sveglia = isWeekend ? "09:00" : "07:00";
console.log("Sveglia alle " + sveglia); // "Sveglia alle 09:00"

let temperatura = 30;
let abbigliamento = temperatura > 25 ? "T-shirt" : "Maglione";
console.log(abbigliamento); // "T-shirt"
```

```javascript
// TERNARI ANNIDATI (usare con cautela per leggibilità)
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

// Più leggibile come if-else-if:
let giudizioAlt;
if (voto >= 90) {
  giudizioAlt = "Eccellente";
} else if (voto >= 70) {
  giudizioAlt = "Buono";
} else if (voto >= 60) {
  giudizioAlt = "Sufficiente";
} else {
  giudizioAlt = "Insufficiente";
}

// CASI D'USO PRATICI
function calcolaTotale(prezzo, isPremium) {
  let sconto = isPremium ? 0.2 : 0.1; // 20% o 10%
  return prezzo * (1 - sconto);
}
console.log(calcolaTotale(100, true)); // 80
console.log(calcolaTotale(100, false)); // 90

// Rendering condizionale (pattern comune)
function mostraMessaggio(utente) {
  return utente ? "Benvenuto " + utente.nome : "Fai il login";
}
console.log(mostraMessaggio({ nome: "Mario" })); // "Benvenuto Mario"
console.log(mostraMessaggio(null)); // "Fai il login"

// Classi CSS condizionali (in frontend)
let isAttivo = true;
let className = "bottone " + (isAttivo ? "attivo" : "disattivo");
console.log(className); // "bottone attivo"

// Valori di default
function saluta(nome) {
  return "Ciao " + (nome ? nome : "ospite");
}
console.log(saluta("Luigi")); // "Ciao Luigi"
console.log(saluta()); // "Ciao ospite"

// Validazione inline
let password = "12345";
let messaggioPassword =
  password.length >= 8 ? "Password valida" : "Password troppo corta";
console.log(messaggioPassword); // "Password troppo corta"
```

### Operatore di Coalescenza Nullish (??)

Questo operatore restituisce il valore a destra solo se quello a sinistra è `null` o `undefined`. È perfetto per assegnare valori di default, perché a differenza di `||`, non scarta valori falsy validi come `0` o una stringa vuota `""`.

```javascript
// PROBLEMA CON || (scarta valori falsy validi)
let contatore = 0;
let valore1 = contatore || 10; // 10 ⚠️ (0 è falsy, usa il default)
console.log(valore1); // 10 (Ma 0 è un valore valido!)

let stringa = "";
let testo1 = stringa || "default"; // "default" ⚠️ (stringa vuota è falsy)
console.log(testo1); // "default" (Ma "" potrebbe essere valida!)

// SOLUZIONE CON ?? (controlla SOLO null/undefined)
let contatore2 = 0;
let valore2 = contatore2 ?? 10; // 0 ✅ (0 non è null/undefined)
console.log(valore2); // 0 (Corretto!)

let stringa2 = "";
let testo2 = stringa2 ?? "default"; // "" ✅ (stringa vuota è valida)
console.log(testo2); // "" (Corretto!)

// CONFRONTO DIRETTO
let numero = 0;
console.log(numero || 100); // 100 (|| tratta 0 come falsy)
console.log(numero ?? 100); // 0 (!! accetta 0 come valido)

let testoVuoto = "";
console.log(testoVuoto || "nessun testo"); // "nessun testo"
console.log(testoVuoto ?? "nessun testo"); // ""

let valoreNull = null;
console.log(valoreNull || "default"); // "default"
console.log(valoreNull ?? "default"); // "default" (stesso comportamento)

let valoreUndefined = undefined;
console.log(valoreUndefined || "default"); // "default"
console.log(valoreUndefined ?? "default"); // "default" (stesso comportamento)
```

```javascript
// VALORI FALSY: come vengono trattati
// Falsy values: false, 0, "", null, undefined, NaN

// Con ||
console.log(false || "default"); // "default"
console.log(0 || "default"); // "default"
console.log("" || "default"); // "default"
console.log(null || "default"); // "default"
console.log(undefined || "default"); // "default"
console.log(NaN || "default"); // "default"

// Con ??
console.log(false ?? "default"); // false ✅
console.log(0 ?? "default"); // 0 ✅
console.log("" ?? "default"); // "" ✅
console.log(null ?? "default"); // "default"
console.log(undefined ?? "default"); // "default"
console.log(NaN ?? "default"); // NaN ✅
```

```javascript
// USO PRATICO: configurazioni con valori di default
function creaConfigurazione(opzioni) {
  // Permette timeout: 0 (valore valido)
  let config = {
    timeout: opzioni.timeout ?? 3000, // Default 3000ms
    maxRetry: opzioni.maxRetry ?? 3, // Default 3 tentativi
    debug: opzioni.debug ?? false, // Default false
    messaggio: opzioni.messaggio ?? "Caricamento...", // Default
  };
  return config;
}

// Timeout 0 è un valore valido!
console.log(creaConfigurazione({ timeout: 0 }));
// { timeout: 0, maxRetry: 3, debug: false, messaggio: "Caricamento..." }

console.log(creaConfigurazione({}));
// { timeout: 3000, maxRetry: 3, debug: false, messaggio: "Caricamento..." }

console.log(creaConfigurazione({ timeout: 5000, maxRetry: 5 }));
// { timeout: 5000, maxRetry: 5, debug: false, messaggio: "Caricamento..." }

// Esempio pratico: paginazione
function ottieniPagina(numeroPagina, elementiPerPagina) {
  let pagina = numeroPagina ?? 1; // Default pagina 1
  let perPagina = elementiPerPagina ?? 10; // Default 10 elementi
  // Nota: pagina 0 è valida, quindi ?? è perfetto
  return { pagina, perPagina };
}

console.log(ottieniPagina(0, 20)); // { pagina: 0, perPagina: 20 }
console.log(ottieniPagina(null, 20)); // { pagina: 1, perPagina: 20 }

// Esempio: form con campi opzionali
function processaForm(dati) {
  return {
    nome: dati.nome ?? "Sconosciuto",
    cognome: dati.cognome ?? "",
    età: dati.età ?? null, // null se non fornita
    bio: dati.bio ?? "", // stringa vuota è valida
  };
}

console.log(processaForm({ nome: "Mario", età: 0 }));
// { nome: "Mario", cognome: "", età: 0, bio: "" }
// età: 0 è preservata (neonato!)

console.log(processaForm({}));
// { nome: "Sconosciuto", cognome: "", età: null, bio: "" }
```

### L'idioma del Doppio NOT (!!)

`!!` non è un operatore, ma un modo di usare l'operatore `!` due volte per convertire esplicitamente qualsiasi valore nel suo equivalente booleano. È una tecnica per verificare se un valore è truthy (cioè si comporta come true) o falsy (false, 0, "", null, undefined, NaN).

```javascript
// VALORI TRUTHY convertiti a true
console.log(!!"Hello"); // true (stringa non vuota)
console.log(!!42); // true (numero diverso da 0)
console.log(!!-1); // true (numero negativo)
console.log(!![]); // true (array vuoto è truthy!)
console.log(!!{}); // true (oggetto vuoto è truthy!)
console.log(!!" "); // true (stringa con spazio)
console.log(!!new Date()); // true (oggetto Date)
console.log(!!function () {}); // true (funzione)

// VALORI FALSY convertiti a false
console.log(!!false); // false
console.log(!!0); // false
console.log(!!-0); // false
console.log(!!""); // false (stringa vuota)
console.log(!!null); // false
console.log(!!undefined); // false
console.log(!!NaN); // false

// COME FUNZIONA
let valore = "testo";
console.log(valore); // "testo" (valore originale)
console.log(!valore); // false (primo NOT: da truthy a false)
console.log(!!valore); // true (secondo NOT: da false a true)

let numero = 0;
console.log(numero); // 0
console.log(!numero); // true (primo NOT: da falsy a true)
console.log(!!numero); // false (secondo NOT: da true a false)
```

```javascript
// USO PRATICO: conversione esplicita a boolean
function haValore(x) {
  return !!x; // Converte a booleano
}

console.log(haValore("test")); // true
console.log(haValore("")); // false
console.log(haValore(0)); // false
console.log(haValore(42)); // true
console.log(haValore(null)); // false
console.log(haValore(undefined)); // false
console.log(haValore([])); // true (array vuoto è truthy!)
console.log(haValore({})); // true (oggetto vuoto è truthy!)

// ALTERNATIVA PIÙ ESPLICITA: Boolean()
function haValoreAlt(x) {
  return Boolean(x); // Stesso risultato di !!x
}

console.log(Boolean("test")); // true
console.log(Boolean("")); // false
console.log(Boolean(0)); // false

// Equivalenti:
console.log(!!"ciao" === Boolean("ciao")); // true
console.log(!!0 === Boolean(0)); // true
```

```javascript
// QUANDO USARE !!
// Caso 1: Return esplicito di booleano
function èValido(input) {
  return !!input; // Esplicita che ritorna boolean
}

// Caso 2: Assegnamento booleano
let isLoggedIn = !!localStorage.getItem("userId");
let hasData = !!document.querySelector(".element");

// Caso 3: In filtri o map
let valori = [0, 1, 2, "", "ciao", null, 3];
let booleani = valori.map((v) => !!v);
console.log(booleani); // [false, true, true, false, true, false, true]

// Filtra solo valori truthy
let truthy = valori.filter((v) => !!v);
console.log(truthy); // [1, 2, "ciao", 3]

// QUANDO NON SERVE !!
// In condizioni if/while, la conversione è automatica
let input = "dati";
if (input) {
  // ✅ Preferibile (conversione implicita)
  console.log("Ha input");
}
if (!!input) {
  // Funziona ma !! è superfluo qui
  console.log("Ha input");
}

// Operatori logici convertono automaticamente
let valore = "test";
let risultato = valore && "eseguito"; // ✅ Preferibile
let risultatoAlt = !!valore && "eseguito"; // Superfluo

// PATTERN COMUNE: verifica esistenza
function componenteMontato() {
  return !!document.getElementById("app");
}

function haDatiLocalStorage() {
  return !!localStorage.getItem("userData");
}

function haProprietà(obj, prop) {
  return !!obj[prop];
}

let persona = { nome: "Mario", età: 0 };
console.log(haProprietà(persona, "nome")); // true
console.log(haProprietà(persona, "età")); // false (età è 0! ⚠️)
console.log(haProprietà(persona, "cognome")); // false
```

### Precedenza degli Operatori (Operator Precedence)

La precedenza stabilisce l'ordine in cui gli operatori vengono eseguiti in un'espressione. Ad esempio, la moltiplicazione ha la precedenza sull'addizione. Per controllare l'ordine di valutazione si usano le parentesi `()`, che hanno la priorità più alta.

```javascript
// SENZA PARENTESI (precedenza naturale)
let risultato1 = 2 + 3 * 4; // 14 (prima 3*4=12, poi 2+12=14)
console.log(risultato1);

let risultato2 = 10 - 2 * 3; // 4 (prima 2*3=6, poi 10-6=4)
console.log(risultato2);

// CON PARENTESI (controllo esplicito dell'ordine)
let risultato3 = (2 + 3) * 4; // 20 (prima 2+3=5, poi 5*4=20)
console.log(risultato3);

let risultato4 = (10 - 2) * 3; // 24 (prima 10-2=8, poi 8*3=24)
console.log(risultato4);

// TABELLA DI PRECEDENZA (dal più alto al più basso)
// ()           → Parentesi (massima priorità)
// ++ --        → Incremento/Decremento
// **           → Esponenziazione
// * / %        → Moltiplicazione, Divisione, Resto
// + -          → Addizione, Sottrazione
// < > <= >=    → Confronti relazionali
// == === != !== → Confronti di uguaglianza
// &&           → AND logico
// ||           → OR logico
// ? :          → Operatore ternario
// =            → Assegnamento (minima priorità)
```

```javascript
// ESEMPI DI PRECEDENZA
console.log(10 + 5 * 2); // 20 (moltiplicazione prima dell'addizione)
console.log((10 + 5) * 2); // 30 (parentesi hanno precedenza)

console.log(10 - 3 + 2); // 9 (stessa precedenza, da sinistra a destra)
console.log(10 - (3 + 2)); // 5 (parentesi cambiano l'ordine)

console.log(2 ** (3 ** 2)); // 512 (esponenziazione è destro-associativa: 3**2=9, poi 2**9=512)
console.log((2 ** 3) ** 2); // 64 (parentesi cambiano: 2**3=8, poi 8**2=64)

console.log(5 + 3 * 2 ** 2); // 17 (prima 2**2=4, poi 3*4=12, poi 5+12=17)
console.log((5 + 3) * 2 ** 2); // 32 (prima 2**2=4, poi 5+3=8, poi 8*4=32)

// CONFRONTI E LOGICA
let a = 5;
let b = 10;
console.log(a < 10 && b > 5); // true (confronti prima, poi AND)
console.log(a < 10 || (b < 5 && false)); // true (AND prima di OR)
// Interpretato come: a < 10 || (b < 5 && false)

// Con parentesi per chiarezza:
console.log((a < 10 || b < 5) && false); // false (cambia il risultato!)

// CASO COMPLESSO
let x = 3;
let y = 4;
let z = x + y * 2 > 10 ? "Grande" : "Piccolo";
// Ordine di valutazione:
// 1. y * 2 = 8
// 2. x + 8 = 11
// 3. 11 > 10 = true
// 4. true ? "Grande" : "Piccolo" = "Grande"
console.log(z); // "Grande"
```

```javascript
// ESEMPI PRATICI
// Calcolo prezzo con sconto e tasse
let prezzo = 100;
let sconto = 0.1; // 10%
let tasse = 0.22; // 22%

// ❌ Ambiguo senza parentesi
let totale1 = prezzo - prezzo * sconto + prezzo * tasse;
console.log(totale1); // 112 (cosa significa?)

// ✅ Chiaro con parentesi
let totale2 = prezzo - prezzo * sconto + prezzo * tasse;
// Meglio ancora:
let prezzoScontato = prezzo * (1 - sconto);
let prezzoFinale = prezzoScontato * (1 + tasse);
console.log(prezzoFinale); // 109.8

// Calcolo con priorità esplicite
let base = 10;
let altezza = 5;
let area = (base * altezza) / 2; // Area triangolo
console.log(area); // 25

// Formula con più operatori
let celsius = 25;
let fahrenheit = (celsius * 9) / 5 + 32;
console.log(fahrenheit); // 77

// Condizioni complesse
let età = 25;
let haPatente = true;
let macchinaDisponibile = true;

// ❌ Difficile da leggere
if ((età >= 18 && haPatente && macchinaDisponibile) || età >= 65) {
  // ...
}

// ✅ Più chiaro
let puòGuidare = età >= 18 && haPatente && macchinaDisponibile;
let èAnziano = età >= 65;
if (puòGuidare || èAnziano) {
  console.log("Può usare il servizio");
}
```

```javascript
// BEST PRACTICE: usare parentesi per chiarezza

// ❌ Non chiaro (anche se tecnicamente corretto)
let risultato = a + (b * c) / d - e;

// ✅ Chiaro (esplicita l'intenzione)
let risultato = a + (b * c) / d - e;

// ❌ Confuso
let condizione = (x > 5 && y < 10) || (z === 0 && w !== null);

// ✅ Leggibile
let condizione = (x > 5 && y < 10) || (z === 0 && w !== null);

// REGOLA D'ORO: Se non sei sicuro della precedenza, usa le parentesi!
// Il codice deve essere leggibile prima che "smart"
```

---

## 6. Gestire le Vecchie e Nuove Funzionalità di JavaScript

Molte delle funzionalità di JavaScript, specialmente quelle più recenti, non sono disponibili nei browser più datati. Invece di attendere che i vecchi browser vengano dismessi, è possibile utilizzare delle tecniche per rendere il codice moderno compatibile con ambienti JavaScript meno recenti. Le due principali sono il Polyfilling e il Transpiling.

### 6.1 Polyfilling

Il termine Polyfill (coniato da Remy Sharp) si riferisce a un pezzo di codice che replica il comportamento di una funzionalità nativa più recente, permettendone l'uso anche in ambienti JavaScript più vecchi che non la supportano.

Ad esempio, ES6 ha introdotto il metodo `Number.isNaN()` per fornire un controllo accurato e privo di bug per i valori NaN, superando la vecchia funzione `isNaN()`. È possibile creare un polyfill per `Number.isNaN()` in modo da poterlo usare nel proprio codice a prescindere dal browser dell'utente finale.

```javascript
// POLYFILL per Number.isNaN()
if (!Number.isNaN) {
  Number.isNaN = function isNaN(x) {
    return x !== x;
  };
}

// Spiegazione: NaN è l'unico valore in JavaScript che non è uguale a se stesso
console.log(NaN !== NaN); // true (proprietà unica di NaN)
console.log(5 !== 5); // false (tutti gli altri valori sono uguali a se stessi)

// Uso del polyfill
console.log(Number.isNaN(NaN)); // true
console.log(Number.isNaN("ciao")); // false
console.log(Number.isNaN(42)); // false
console.log(Number.isNaN(undefined)); // false

// Confronto con il vecchio isNaN() (problematico)
console.log(isNaN("ciao")); // true ⚠️ (converte "ciao" a NaN prima di controllare)
console.log(Number.isNaN("ciao")); // false ✅ (controlla se è VERAMENTE NaN)
```

L'istruzione `if` serve come "guardia": controlla se `Number.isNaN` esiste già (come nei browser ES6) e, in caso contrario, lo definisce. In questo modo, si evita di sovrascrivere l'implementazione nativa.

```javascript
// PATTERN COMPLETO DI POLYFILLING

// 1. Controlla se la funzionalità esiste
if (!Array.prototype.includes) {
  // 2. Se non esiste, implementala
  Array.prototype.includes = function (searchElement, fromIndex) {
    // Gestione dei parametri
    if (this == null) {
      throw new TypeError('"this" is null or not defined');
    }

    let array = Object(this);
    let len = array.length >>> 0;

    if (len === 0) {
      return false;
    }

    let n = fromIndex | 0;
    let k = Math.max(n >= 0 ? n : len - Math.abs(n), 0);

    // Ricerca dell'elemento
    while (k < len) {
      if (array[k] === searchElement) {
        return true;
      }
      k++;
    }

    return false;
  };
}

// Test del polyfill
let numeri = [1, 2, 3, 4, 5];
console.log(numeri.includes(3)); // true
console.log(numeri.includes(10)); // false

let frutti = ["mela", "banana", "arancia"];
console.log(frutti.includes("banana")); // true
console.log(frutti.includes("kiwi")); // false
```

```javascript
// ESEMPIO: Polyfill per Array.prototype.find() (ES6)
if (!Array.prototype.find) {
  Array.prototype.find = function (predicate) {
    if (this == null) {
      throw new TypeError("Array.prototype.find called on null or undefined");
    }
    if (typeof predicate !== "function") {
      throw new TypeError("predicate must be a function");
    }

    let list = Object(this);
    let length = list.length >>> 0;
    let thisArg = arguments[1];

    for (let i = 0; i < length; i++) {
      let value = list[i];
      if (predicate.call(thisArg, value, i, list)) {
        return value;
      }
    }
    return undefined;
  };
}

// Test del polyfill
let utenti = [
  { id: 1, nome: "Mario" },
  { id: 2, nome: "Luigi" },
  { id: 3, nome: "Peach" },
];

let utente = utenti.find((u) => u.id === 2);
console.log(utente); // { id: 2, nome: 'Luigi' }

let nonEsiste = utenti.find((u) => u.id === 10);
console.log(nonEsiste); // undefined
```

```javascript
// ESEMPIO: Polyfill per String.prototype.startsWith() (ES6)
if (!String.prototype.startsWith) {
  String.prototype.startsWith = function (search, position) {
    position = position || 0;
    return this.indexOf(search, position) === position;
  };
}

// Test del polyfill
let testo = "JavaScript è fantastico";
console.log(testo.startsWith("Java")); // true
console.log(testo.startsWith("Script")); // false
console.log(testo.startsWith("Script", 4)); // true (inizia dalla posizione 4)

let url = "https://example.com";
console.log(url.startsWith("https://")); // true
console.log(url.startsWith("http://")); // false
```

Non tutte le nuove funzionalità sono completamente "polyfillabili". A volte, un polyfill può replicare la maggior parte del comportamento, ma con piccole deviazioni rispetto alla specifica ufficiale. Per questo motivo, è fondamentale essere molto attenti nell'implementare un polyfill da soli.

La pratica migliore è affidarsi a raccolte di polyfill già testate e affidabili, come quelle fornite da librerie quali ES5-Shim e ES6-Shim.

```javascript
// LIBRERIE DI POLYFILL POPOLARI

// 1. core-js (la più completa)
// npm install core-js
// import 'core-js/stable';

// 2. polyfill.io (servizio CDN)
// <script src="https://polyfill.io/v3/polyfill.min.js"></script>

// 3. ES6-Shim
// npm install es6-shim
// import 'es6-shim';

// Esempio di utilizzo con polyfill automatico
// Il browser scarica solo i polyfill che gli servono
```

### 6.2 Transpiling

A differenza del polyfilling, che replica funzionalità mancanti, non è possibile creare un "polyfill" per una nuova sintassi del linguaggio. Un motore JavaScript datato non riconoscerebbe la nuova sintassi e genererebbe un errore di validazione.

La soluzione a questo problema è il Transpiling (un termine che unisce transforming e compiling). Si tratta di un processo in cui uno strumento, chiamato transpiler, converte il codice sorgente scritto con la sintassi più recente in una versione equivalente che utilizza una sintassi più vecchia e compatibile con un maggior numero di ambienti.

In pratica, lo sviluppatore scrive codice moderno e pulito, ma ciò che viene eseguito nel browser è il codice "tradotto". Questo processo viene solitamente integrato nella fase di build dell'applicazione, insieme ad altri strumenti come linter e minifier.

#### Perché Usare il Transpiling?

Ci sono diverse ragioni importanti per adottare questo approccio:

- **Leggibilità e Manutenibilità** → La nuova sintassi è progettata per rendere il codice più chiaro e facile da gestire. Le alternative più vecchie sono spesso più complesse e verbose.

- **Ottimizzazione delle Performance** → È possibile configurare il processo di build per servire il codice con la sintassi moderna ai browser più recenti (che possono avere ottimizzazioni specifiche) e il codice transpilato solo a quelli più vecchi.

- **Feedback alla Community** → Usare le nuove funzionalità in anticipo permette di testarle su larga scala nel mondo reale. Questo fornisce un feedback prezioso al comitato TC39 (che standardizza JavaScript), consentendo di correggere eventuali errori di progettazione prima che diventino permanenti.

#### Esempio di Transpiling

ES6 ha introdotto i valori di default per i parametri delle funzioni:

```javascript
// CODICE ES6 (moderno)
function saluta(nome = "Ospite") {
  console.log("Ciao, " + nome + "!");
}

saluta(); // "Ciao, Ospite!"
saluta("Mario"); // "Ciao, Mario!"
saluta(undefined); // "Ciao, Ospite!" (undefined attiva il default)
saluta(null); // "Ciao, null!" (null NON attiva il default)
```

Questa sintassi non è valida nei motori pre-ES6. Un transpiler la convertirebbe in un codice simile a questo:

```javascript
// CODICE ES5 (transpilato, compatibile con browser vecchi)
function saluta(nome) {
  if (nome === undefined) {
    nome = "Ospite";
  }
  console.log("Ciao, " + nome + "!");
}

// Oppure, versione più concisa
function saluta(nome) {
  nome = nome === undefined ? "Ospite" : nome;
  console.log("Ciao, " + nome + "!");
}

saluta(); // "Ciao, Ospite!"
saluta("Mario"); // "Ciao, Mario!"
saluta(undefined); // "Ciao, Ospite!"
saluta(null); // "Ciao, null!"
```

Questo esempio mostra non solo come la sintassi venga resa compatibile, ma chiarisce anche il comportamento della funzionalità: il valore di default viene applicato solo se al parametro viene passato `undefined` (o nessun valore).

```javascript
// ALTRO ESEMPIO: Arrow Functions

// ES6 (moderno)
const numeri = [1, 2, 3, 4, 5];
const doppi = numeri.map((n) => n * 2);
console.log(doppi); // [2, 4, 6, 8, 10]

// ES5 (transpilato)
var numeri = [1, 2, 3, 4, 5];
var doppi = numeri.map(function (n) {
  return n * 2;
});
console.log(doppi); // [2, 4, 6, 8, 10]
```

```javascript
// ESEMPIO: Template Literals

// ES6 (moderno)
const nome = "Mario";
const età = 30;
const messaggio = `Ciao, mi chiamo ${nome} e ho ${età} anni.`;
console.log(messaggio); // "Ciao, mi chiamo Mario e ho 30 anni."

// ES5 (transpilato)
var nome = "Mario";
var età = 30;
var messaggio = "Ciao, mi chiamo " + nome + " e ho " + età + " anni.";
console.log(messaggio); // "Ciao, mi chiamo Mario e ho 30 anni."
```

```javascript
// ESEMPIO: Destructuring

// ES6 (moderno)
const persona = { nome: "Luigi", età: 25, città: "Roma" };
const { nome, età } = persona;
console.log(nome); // "Luigi"
console.log(età); // 25

const colori = ["rosso", "verde", "blu"];
const [primo, secondo] = colori;
console.log(primo); // "rosso"
console.log(secondo); // "verde"

// ES5 (transpilato)
var persona = { nome: "Luigi", età: 25, città: "Roma" };
var nome = persona.nome;
var età = persona.età;
console.log(nome); // "Luigi"
console.log(età); // 25

var colori = ["rosso", "verde", "blu"];
var primo = colori[0];
var secondo = colori[1];
console.log(primo); // "rosso"
console.log(secondo); // "verde"
```

```javascript
// ESEMPIO: Classes

// ES6 (moderno)
class Animale {
  constructor(nome) {
    this.nome = nome;
  }

  parla() {
    console.log(this.nome + " fa un verso");
  }
}

class Cane extends Animale {
  parla() {
    console.log(this.nome + " abbaia");
  }
}

const cane = new Cane("Fido");
cane.parla(); // "Fido abbaia"

// ES5 (transpilato - versione semplificata)
function Animale(nome) {
  this.nome = nome;
}

Animale.prototype.parla = function () {
  console.log(this.nome + " fa un verso");
};

function Cane(nome) {
  Animale.call(this, nome);
}

Cane.prototype = Object.create(Animale.prototype);
Cane.prototype.constructor = Cane;

Cane.prototype.parla = function () {
  console.log(this.nome + " abbaia");
};

var cane = new Cane("Fido");
cane.parla(); // "Fido abbaia"
```

```javascript
// CONFIGURAZIONE TIPICA DI BABEL (transpiler)

// .babelrc o babel.config.json
{
  "presets": [
    [
      "@babel/preset-env",
      {
        "targets": {
          "browsers": ["> 0.5%", "last 2 versions", "not dead"]
        }
      }
    ]
  ]
}

// Babel transpila automaticamente:
// - Arrow functions → function expressions
// - const/let → var
// - Template literals → concatenazione stringhe
// - Destructuring → assegnamenti multipli
// - Classes → constructor functions + prototype
// - Spread operator → Array.prototype.concat/Object.assign
// - E molto altro...
```

In conclusione il transpiling è oggi considerato una parte standard del processo di sviluppo in JavaScript. Poiché il linguaggio evolve rapidamente, l'uso di un transpiler permette di adottare le nuove sintassi non appena diventano utili, senza dover attendere anni per la dismissione dei vecchi browser.

Tra i transpiler più noti ci sono **Babel** (precedentemente conosciuto come 6to5) e **Traceur**.

```javascript
// TRANSPILER POPOLARI

// 1. BABEL (il più usato)
// npm install --save-dev @babel/core @babel/cli @babel/preset-env
// npx babel src --out-dir dist

// 2. TYPESCRIPT (transpiler + type checker)
// npm install --save-dev typescript
// tsc src/index.ts

// 3. SWC (molto veloce, scritto in Rust)
// npm install --save-dev @swc/core @swc/cli
// npx swc src -d dist

// 4. ESBUILD (velocissimo)
// npm install --save-dev esbuild
// node esbuild.config.js
```

### 6.3 Non-JavaScript

Quando si scrive codice JavaScript, la maggior parte del tempo lo si fa per eseguirlo all'interno di ambienti specifici, come i browser. È importante capire che una parte significativa del codice che si scrive non è, in senso stretto, controllata direttamente dal linguaggio JavaScript stesso.

L'esempio più comune di questo concetto è l'API del DOM (Document Object Model). Quando si utilizza un'istruzione come:

```javascript
// DOM API (fornita dal BROWSER, non da JavaScript)
let elemento = document.getElementById("mioId");

// 'document' è un oggetto globale fornito dal browser
console.log(typeof document); // "object"
console.log(document); // Document { ... }

// Questi metodi NON fanno parte della specifica JavaScript
elemento.addEventListener("click", function () {
  console.log("Cliccato!");
});

elemento.style.color = "red";
elemento.innerHTML = "Nuovo testo";
elemento.classList.add("attivo");
```

La variabile `document` è una variabile globale disponibile quando il codice viene eseguito in un browser. Tuttavia, non è fornita dal motore JavaScript (JS engine), né è definita dalle specifiche del linguaggio. Si presenta come un normale oggetto JavaScript, ma in realtà è un tipo speciale di oggetto, spesso chiamato "oggetto ospite" (host object).

Allo stesso modo, il metodo `getElementById()` su document sembra una normale funzione JavaScript, ma in realtà è solo un'interfaccia esposta verso una funzionalità interna del browser, fornita dal DOM. Tradizionalmente, il DOM e i suoi comportamenti sono implementati in linguaggi come C/C++.

```javascript
// ALTRI ESEMPI DI API DEL BROWSER (non JavaScript puro)

// 1. WINDOW OBJECT
console.log(window.innerWidth); // Larghezza finestra
console.log(window.location.href); // URL corrente
window.scrollTo(0, 100); // Scroll della pagina

// 2. TIMERS
setTimeout(function () {
  console.log("Dopo 1 secondo");
}, 1000);

setInterval(function () {
  console.log("Ogni 2 secondi");
}, 2000);

// 3. FETCH API (richieste HTTP)
fetch("https://api.example.com/data")
  .then((response) => response.json())
  .then((data) => console.log(data));

// 4. LOCAL STORAGE
localStorage.setItem("chiave", "valore");
let valore = localStorage.getItem("chiave");

// 5. GEOLOCATION
navigator.geolocation.getCurrentPosition(function (position) {
  console.log("Latitudine:", position.coords.latitude);
  console.log("Longitudine:", position.coords.longitude);
});
```

Un altro esempio riguarda l'input/output (I/O). La funzione `alert()`, che mostra una finestra di dialogo nel browser, non è fornita dal motore JavaScript, ma dall'ambiente del browser. La chiamata a questa funzione invia il messaggio alle componenti interne del browser, che si occupano di creare e visualizzare la finestra di dialogo.

```javascript
// DIALOG API (fornite dal browser)

// Alert (blocca l'esecuzione)
alert("Questo è un messaggio di avviso");

// Confirm (restituisce true/false)
let risposta = confirm("Sei sicuro?");
if (risposta) {
  console.log("Utente ha confermato");
} else {
  console.log("Utente ha annullato");
}

// Prompt (chiede input all'utente)
let nome = prompt("Come ti chiami?", "Mario");
console.log("Ciao, " + nome);

// NOTA: Questi metodi sono SINCRONI e bloccano l'esecuzione
// Non sono considerati best practice nelle applicazioni moderne
```

Lo stesso vale per `console.log()`, un meccanismo fornito dal browser e collegato agli strumenti per sviluppatori.

```javascript
// CONSOLE API (fornita dall'ambiente di esecuzione)

// Vari metodi di logging
console.log("Messaggio normale"); // Log normale
console.info("Informazione"); // Info
console.warn("Attenzione!"); // Warning (giallo)
console.error("Errore!"); // Errore (rosso)

// Debugging
console.table([
  { nome: "Mario", età: 30 },
  { nome: "Luigi", età: 25 },
]);

console.group("Gruppo di log");
console.log("Messaggio 1");
console.log("Messaggio 2");
console.groupEnd();

// Timing
console.time("operazione");
// ... codice da misurare ...
console.timeEnd("operazione"); // Mostra il tempo trascorso

// Assert
console.assert(5 > 10, "5 non è maggiore di 10"); // Mostra errore se false

// Trace
function funzione1() {
  funzione2();
}
function funzione2() {
  console.trace("Stack trace qui");
}
funzione1(); // Mostra lo stack delle chiamate
```

```javascript
// CONFRONTO: JavaScript PURO vs API DEL BROWSER

// ✅ JAVASCRIPT PURO (specifica ECMAScript)
let array = [1, 2, 3];
let somma = array.reduce((acc, n) => acc + n, 0);
console.log(typeof Array); // "function" (costruttore nativo JS)
console.log(typeof Object); // "function" (costruttore nativo JS)
console.log(typeof String); // "function" (costruttore nativo JS)

// ❌ API DEL BROWSER (NON parte di JavaScript)
let elemento = document.querySelector(".classe");
fetch("https://api.example.com");
localStorage.setItem("key", "value");
console.log(typeof document); // "object" (host object)
console.log(typeof window); // "object" (host object)
console.log(typeof navigator); // "object" (host object)

// Node.js ha le SUE API (diverse dal browser)
// require(), __dirname, process, fs, http, ecc.
```

```javascript
// DIFFERENZE TRA AMBIENTI

// IN BROWSER:
if (typeof window !== "undefined") {
  console.log("Siamo in un browser");
  console.log("User agent:", navigator.userAgent);
  document.body.style.backgroundColor = "lightblue";
}

// IN NODE.JS:
if (typeof process !== "undefined") {
  console.log("Siamo in Node.js");
  console.log("Versione Node:", process.version);
  // const fs = require('fs');
  // fs.readFileSync('file.txt');
}

// AMBIENTE UNIVERSALE:
if (typeof globalThis !== "undefined") {
  console.log("globalThis è disponibile (ES2020+)");
  // globalThis funziona in browser (= window) e Node.js (= global)
}
```

```javascript
// WEB APIs COMUNI (non JavaScript puro)

// 1. XMLHttpRequest (vecchio modo di fare richieste HTTP)
let xhr = new XMLHttpRequest();
xhr.open("GET", "https://api.example.com/data");
xhr.onload = function () {
  console.log(xhr.responseText);
};
xhr.send();

// 2. WebSocket (comunicazione bidirezionale)
let socket = new WebSocket("ws://example.com/socket");
socket.onmessage = function (event) {
  console.log("Messaggio ricevuto:", event.data);
};

// 3. IndexedDB (database nel browser)
let request = indexedDB.open("MioDatabase", 1);
request.onsuccess = function (event) {
  let db = event.target.result;
  console.log("Database aperto");
};

// 4. Web Workers (thread paralleli)
let worker = new Worker("worker.js");
worker.postMessage("Inizia lavoro");
worker.onmessage = function (event) {
  console.log("Risultato worker:", event.data);
};

// 5. Canvas API (grafica 2D)
let canvas = document.getElementById("canvas");
let ctx = canvas.getContext("2d");
ctx.fillStyle = "red";
ctx.fillRect(10, 10, 100, 100);
```

```javascript
// HOST OBJECTS vs NATIVE OBJECTS

// NATIVE OBJECTS (parte di JavaScript)
let nativo1 = new Array(1, 2, 3); // Array nativo
let nativo2 = new Date(); // Date nativo
let nativo3 = new RegExp("pattern"); // RegExp nativo
console.log(Array.toString()); // "function Array() { [native code] }"

// HOST OBJECTS (forniti dall'ambiente)
let host1 = document.createElement("div"); // HTMLDivElement (browser)
let host2 = new XMLHttpRequest(); // XMLHttpRequest (browser)
let host3 = window.performance; // Performance API (browser)
// In Node.js: Buffer, process, require, ecc.

// DIFFERENZA CHIAVE:
// - Native objects: definiti dalla specifica ECMAScript
// - Host objects: definiti dall'ambiente (browser, Node.js, Deno, ecc.)
```

Sebbene questi meccanismi non facciano parte del linguaggio JavaScript puro, è fondamentale esserne consapevoli, poiché sono presenti in quasi tutti i programmi JavaScript che si scrivono per il web.

```javascript
// BEST PRACTICE: Verifica della disponibilità delle API

// Prima di usare un'API del browser, controlla se esiste
if (typeof localStorage !== "undefined") {
  localStorage.setItem("chiave", "valore");
} else {
  console.log("localStorage non disponibile");
}

if (typeof fetch === "function") {
  fetch("https://api.example.com");
} else {
  console.log("fetch() non disponibile, usa XMLHttpRequest o un polyfill");
}

if ("geolocation" in navigator) {
  navigator.geolocation.getCurrentPosition(callback);
} else {
  console.log("Geolocation API non supportata");
}

// Feature detection (meglio di user-agent sniffing)
if ("serviceWorker" in navigator) {
  navigator.serviceWorker.register("/sw.js");
}
```

---
