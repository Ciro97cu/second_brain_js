# Valori e Tipi (Values & Types)

**Appunti Completi**: [[../../appunti-completi#31-valori-e-tipi-values--types]]

I dati in JavaScript sono rappresentati attraverso tipi (types). JavaScript fornisce tipi primitivi built-in per gestire diverse categorie di informazioni.

## Tipi Primitivi Built-in

1. **string** → Testo
2. **number** → Numeri (interi e decimali)
3. **boolean** → Valori logici (`true`/`false`)
4. **null** → Assenza intenzionale di valore
5. **undefined** → Valore non assegnato
6. **symbol** → Identificatori unici (ES6)
7. **object** → Strutture dati complesse (oggetti, array, Date, ecc.)

## Caratteristiche dei Tipi

### Primitivi vs Object

I primi 6 tipi sono **primitivi** (immutabili, passati per valore).
Gli **object** sono complessi (mutabili, passati per riferimento) e includono: oggetti letterali, array, Date, funzioni, ecc.

### Immutabilità Primitivi

I valori primitivi non possono essere modificati. Operazioni su stringhe, numeri, booleani creano nuovi valori invece di modificare quelli esistenti.

### Symbol

Introdotto in ES6 per creare identificatori unici. Ogni `Symbol()` è diverso da ogni altro, anche con la stessa descrizione.

## Esempio di Riferimento

```javascript
/* Tipi primitivi */

// string
let nome = "Mario";
let cognome = "Rossi";
let saluto = `Ciao ${nome}!`; // template literal (ES6)

// number (interi e decimali)
let intero = 42;
let decimale = 3.14;
let negativo = -10;
let infinito = Infinity;
let nonNumero = NaN; // Not a Number

// boolean
let vero = true;
let falso = false;
let maggiorenne = eta >= 18; // risultato di confronto

// null (assenza intenzionale)
let risultato = null;

// undefined (non inizializzato)
let indefinito;
console.log(indefinito); // undefined

let prop = obj.inesistente; // undefined

// symbol (identificatori unici)
let id1 = Symbol("id");
let id2 = Symbol("id");
console.log(id1 === id2); // false (sempre unici)

// object (strutture complesse)
let persona = {
  nome: "Mario",
  eta: 30,
  citta: "Roma",
};

let numeri = [1, 2, 3, 4, 5]; // array è object
let data = new Date(); // Date è object

/* Immutabilità primitivi */
let str = "ciao";
str.toUpperCase(); // crea nuovo valore
console.log(str); // "ciao" (originale invariato)

let strUpper = str.toUpperCase();
console.log(strUpper); // "CIAO" (nuovo valore)

/* Oggetti sono mutabili */
let arr = [1, 2, 3];
arr.push(4); // modifica l'array originale
console.log(arr); // [1, 2, 3, 4]

let obj = { x: 1 };
obj.x = 2; // modifica l'oggetto
console.log(obj); // { x: 2 }

/* Symbol per proprietà uniche */
let ID = Symbol("userId");
let utente = {
  [ID]: 12345,
  nome: "Anna",
};
console.log(utente[ID]); // 12345
console.log(utente.nome); // "Anna"

/* Casi pratici */
// null per assenza esplicita
let searchResult = null; // nessun risultato
if (searchResult === null) {
  console.log("Nessun risultato");
}

// undefined per valori mancanti
function saluta(nome) {
  if (nome === undefined) {
    nome = "Ospite";
  }
  return "Ciao " + nome;
}
console.log(saluta()); // "Ciao Ospite"
```

## Punti Chiave

1. **7 tipi totali**: 6 primitivi (string, number, boolean, null, undefined, symbol) + object

2. **Primitivi immutabili**: Operazioni creano nuovi valori, non modificano l'originale

3. **Object mutabili**: Modifiche alterano l'oggetto originale (passaggio per riferimento)

4. **null vs undefined**:
   - `null` → assenza intenzionale (assegnato esplicitamente)
   - `undefined` → valore non assegnato (default)

5. **NaN**: Tipo `number` ma rappresenta errore di calcolo. Non uguale a se stesso

6. **Symbol**: Sempre unici, utili per proprietà "private" di oggetti o come chiavi uniche

7. **Array e funzioni**: Sono tipi speciali di object

## Collegamenti

- [[typeof]] - Operatore per verificare il tipo di un valore
- [[tipizzazione-dinamica]] - Le variabili non hanno tipo fisso
- [[../oggetti/oggetti]] - Approfondimento sul tipo object
- [[../variabili/variabili]] - I contenitori che memorizzano valori tipizzati
