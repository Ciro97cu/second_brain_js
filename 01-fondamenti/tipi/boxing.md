# [[../../appunti-completi#35-boxing-e-metodi-dei-primitivi|Boxing e Metodi dei Primitivi]]

In JavaScript, i **tipi primitivi** (string, number, boolean) espongono metodi e proprietà utili per manipolarli, nonostante non siano oggetti.

## Metodi dei Tipi Primitivi

```javascript
let testo = "javascript";
console.log(testo.length); // 10 (proprietà)
console.log(testo.toUpperCase()); // "JAVASCRIPT" (metodo)

let numero = 3.14159;
console.log(numero.toFixed(2)); // "3.14" (metodo)
```

Sembra strano: i primitivi non sono oggetti, come hanno metodi?

## Il Meccanismo del Boxing

**Boxing** è il processo automatico con cui JavaScript "avvolge" temporaneamente un valore primitivo in un oggetto wrapper.

Quando si tenta di accedere a proprietà/metodo su primitivo:

1. JavaScript **crea oggetto wrapper temporaneo** (String, Number, Boolean)
2. L'oggetto wrapper **contiene i metodi**
3. Il metodo viene **eseguito**
4. L'oggetto wrapper viene **scartato**

```javascript
let a = "ciao";
// a.toUpperCase() → cosa succede:
// 1. new String("ciao") creato temporaneamente
// 2. String.prototype.toUpperCase() chiamato
// 3. Risultato "CIAO" restituito
// 4. Oggetto String temporaneo eliminato

console.log(a.toUpperCase()); // "CIAO"
console.log(typeof a); // "string" (ancora primitivo!)
```

Processo **trasparente** per lo sviluppatore.

## Wrapper Objects vs Primitivi

**Regola fondamentale**: Preferire sempre **valori primitivi**, lasciare boxing a JavaScript.

```javascript
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

// Problemi con wrapper
console.log(str1 === "testo"); // true
console.log(str2 === "testo"); // false (object vs string)
```

## Built-in Objects: Funzioni Costruttore

JavaScript fornisce **oggetti built-in** con nomi che sembrano corrispondere ai tipi primitivi: `String`, `Number`, `Boolean`, `Object`, `Function`, `Array`, `Date`, `RegExp`, `Error`.

I nomi maiuscoli possono far pensare a **tipi** o **classi** (come `String` in Java), ma in realtà sono **funzioni** che possono essere usate come **costruttori** con l'operatore `new`.

```javascript
/* Primitivo vs Wrapper Object */
var strPrimitive = "I am a string";
typeof strPrimitive; // "string"
strPrimitive instanceof String; // false

var strObject = new String("I am a string");
typeof strObject; // "object"
strObject instanceof String; // true

/*
 * Ispezionando il sottotipo interno:
 */
Object.prototype.toString.call(strObject); // "[object String]"
/*
 * Conferma che strObject è un oggetto
 * creato dal costruttore String
 */
```

### Primitivi Sono Immutabili

Il valore primitivo `"I am a string"` non è un oggetto: è un **valore letterale primitivo e immutabile**.

Per eseguire operazioni come controllare lunghezza o accedere a caratteri, in teoria serve un oggetto `String`. Ma JavaScript risolve questo con **boxing automatico**.

### La Coercizione Automatica Risolve Tutto

Quando si accede a proprietà/metodi su primitivi, il motore applica automaticamente **boxing**:

```javascript
var strPrimitive = "I am a string";

/*
 * Anche se è primitivo, si può accedere a metodi
 */
console.log(strPrimitive.length); // 13
console.log(strPrimitive.charAt(3)); // "m"

/*
 * Il motore esegue automaticamente:
 * 1. Crea temporaneamente new String(strPrimitive)
 * 2. Accede alla proprietà/metodo
 * 3. Scarta l'oggetto wrapper
 */
```

Stesso meccanismo per `Number` e `Boolean`:

```javascript
var num = 42.359;
num.toFixed(2); // "42.36"

var bool = true;
bool.toString(); // "true"
```

### Preferire Sempre la Forma Letterale

