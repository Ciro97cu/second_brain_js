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

### 2.2 Statement (Istruzione)

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

### 2.3 Expression (Espressione)

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

### 2.4 Blocchi di Codice (Code Blocks)

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

### 3.4 Oggetti (Objects)

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
let copiaProf onda = JSON.parse(JSON.stringify(utente));
// Oppure librerie come lodash (_.cloneDeep)
```

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
