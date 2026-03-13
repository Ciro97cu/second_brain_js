# [[../../appunti-completi#il-mito-tutto-è-un-oggetto|Il Mito "Tutto è un Oggetto"]]

In JavaScript, è diffusa l'errata convinzione che "tutto sia un oggetto". Questa affermazione è inesatta. I valori appartenenti ai tipi primitivi (come stringhe, numeri e booleani) non sono oggetti.

## Primitivi vs Oggetti

Si può dimostrare facilmente che i primitivi non sono oggetti provando ad assegnarvi nuove proprietà:

```javascript
// I primitivi non sono oggetti
let str = "ciao";
let num = 42;
let bool = true;

console.log(typeof str); // "string" (non "object")

// Prova: i primitivi non hanno proprietà proprie
str.miaProprieta = "valore";
console.log(str.miaProprieta); // undefined (l'aggiunta viene ignorata)
```

Al contrario, gli oggetti consentono l'aggiunta dinamica di proprietà:

```javascript
// Gli oggetti consentono l'aggiunta di proprietà
let oggetto = {};
oggetto.miaProprieta = "valore";
console.log(oggetto.miaProprieta); // "valore"
```

## L'origine della Confusione: Il Boxing

La confusione deriva dal fatto che i primitivi sembrano possedere metodi:

```javascript
let testo = "hello";
console.log(testo.toUpperCase()); // "HELLO"
```

Questo comportamento è spiegato dal meccanismo di "boxing" automatico (approfondito in [[boxing]]). Quando si accede a un metodo su un primitivo, il motore JavaScript lo avvolge temporaneamente in un oggetto corrispondente (es. `String`), chiama il metodo e poi scarta l'oggetto temporaneo. 

### Implicazioni Pratiche

- **Primitivi**: Valori semplici e immutabili. Operazioni come `.toUpperCase()` restituiscono un nuovo valore e non modificano l'originale.
- **Oggetti**: Strutture complesse e mutabili. Metodi come `.push()` su un array alterano la struttura di partenza.

```javascript
// Primitivi: immutabili
let x = "ciao";
x.toUpperCase(); 
console.log(x); // "ciao" (invariato)

// Oggetti: mutabili
let arr = [1, 2, 3];
arr.push(4); 
console.log(arr); // [1, 2, 3, 4]
```