La comunità JavaScript raccomanda **fortemente** di usare sempre **forma letterale primitiva** piuttosto che wrapper espliciti:

```javascript
/* ✅ PREFERITO: Forma letterale primitiva */
var str = "hello";
var num = 42;
var bool = true;

/* ❌ EVITARE: Wrapper espliciti (inutili) */
var str = new String("hello");
var num = new Number(42);
var bool = new Boolean(true);
```

I wrapper espliciti sono **inutili** (boxing automatico funziona) e causano **comportamenti confusi**:

```javascript
var primitivo = "hello";
var wrapper = new String("hello");

primitivo == wrapper; // true (coercizione)
primitivo === wrapper; // false! (tipi diversi)

/* Wrapper booleano sempre truthy */
var falseWrapper = new Boolean(false);

if (falseWrapper) {
  console.log("Eseguito!"); // ⚠️ Anche se contiene false!
}
/*
 * L'OGGETTO è truthy, non il valore contenuto
 */
```

### Casi Speciali: null, undefined, Date, Error

**null e undefined** non hanno wrapper: esistono solo come primitivi.

```javascript
var n = null;
var u = undefined;

// ❌ Accesso a proprietà genera TypeError
// n.toString();        // TypeError
// u.length;            // TypeError
```

**Date** richiede **sempre** il costruttore (no forma letterale):

```javascript
var now = new Date(); // ✅ Unico modo
var birthday = new Date("1990-05-15");
```

**Array, RegExp, Function**: preferire sempre forma letterale quando disponibile.

```javascript
/* ✅ PREFERITO: Forma letterale */
var arr = [1, 2, 3];
var regex = /ab+c/;
var func = function () {};

/* ❌ EVITARE: Forma costruita (solo casi speciali) */
var arr = new Array(1, 2, 3);
var regex = new RegExp("ab+c"); // Utile per pattern dinamici
var func = new Function("a", "b", "return a + b"); // Sconsigliato
```

**Error** viene solitamente creato automaticamente quando vengono sollevate eccezioni:

```javascript
/* Creazione automatica */
try {
  nonExistentFunction();
} catch (e) {
  console.log(e.message); // Error object automatico
}

/* Creazione esplicita (rara) */
throw new Error("Qualcosa è andato storto");
```

## Conversione Esplicita a Number

**Operatore Unario +** - Modo moderno e conciso:

```javascript
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
// parseInt(string, radix)
console.log(parseInt("42")); // 42
console.log(parseInt("42.99")); // 42 (solo intera)
console.log(parseInt("42px")); // 42 (ignora resto)
console.log(parseInt("3.14")); // 3

// parseFloat(string)
console.log(parseFloat("3.14")); // 3.14
console.log(parseFloat("99.99€")); // 99.99
```

**Number()** - Conversione completa:

```javascript
Number("42"); // 42
Number("3.14"); // 3.14
Number("42px"); // NaN (stringa non valida)
Number(true); // 1
Number(false); // 0
```

## Conversione Esplicita a String

**String()** - Sicura con tutti i valori:

```javascript
String(42); // "42"
String(true); // "true"
String(null); // "null"
String(undefined); // "undefined"
String([1, 2]); // "1,2"
```

**.toString()** - Metodo su valori (non su null/undefined):

```javascript
let num = 42;
num.toString(); // "42"

true.toString(); // "true"

// ❌ Errori
// null.toString();      // TypeError
// undefined.toString(); // TypeError
```

**Raccomandazione**: Usare **String()** per robustezza, evita errori con null/undefined.

## Collegamenti

- [[valori-tipi]] - Tipi primitivi vs Object
- [[tipi-e-sottotipi]] - Sistema dei tipi e sottotipi di object
- [[coercizione]] - Coercizione esplicita e implicita
- [[typeof]] - Verificare tipo dei valori
- [[../oggetti/oggetti]] - Differenza primitivi/oggetti e riferimenti
- [[../oggetti/object-literal-vs-constructed]] - Forma letterale vs costruita per oggetti

#boxing #wrappers #primitivi #built-in-objects #coercizione-automatica #string #number #boolean
