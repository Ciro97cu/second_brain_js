# Boxing e Metodi dei Primitivi

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
- [[coercizione]] - Coercizione esplicita e implicita
- [[../oggetti/oggetti]] - Differenza primitivi/oggetti
- [[typeof]] - Verificare tipo dei valori
