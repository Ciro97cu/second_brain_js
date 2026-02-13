# Operatori Logici

Gli operatori logici combinano o invertono valori booleani. Sono fondamentali per costruire condizioni complesse.

## Operatori

- `&&` → AND logico (true se entrambi true)
- `||` → OR logico (true se almeno uno true)
- `!` → NOT logico (inverte il booleano)

## Short-Circuit Evaluation

JavaScript valuta le espressioni logiche da sinistra a destra e si ferma appena conosce il risultato:

**&&** (AND): Si ferma al primo valore falsy

- Se il primo è falsy, restituisce quello (non valuta il secondo)
- Se il primo è truthy, restituisce il secondo

**||** (OR): Si ferma al primo valore truthy

- Se il primo è truthy, restituisce quello (non valuta il secondo)
- Se il primo è falsy, restituisce il secondo

## Valori Falsy/Truthy

**Falsy** (considerati false): `false`, `0`, `""`, `null`, `undefined`, `NaN`

**Truthy** (tutto il resto): `true`, numeri non-zero, stringhe non vuote, oggetti, array

## Esempio di Riferimento

```javascript
/* Operatori logici */

// && (AND)
console.log(true && true); // true
console.log(true && false); // false
console.log(false && true); // false
console.log(false && false); // false

let eta = 25;
let haPatente = true;
if (eta >= 18 && haPatente) {
  console.log("Può guidare");
}

// || (OR)
console.log(true || false); // true
console.log(false || true); // true
console.log(false || false); // false
console.log(true || true); // true

let isWeekend = false;
let isFestivo = true;
if (isWeekend || isFestivo) {
  console.log("Non si lavora");
}

// ! (NOT)
console.log(!true); // false
console.log(!false); // true
console.log(!!true); // true (doppio NOT)

let piove = false;
if (!piove) {
  console.log("Niente ombrello");
}

// Short-circuit con &&
let user = null;
let nome = user && user.nome; // null (si ferma a user)
console.log(nome); // null (no error!)

let obj = { nome: "Mario" };
let n = obj && obj.nome; // "Mario"
console.log(n);

// Short-circuit con ||
let input = "";
let val = input || "default"; // "default"
console.log(val);

let numero = 0;
let num = numero || 100; // 100 (0 è falsy)
console.log(num);

// Combinare operatori
let temp = 25;
let sole = true;
let weekend = false;

if ((temp > 20 && sole) || weekend) {
  console.log("Bella giornata!");
}

// Uso pratico: validazione
function saluta(persona) {
  let nome = persona && persona.nome;
  console.log("Ciao " + (nome || "ospite"));
}

saluta({ nome: "Anna" }); // "Ciao Anna"
saluta(null); // "Ciao ospite"
saluta({}); // "Ciao ospite"

// Catena di OR per default
function configura(opts) {
  opts = opts || {};
  let timeout = opts.timeout || 3000;
  let retry = opts.retry || 3;
  return { timeout, retry };
}

console.log(configura()); // { timeout: 3000, retry: 3 }
console.log(configura({ timeout: 5000 })); // { timeout: 5000, retry: 3 }

// Evitare esecuzione con &&
let debug = true;
debug && console.log("Debug attivo"); // esegue solo se debug è true

let arr = [1, 2, 3];
arr.length > 0 && console.log("Array non vuoto");
```

## Punti Chiave

1. **Short-circuit**: Gli operatori si fermano appena possibile, utile per evitare errori (`obj && obj.prop`)

2. **&& restituisce**: Primo valore falsy, oppure l'ultimo valore se tutti truthy

3. **|| restituisce**: Primo valore truthy, oppure l'ultimo valore se tutti falsy

4. **Problema con ||**: Scarta valori falsy validi come `0` o `""`. Per default, considerare `??` (coalescenza nullish)

5. **! doppio (!!)**: Converte esplicitamente a booleano (`!!0` → `false`, `!!"test"` → `true`)

6. **Precedenza**: `!` ha massima precedenza, poi `&&`, infine `||`

## Collegamenti

- [[operatori/confronto-uguaglianza]] - I confronti producono booleani usati con operatori logici
- [[operatori/speciali]] - L'operatore ?? è alternativa a || per default
- [[tipizzazione-dinamica]] - Valori falsy/truthy nella coercizione
