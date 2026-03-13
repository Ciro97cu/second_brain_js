# [[../../../appunti-completi#il-sistema-di-tipi-in-javascript|Sistema dei Tipi JavaScript: Tipi e Sottotipi]]

JavaScript ha un sistema di tipi composto da **6 tipi primitivi** più un tipo complesso **object**. Contrariamente al mito popolare, **non tutto è un oggetto** in JavaScript. Inoltre, alcuni tipi come `function` e array sono **sottotipi specializzati** di object, non tipi indipendenti.

## Concetti Chiave

- **6 tipi primitivi**: string, number, boolean, undefined, null, symbol (immutabili, passati per valore)
- **1 tipo complesso**: object (mutabile, passato per riferimento)
- **typeof restituisce 7 valori** (più "function"): Ma function non è un tipo separato, è un **sottotipo** di object
- **Mito "tutto è oggetto"**: Falso! I primitivi non sono oggetti (possono solo essere "boxed" temporaneamente)
- **Sottotipi di object**: function, array, Date, RegExp, Error, etc.

## I 6 Tipi Primitivi + Object

```javascript
/* I 6 PRIMITIVI */

// 1. string - Sequenze di caratteri
let nome = "Mario";
let saluto = `Ciao ${nome}`; // template literal

// 2. number - Numeri a virgola mobile (64 bit IEEE 754)
let intero = 42;
let decimale = 3.14;
let infinito = Infinity;
let nonNumero = NaN; // Not a Number (tipo number!)

// 3. boolean - Valori logici
let vero = true;
let falso = false;

// 4. undefined - Valore non assegnato
let nonInizializzato;
console.log(nonInizializzato); // undefined

// 5. null - Assenza intenzionale di valore
let risultatoVuoto = null;

// 6. symbol - Identificatori unici (ES6+)
let id = Symbol("identificatore");
let id2 = Symbol("identificatore");
console.log(id === id2); // false (sempre diversi)

/* IL TIPO OBJECT */

// object - Collezioni di proprietà (chiave-valore)
let persona = {
  nome: "Mario",
  eta: 30,
};

let numeri = [1, 2, 3]; // array è un object
let data = new Date(); // Date è un object
let regex = /ab+c/; // RegExp è un object
let errore = new Error("Ops"); // Error è un object

// function - Callable object (sottotipo di object)
function saluta() {
  console.log("Ciao!");
}
```

## typeof e il Bug Storico di null

L'operatore `typeof` sembra suggerire 8 tipi, ma è ingannevole:

```javascript
console.log(typeof "testo"); // "string" ✅
console.log(typeof 42); // "number" ✅
console.log(typeof true); // "boolean" ✅
console.log(typeof undefined); // "undefined" ✅
console.log(typeof Symbol("x")); // "symbol" ✅

console.log(typeof null); // "object" ⚠️ BUG STORICO!

console.log(typeof {}); // "object" ✅
console.log(typeof []); // "object" (array è object)
console.log(typeof function () {}); // "function" ⚠️ (ma function È un object!)
```

**Il bug di `typeof null`**: Per ragioni storiche (bug nel motore originale JavaScript 1995), `typeof null` restituisce `"object"` invece di `"null"`. Questo non è mai stato corretto per retrocompatibilità.

```javascript
// ❌ NON usare typeof per verificare null
if (typeof valore === "object") {
  // Questo include sia oggetti CHE null!
}

// ✅ Verificare null esplicitamente
if (valore === null) {
  // Modo corretto
}

// ✅ Oppure escludere null
if (typeof valore === "object" && valore !== null) {
  // Ora sono sicuro che è un object vero
}
```

> **Approfondimento**: [typeof](typeof.md) spiega tutti i casi speciali dell'operatore.

## Il Mito: "Tutto è un Oggetto"

**Falso!** Questa affermazione comune è **inesatta**. I valori primitivi **non sono oggetti**:

