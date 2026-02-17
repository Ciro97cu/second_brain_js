# Valori Truthy e Falsy

**Appunti Completi**: [[../../appunti-completi#34-valori-truthy-e-falsy]]

In JavaScript, quando un valore non booleano viene usato in un **contesto che si aspetta un booleano** (come la condizione di un `if` o l'operando di un operatore logico), il linguaggio lo converte implicitamente in `true` o `false`.

Questo processo è chiamato **coercizione booleana**, e i valori vengono classificati come **truthy** o **falsy** in base al risultato.

## Valori Falsy

I valori **falsy** sono quelli che, quando forzati a diventare booleani, si convertono in `false`.

La lista dei valori falsy è **breve e ben definita**:

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

```javascript
/*
 * Test dei valori falsy
 */

if (false) {
  console.log("Non verrà mai eseguito");
}

if (0) {
  console.log("Non verrà mai eseguito");
}

if ("") {
  console.log("Non verrà mai eseguito");
}

if (null) {
  console.log("Non verrà mai eseguito");
}

if (undefined) {
  console.log("Non verrà mai eseguito");
}

if (NaN) {
  console.log("Non verrà mai eseguito");
}
```

## Valori Truthy

Un valore **truthy** è qualsiasi valore che, quando convertito in booleano, diventa `true`. Questo include praticamente **tutto il resto**.

**Esempi comuni**:

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
-Infinity       // truthy

// Array (anche vuoti!)
[]              // truthy ⚠️
[0]             // truthy
[false]         // truthy

// Oggetti (anche vuoti!)
{}              // truthy ⚠️
{a: 0}          // truthy

// Funzioni
function() {}   // truthy

// Date
new Date()      // truthy

// Simboli
Symbol()        // truthy
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

let oggettoVuoto = {};

if (oggettoVuoto) {
  console.log("Anche questo VIENE eseguito!"); // ✅
}

// Per controllare se un array è vuoto:
if (arrayVuoto.length === 0) {
  console.log("Array vuoto"); // ✅ Modo corretto
}

// Per controllare se un oggetto è vuoto:
if (Object.keys(oggettoVuoto).length === 0) {
  console.log("Oggetto vuoto"); // ✅ Modo corretto
}
```

## Utilizzo Pratico

La conoscenza dei valori truthy e falsy permette di scrivere codice più **conciso e leggibile**, specialmente nelle istruzioni condizionali.

### Controllo Esistenza Valore

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

### Default Values

```javascript
/*
 * Assegnare valori di default
 */

let userInput = "";
let messaggio = userInput || "Messaggio di default";

console.log(messaggio); // "Messaggio di default"

// Se userInput è falsy, viene usato il secondo operando
let userName = null;
let displayName = userName || "Guest";

console.log(displayName); // "Guest"
```

### Guard Clauses

```javascript
/*
 * Guard clauses per validazione
 */

function processaOrdine(ordine) {
  // ❌ Controllo esplicito verboso
  if (ordine === null || ordine === undefined) {
    return;
  }

  // ✅ Controllo conciso con truthy/falsy
  if (!ordine) {
    return;
  }

  // processa ordine...
}
```

### Conversione Esplicita a Boolean

Per convertire esplicitamente un valore in boolean:

```javascript
/*
 * Conversione esplicita
 */

// Usando Boolean()
let valore1 = Boolean("ciao"); // true
let valore2 = Boolean(""); // false
let valore3 = Boolean(0); // false
let valore4 = Boolean(42); // true

// Usando doppia negazione !!
let valore5 = !!"ciao"; // true
let valore6 = !!""; // false
let valore7 = !!0; // false
let valore8 = !!42; // true

// Come funziona !!
// !"ciao" → !true → false
// !!"ciao" → !false → true
```

## Casi Particolari e Attenzioni

### Stringhe che Sembrano False

```javascript
/*
 * Stringhe sono truthy anche se "sembrano" false
 */

if ("0") {
  console.log("Eseguito!"); // ✅ "0" è una stringa truthy
}

if ("false") {
  console.log("Eseguito!"); // ✅ "false" è una stringa truthy
}
```

### Confronto == vs Truthy/Falsy

```javascript
/*
 * Truthy/Falsy ≠ Uguaglianza ==
 */

// [] è truthy
if ([]) {
  console.log("Array vuoto è truthy"); // ✅
}

// Ma [] == true è false!
console.log([] == true); // false
console.log([] == false); // true (per coercizione complessa)

// Usare sempre === per confronti espliciti
console.log(Boolean([]) === true); // true (conversione esplicita)
```

## Best Practices

**Uso Consapevole**

```javascript
// ✅ Buon uso per controlli di esistenza
function saluta(nome) {
  if (!nome) {
    nome = "Guest";
  }
  console.log("Ciao, " + nome);
}

// ⚠️ Attenzione con numeri - 0 è falsy!
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

if (flag === true) {
  // chiaro che ci aspettiamo boolean
}
```

## Collegamenti

- [[coercizione]] - Coercizione di tipo in generale
- [[valori-tipi]] - Tipi primitivi e values
- [[../sintassi/condizionali]] - Uso nelle condizioni if/else
- [[../operatori/operatori-logici]] - Operatori logici e truthy/falsy
