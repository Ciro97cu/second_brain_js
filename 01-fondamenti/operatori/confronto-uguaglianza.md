# [[../../appunti-completi#5-operatori|Operatori di Confronto ed Uguaglianza]]

Gli operatori di confronto restituiscono un valore booleano (`true`/`false`) basato sulla relazione tra due valori.

## Uguaglianza/Disuguaglianza

- `===` → uguaglianza stretta (stesso tipo E valore)
- `!==` → non uguaglianza stretta
- `==` → uguaglianza lasca (con coercizione)
- `!=` → non uguaglianza lasca

## Relazionali

- `<` → minore di
- `>` → maggiore di
- `<=` → minore o uguale
- `>=` → maggiore o uguale

## === vs ==

**===** (Stretta): Confronta tipo e valore. Nessuna conversione.

- `5 === 5` → `true`
- `5 === "5"` → `false` (tipi diversi)

**==** (Lasca): Converte i tipi prima del confronto.

- `5 == "5"` → `true` (stringa convertita a numero)
- `null == undefined` → `true` (caso speciale)

**Regola sicurezza con ==**: Evitare se uno dei valori potrebbe essere `true`, `false`, `0`, `""`, `[]`.

## Confronto di Oggetti/Array

Sia `==` che `===` confrontano il **riferimento** in memoria, non il contenuto.

```javascript
[1, 2] === [1, 2]; // false (riferimenti diversi)
let a = [1, 2];
let b = a;
a === b; // true (stesso riferimento)
```

## Operatori Relazionali

Con **stringhe**: confronto lessicografico (alfabetico).
Con **altri tipi**: conversione a numero.

**Attenzione**: Se la conversione produce `NaN`, il confronto è sempre `false`.

## Esempio di Riferimento

```javascript
/* Confronto ed uguaglianza */

// === (uguaglianza stretta)
console.log(5 === 5); // true
console.log(5 === "5"); // false (tipi diversi)
console.log(true === 1); // false
console.log(null === undefined); // false

// == (uguaglianza lasca)
console.log(5 == "5"); // true (coercizione)
console.log(true == 1); // true
console.log(null == undefined); // true (speciale)


// Uso sicuro di ==
let input = "42";
if (input == 42) {
  // Sicuro
  console.log("Match numero");
}

let val = null;
if (val == null) {
  // Sicuro: cattura null E undefined
  console.log("Non definito");
}

// Oggetti e array (confronto per riferimento)
let arr1 = [1, 2, 3];
let arr2 = [1, 2, 3];
let arr3 = arr1;

console.log(arr1 === arr2); // false (array diversi)
console.log(arr1 === arr3); // true (stesso riferimento)

let obj1 = { x: 1 };
let obj2 = { x: 1 };
console.log(obj1 === obj2); // false (oggetti diversi)

// Operatori relazionali - numeri
console.log(10 > 5); // true
console.log(3 <= 3); // true
console.log(7 < 2); // false

// Stringhe (lessicografico)
console.log("apple" < "banana"); // true
console.log("10" < "9"); // true (confronto caratteri: "1" < "9")


// Casi speciali con null
console.log(null > 0); // false
console.log(null == 0); // false
console.log(null >= 0); // true ⚠️ (null → 0)
```

## Punti Chiave

1. **Preferire ===**: Evita sorprese della coercizione. Usare `==` solo quando serve coercizione consapevole

2. **== null**: Utile per catturare sia `null` che `undefined` in un solo controllo

3. **Oggetti/Array**: Confrontano riferimenti. Per confronto contenuto serve logica custom o librerie

4. **NaN**: Non uguale a niente (nemmeno se stesso). Usare `isNaN()` o `Number.isNaN()`

5. **Stringhe**: Confronto carattere per carattere. `"10" < "9"` è `true` (confronto stringhe, non numeri)

6. **null >= 0**: `true` per coercizione, ma `null == 0` è `false` (caso speciale)

## Collegamenti

- [[operatori/logici]] - Combinare confronti nelle condizioni
- [[../tipi/coercizione]] - Differenza tra == (con coercizione) e === (senza)
- [[../tipi/valori-tipi]] - I tipi confrontabili