```javascript
// Primitivi NON sono oggetti
let str = "ciao";
console.log(typeof str); // "string" (non "object")

let num = 42;
console.log(typeof num); // "number" (non "object")

let bool = true;
console.log(typeof bool); // "boolean" (non "object")

// Prova: i primitivi non hanno proprietà proprie
let primitivo = "test";
primitivo.miaProprietà = "valore";
console.log(primitivo.miaProprietà); // undefined (aggiunta ignorata!)

// Oggetti HANNO proprietà
let oggetto = {};
oggetto.miaProprietà = "valore";
console.log(oggetto.miaProprietà); // "valore" ✅
```

### Da Dove Nasce la Confusione?

La confusione nasce dal fatto che i primitivi **sembrano** avere metodi:

```javascript
let testo = "hello";
console.log(testo.toUpperCase()); // "HELLO" - Come fa se non è un oggetto?

let numero = 42.567;
console.log(numero.toFixed(2)); // "42.57" - Dove sono questi metodi?
```

**Risposta: Boxing automatico**. Quando accedi a un metodo su un primitivo, JavaScript **temporaneamente** lo "avvolge" (wrap) in un oggetto corrispondente, chiama il metodo, e poi scarta l'oggetto temporaneo:

```javascript
// Quello che scrivi:
let str = "hello";
str.toUpperCase();

// Quello che JavaScript fa dietro le quinte:
let str = "hello";
new String(str).toUpperCase(); // Crea wrapper temporaneo, chiama metodo, scarta wrapper

// Per questo le assegnazioni non funzionano:
str.miaProprietà = "valore"; // Assegna alla versione boxed, poi scartata
console.log(str.miaProprietà); // undefined (l'oggetto temporaneo non esiste più)
```

> **Approfondimento**: Il meccanismo di boxing è spiegato in dettaglio in [boxing](boxing.md).

### Conclusione: Primitivi vs Oggetti

- **Primitivi**: Valori semplici, immutabili, passati per valore
- **Oggetti**: Strutture complesse, mutabili, passati per riferimento
- **Boxing**: I primitivi possono essere temporaneamente avvolti per accedere a metodi, ma **non sono oggetti**

```javascript
/* Differenza fondamentale */

// Primitivi: immutabili
let x = "ciao";
x.toUpperCase(); // Crea nuovo valore, non modifica x
console.log(x); // "ciao" (invariato)

// Oggetti: mutabili
let arr = [1, 2, 3];
arr.push(4); // Modifica l'array originale
console.log(arr); // [1, 2, 3, 4]
```

## Sottotipi di Object: function e Array

Anche se `typeof function() {}` restituisce `"function"`, le **funzioni sono oggetti**. Più precisamente, sono un **sottotipo** di object con capacità aggiuntiva: essere **callable** (invocabili).

### Function: Callable Objects (First-Class Citizens)

```javascript
function saluta(nome) {
  return `Ciao, ${nome}!`;
}

// Le funzioni SONO oggetti
console.log(typeof saluta); // "function" (caso speciale di typeof)
console.log(saluta instanceof Object); // true ✅

// Possono avere proprietà come qualsiasi oggetto
saluta.linguaggio = "Italiano";
saluta.versione = 1.0;

console.log(saluta.linguaggio); // "Italiano"

// Hanno proprietà built-in
console.log(saluta.name); // "saluta"
console.log(saluta.length); // 1 (numero parametri formali)

// Possono essere assegnate a variabili
let fn = saluta;
console.log(fn("Mario")); // "Ciao, Mario!"

// Possono essere passate come argomenti
function eseguiDueVolte(funzione, valore) {
  funzione(valore);
  funzione(valore);
}

eseguiDueVolte(saluta, "Mario"); // Chiama saluta due volte

// Possono essere restituite da altre funzioni
function creaCounter() {
  let count = 0;
  return function () {
    return ++count;
  };
}

let counter = creaCounter();
console.log(counter()); // 1
console.log(counter()); // 2
```

