# Precedenza degli Operatori

La precedenza (operator precedence) stabilisce l'ordine in cui gli operatori vengono valutati in un'espressione complessa.

## Principio Base

Come in matematica, alcuni operatori hanno priorità su altri. La moltiplicazione viene eseguita prima dell'addizione: `2 + 3 * 4` = `2 + 12` = `14`.

## Parentesi

Le parentesi `()` hanno la massima priorità e forzano l'ordine di valutazione.

`(2 + 3) * 4` = `5 * 4` = `20`

## Ordine di Precedenza Comune

Dal **più alto** (eseguito prima) al **più basso**:

1. `()` — parentesi
2. `++`, `--` — incremento/decremento
3. `!` — NOT logico
4. `**` — esponenziazione
5. `*`, `/`, `%` — moltiplicazione, divisione, resto
6. `+`, `-` — addizione, sottrazione
7. `<`, `>`, `<=`, `>=` — relazionali
8. `==`, `===`, `!=`, `!==` — uguaglianza
9. `&&` — AND logico
10. `||` — OR logico
11. `??` — coalescenza nullish
12. `? :` — ternario
13. `=`, `+=`, `-=`, etc. — assegnamento

## Associatività

Operatori con stessa precedenza vengono valutati secondo l'associatività:

**Sinistra → Destra**: `+`, `-`, `*`, `/`, `%`

- `10 - 3 + 2` = `(10 - 3) + 2` = `9`

**Destra → Sinistra**: `**`, `=`, `? :`

- `2 ** 3 ** 2` = `2 ** (3 ** 2)` = `2 ** 9` = `512`

## Esempio di Riferimento

```javascript
/* Precedenza degli operatori */

// Aritmetica base
console.log(2 + 3 * 4); // 14 (prima *, poi +)
console.log((2 + 3) * 4); // 20 (parentesi forzano +)

console.log(10 + 5 * 2); // 20 (moltiplicazione prima)
console.log((10 + 5) * 2); // 30 (addizione forzata prima)

// Esponenziazione (destra → sinistra)
console.log(2 ** (3 ** 2)); // 512 (2 ** 9)
console.log((2 ** 3) ** 2); // 64 (8 ** 2)

// Stessa precedenza (sinistra → destra)
console.log(10 - 3 + 2); // 9 ((10-3)+2)
console.log(10 - (3 + 2)); // 5

console.log((20 / 4) * 2); // 10 ((20/4)*2)
console.log(20 / (4 * 2)); // 2.5

// Confronti e logica
let a = 5;
let b = 10;

console.log(a < 10 && b > 5); // true (confronti prima di &&)
console.log((a < 10 && b > 5) || false); // true (&& prima di ||)
console.log(a < 10 && (b > 5 || false)); // true (parentesi cambiano)

// Espressione complessa
let x = 3;
let y = 4;
let result = x + y * 2 > 10 ? "Grande" : "Piccolo";
// Ordine: y*2 → x+8 → 11>10 → true → "Grande"
console.log(result); // "Grande"

// NOT ha alta precedenza
console.log(!false && true); // true (NOT prima di &&)
console.log(!(false && true)); // true

// Assegnamento (ultima precedenza)
let val = 5 + 3; // prima calcola 5+3, poi assegna
console.log(val); // 8

let sum = (a = b = 10); // assegnamenti (destra → sinistra)
console.log(sum, a, b); // 10, 10, 10

// Best practice: parentesi per chiarezza
let prezzo = 100;
let tasse = 20;
let sconto = 0.1;

// ❌ Difficile da leggere
let totale1 = prezzo + tasse * 1 - sconto;

// ✅ Chiaro con parentesi
let totale2 = (prezzo + tasse) * (1 - sconto);

// Ternario ha bassa precedenza
let age = 20;
let tipo = age >= 18 ? "adulto" : "minore";
let msg = "Tipo: " + tipo; // concatenazione prima del ternario

// Coalescenza nullish
let count = 0;
let def = count ?? 10; // ?? ha bassa precedenza
console.log(def); // 0

// ⚠️ Non si può mescolare ?? con && o || senza parentesi
// let mixed = true || false ?? true; // SyntaxError
let mixed = (true || false) ?? true; // ✅ Parentesi obbligatorie
```

## Punti Chiave

1. **Parentesi**: Sempre sicure. Usarle per chiarezza anche quando non strettamente necessarie

2. **Matematica standard**: `*`, `/`, `%` prima di `+`, `-`

3. **Confronti prima di logica**: `<`, `>` prima di `&&`, che viene prima di `||`

4. **Assegnamento ultimo**: `=` e varianti hanno la precedenza più bassa

5. **Esponenziazione**: Unico operatore con associatività destra-sinistra

6. **?? con && o ||**: Richiedono parentesi esplicite (regola del linguaggio)

7. **Leggibilità > Brevità**: Se ci sono dubbi, usa parentesi per rendere chiaro l'intento

## Collegamenti

- [[operatori/matematici]] - Operatori matematici e loro precedenza
- [[operatori/logici]] - AND ha precedenza su OR
- [[expression]] - Le espressioni vengono valutate secondo precedenza
