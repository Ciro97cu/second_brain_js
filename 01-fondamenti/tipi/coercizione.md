# Coercizione (Type Coercion)

La **coercizione** è il processo di conversione di un valore da un tipo a un altro in JavaScript. Può essere esplicita (richiesta dal programmatore) o implicita (eseguita automaticamente dal linguaggio).

## Coercizione Esplicita

Il programmatore converte deliberatamente un tipo usando funzioni dedicate. L'intenzione è chiara e il risultato prevedibile.

**Funzioni principali**:

- `Number()` → converte a number
- `String()` → converte a string
- `Boolean()` → converte a boolean
- `parseInt()` / `parseFloat()` → converte string a integer/float

```javascript
// String → Number
let prezzo = "99.99";
let prezzoNumerico = Number(prezzo); // 99.99

let quantita = "42";
let quantitaInt = parseInt(quantita); // 42

// Number → String
let numero = 42;
let numeroStringa = String(numero); // "42"

// Any → Boolean
console.log(Boolean(1)); // true
console.log(Boolean(0)); // false
console.log(Boolean("")); // false
console.log(Boolean("testo")); // true
```

## Coercizione Implicita

JavaScript converte automaticamente i tipi quando incontra operazioni tra tipi diversi.

**Casi comuni**:

- Operatore `==` (uguaglianza lasca)
- Operatore `+` con string
- Contesti booleani (if, while)

```javascript
// == converte automaticamente
console.log("99.99" == 99.99); // true (string → number)
console.log(42 == "42"); // true
console.log(true == 1); // true
console.log(null == undefined); // true

// + con string concatena
console.log(5 + 3); // 8 (number + number)
console.log("5" + 3); // "53" (concatenazione)

// Altri operatori convertono a number
console.log("10" - 5); // 5
console.log("10" * "2"); // 20

// Contesto booleano
if ("testo") {
  // string non vuota → true
}
if (0) {
  // 0 → false
}
```

## Controversia e Best Practice

La coercizione implicita è controversa: alcuni la evitano sempre preferendo `===`, altri la usano consapevolmente per codice più espressivo.

**Raccomandazioni**:

1. **Preferire `===`** per evitare sorprese
2. **Usare `==` consapevolmente** quando vantaggioso (es. `value == null` cattura sia null che undefined)
3. **Evitare `==`** con: `true`, `false`, `0`, `""`, `[]`
4. **Coercizione esplicita** quando la conversione è il cuore della logica

```javascript
// ❌ Implicita confusa
if (prezzoInput == 0) {
  // cattura "", [], false
}

// ✅ Esplicita chiara
if (Number(prezzoInput) === 0) {
  // prevedibile
}

// ✅ Caso valido per ==
if (value == null) {
  // cattura null E undefined elegantemente
}
```

## Collegamenti

- [[valori-tipi]] - I 7 tipi primitivi e object
- [[tipizzazione-dinamica]] - Variabili non legate a un tipo
- [[../oggetti/oggetti]] - Conversione tra tipi e object
- [[../operatori/confronto-uguaglianza]] - Differenza tra == e ===
- [[typeof]] - Determinare il tipo di un valore