**First-Class Citizens**: In JavaScript, le funzioni sono "cittadini di prima classe" perché possono essere:

1. Assegnate a variabili
2. Passate come argomenti
3. Restituite da altre funzioni
4. Memorizzate in strutture dati
5. Create a runtime (anonime, arrow functions)

Questa caratteristica è fondamentale per la programmazione funzionale in JavaScript.

### Array: Structured Objects con Comportamento Extra

Gli array sono oggetti specializzati per memorizzare collezioni **ordinate** e **indicizzate numericamente**:

```javascript
let numeri = [10, 20, 30];

// Array è un object
console.log(typeof numeri); // "object"
console.log(numeri instanceof Object); // true
console.log(Array.isArray(numeri)); // true ✅ (metodo corretto per verificare)

// Ma ha comportamento speciale

// 1. Indici numerici automatici
console.log(numeri[0]); // 10
console.log(numeri[1]); // 20

// 2. Proprietà length automatica
console.log(numeri.length); // 3

numeri.push(40); // Aggiunge elemento
console.log(numeri.length); // 4 (aggiornato automaticamente)

// 3. Metodi specializzati per collezioni
numeri.forEach((n) => console.log(n));
let raddoppiati = numeri.map((n) => n * 2); // [20, 40, 60, 80]

// Ma è comunque possibile aggiungere proprietà come oggetto
numeri.descrizione = "Lista di numeri";
console.log(numeri.descrizione); // "Lista di numeri"

// ATTENZIONE: proprietà non-numeriche non influenzano length
console.log(numeri.length); // 4 (non 5!)
```

### Array vs Object: Quando Usare Quale?

```javascript
/* ✅ USA ARRAY per collezioni ordinate con indici numerici */
let studenti = ["Mario", "Luigi", "Peach"];
studenti.forEach((studente, indice) => {
  console.log(`${indice}: ${studente}`);
});

// Operazioni su sequenze
let primi3 = studenti.slice(0, 3);
let ordinati = studenti.sort();

/* ✅ USA OBJECT per collezioni chiave-valore senza ordine garantito */
let voti = {
  Mario: 28,
  Luigi: 30,
  Peach: 27,
};

console.log(voti.Mario); // 28
console.log(voti["Luigi"]); // 30

/* ❌ Array con chiavi non numeriche (tecnicamente possibile, ma confuso) */
let arrayConfuso = ["Mario", "Luigi"];
arrayConfuso["insegnante"] = "Yoshi"; // Aggiunge proprietà non-numerica
console.log(arrayConfuso.length); // 2 (insegnante non conta!)
console.log(arrayConfuso.insegnante); // "Yoshi" (esiste, ma fuorviante)

// Meglio usare object se hai chiavi miste
let classeChiara = {
  studente1: "Mario",
  studente2: "Luigi",
  insegnante: "Yoshi",
};
```

## Altri Sottotipi di Object

Oltre a function e array, JavaScript fornisce altri sottotipi built-in:

```javascript
// Date - Gestione date e orari
let adesso = new Date();
console.log(typeof adesso); // "object"
console.log(adesso instanceof Date); // true

// RegExp - Espressioni regolari
let pattern = /[a-z]+/i;
console.log(typeof pattern); // "object"
console.log(pattern instanceof RegExp); // true

// Error - Gestione errori
let errore = new Error("Qualcosa è andato storto");
console.log(typeof errore); // "object"
console.log(errore instanceof Error); // true

// Map, Set (ES6+) - Collezioni specializzate
let mappa = new Map();
mappa.set("chiave", "valore");
console.log(typeof mappa); // "object"
console.log(mappa instanceof Map); // true

let insieme = new Set([1, 2, 3, 3]);
console.log(typeof insieme); // "object"
console.log(insieme.size); // 3 (duplicati rimossi)
```

Tutti questi sono **sottotipi specializzati** di object, ciascuno con comportamento e metodi specifici.

## Implicazioni Pratiche

### 1. Verifica dei Tipi

