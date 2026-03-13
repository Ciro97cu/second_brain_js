# [[../../appunti-completi#Valori Truthy|Lista dei Valori Truthy]]

Un valore **truthy** è qualsiasi entità in JavaScript che, sottoposta a coercizione booleana implicita, restituisce il valore `true`.

Dato che i valori falsy costituiscono una lista definita e limitata, la regola per identificare i valori truthy è semplice: **tutto ciò che non è falsy è truthy**.

## Esempi Comuni di Valori Truthy

La categoria dei valori truthy comprende sia tipi primitivi che oggetti complessi. Alcuni esempi classici includono:

```javascript
/*
 * Esempi rappresentativi di valori truthy
 */

// Stringhe non vuote
"testo"         // truthy
"0"             // truthy (stringa contente carattere '0')
"false"         // truthy (stringa contente la parola 'false')
" "             // truthy (spazio vuoto, non stringa di lunghezza zero)

// Numeri diversi dallo zero
42              // truthy
-1              // truthy
3.14            // truthy
Infinity        // truthy
-Infinity       // truthy

// Funzioni e Classi
function() {}   // truthy
class MyClass {} // truthy

// Date e Simboli
new Date()      // truthy
Symbol()        // truthy
```

## Casi Controintuitivi (Oggetti e Array Vuoti)

Una delle cause principali di bug in JavaScript riguarda le strutture dati vuote. **Tutti gli oggetti e gli array sono truthy, inclusi quelli vuoti**.

Questo accade perché la coercizione valuta la presenza in memoria di un oggetto istanziato, prescindendo dalle proprietà al suo interno.

```javascript
/*
 * Array e oggetti vuoti sono truthy
 */

let arrayVuoto = [];
if (arrayVuoto) {
  console.log("Viene eseguito!"); // ✅ Eseguito
}

let oggettoVuoto = {};
if (oggettoVuoto) {
  console.log("Viene eseguito!"); // ✅ Eseguito
}
```

### Controllo Corretto di Array e Oggetti Vuoti

Per evitare logiche fallaci quando si determina se una collezione contiene elementi, è necessario ispezionarne proprietà specifiche e non basarsi sulla valutazione truthy dell'oggetto stesso.

```javascript
let risultati = [];

// Sbagliato: passa sempre, l'array esiste
if (risultati) {
  // ...
}

// Corretto: verifica la lunghezza numerica (coercizione implicita di number)
// length > 0 è truthy, length === 0 è falsy
if (risultati.length) {
  // ...
}

let config = {};

// Corretto: verifica la quantità di chiavi dell'oggetto
if (Object.keys(config).length) {
  // ...
}
```