```javascript
// ❌ typeof non è sufficiente per array
let arr = [1, 2, 3];
console.log(typeof arr); // "object" (non specifico)

// ✅ Usa Array.isArray()
console.log(Array.isArray(arr)); // true

// ✅ Usa instanceof per sottotipi
console.log(arr instanceof Array); // true
console.log(arr instanceof Object); // true (array è anche object)

// ❌ typeof null restituisce "object"
let nullo = null;
if (typeof nullo === "object") {
  /* ATTENZIONE: anche null entra qui! */
}

// ✅ Verifica null esplicitamente
if (nullo === null) {
  /* Modo corretto */
}
```

### 2. Scelta della Struttura Dati

```javascript
// ✅ Array per sequenze ordinate con operazioni su indici
let punteggi = [95, 87, 92];
let media = punteggi.reduce((a, b) => a + b) / punteggi.length;

// ✅ Object per mappature chiave-valore
let configurazione = {
  host: "localhost",
  port: 3000,
  ssl: false,
};

// ✅ Function per logica riutilizzabile e callable
let calcola = (a, b) => a + b;
let risultato = calcola(5, 3); // Invocabile

// ✅ Map per chiavi di qualsiasi tipo (non solo stringhe)
let mappa = new Map();
mappa.set(oggetto, "valore"); // Chiave può essere oggetto!

// ✅ Set per valori unici
let uniqueValues = new Set([1, 2, 2, 3]); // Set { 1, 2, 3 }
```

### 3. Comprensione del Passaggio Parametri

```javascript
// Primitivi: passati per valore (copia)
function modificaPrimitivo(x) {
  x = 100;
}

let num = 42;
modificaPrimitivo(num);
console.log(num); // 42 (invariato)

// Oggetti: passati per riferimento (stesso oggetto)
function modificaOggetto(obj) {
  obj.valore = 100;
}

let oggetto = { valore: 42 };
modificaOggetto(oggetto);
console.log(oggetto.valore); // 100 (modificato!)

// Array e function seguono stesse regole (sono oggetti)
function modificaArray(arr) {
  arr.push(4);
}

let lista = [1, 2, 3];
modificaArray(lista);
console.log(lista); // [1, 2, 3, 4] (modificato)
```

## Punti Chiave

1. **7 tipi in JavaScript**: 6 primitivi (string, number, boolean, undefined, null, symbol) + object

2. **typeof bugg per null**: Restituisce `"object"` ma null non è un oggetto. Usa `=== null` per verificare

3. **"Tutto è oggetto" è falso**: I primitivi non sono oggetti, ma possono essere boxed temporaneamente

4. **function è un sottotipo di object**: Callable object con proprietà speciali (name, length, prototype)

5. **Array è un sottotipo di object**: Object strutturato con indici numerici e proprietà length automatica

6. **First-class functions**: Le funzioni possono essere assegnate, passate e restituite come valori

7. **Usa Array.isArray()**: `typeof` restituisce `"object"` sia per array che oggetti. Usa metodo specifico

8. **Boxing automatico**: Accedere a metodi su primitivi crea temporaneamente oggetti wrapper

9. **Altri sottotipi**: Date, RegExp, Error, Map, Set sono tutti sottotipi di object

10. **Scelta struttura dati**: Array per sequenze ordinate, Object per chiave-valore, function per logica callable

## Collegamenti

- [[valori-tipi]] - Panoramica generale dei tipi JavaScript
- [[typeof]] - Operatore typeof e casi speciali (bug di null)
- [[boxing]] - Meccanismo di boxing automatico dei primitivi
- [[../oggetti/oggetti]] - Manipolazione e proprietà degli oggetti
- [[../oggetti/object-literal-vs-constructed]] - Creazione di oggetti
- [[../array/array]] - Array come sottotipo specializzato
- [[../funzioni/funzioni]] - Funzioni come callable objects

#tipi #type-system #primitivi #object #sottotipi #function #array #first-class-citizens #boxing #typeof
