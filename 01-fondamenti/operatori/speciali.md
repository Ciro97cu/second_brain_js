# [[../../appunti-completi#5-operatori|Operatori Speciali]]

Operatori con comportamenti particolari per casi d'uso specifici.

## Operatori

- `? :` → operatore ternario (condizionale compatto)
- `??` → coalescenza nullish (default per null/undefined)
- `!!` → doppio NOT (conversione a booleano)

## Operatore Ternario (? :)

Sintassi compatta per espressioni condizionali:

```javascript
condizione ? valoreSeVero : valoreSeFalso;
```

È l'unico operatore JavaScript con tre operandi.

## Coalescenza Nullish (??)

Restituisce il valore a destra solo se quello a sinistra è `null` o `undefined`.

**Differenza da ||**:

- `||` → scarta tutti i falsy (`0`, `""`, `false`)
- `??` → scarta solo `null` e `undefined`

Utile quando `0`, `""` o `false` sono valori validi.

## Doppio NOT (!!)

Non è un operatore unico, ma uso di `!` due volte per convertire esplicitamente qualsiasi valore al suo equivalente booleano.

## Esempio di Riferimento

```javascript
/* Operatori speciali */

// Ternario - base
let eta = 20;
let tipo = eta >= 18 ? "adulto" : "minore";
console.log(tipo); // "adulto"

// Equivalente if-else
let tipoAlt;
if (eta >= 18) {
  tipoAlt = "adulto";
} else {
  tipoAlt = "minore";
}

// Ternario in espressioni
let punti = 85;
console.log("Hai " + (punti >= 60 ? "passato" : "fallito"));

// Ternari annidati (con cautela!)
let voto = 75;
let giudizio =
  voto >= 90
    ? "Eccellente"
    : voto >= 70
      ? "Buono"
      : voto >= 60
        ? "Sufficiente"
        : "Insufficiente";
console.log(giudizio); // "Buono"

// Coalescenza Nullish (??)
let contatore = 0;
console.log(contatore || 10); // 10 ⚠️ (0 è falsy)
console.log(contatore ?? 10); // 0 ✅ (0 è valido)

let testo = "";
console.log(testo || "default"); // "default" ⚠️
console.log(testo ?? "default"); // "" ✅

let val = null;
console.log(val ?? "N/D"); // "N/D"

let num = undefined;
console.log(num ?? 100); // 100

// Uso pratico: configurazione con default
function setup(opts) {
  let timeout = opts.timeout ?? 3000; // 0 è valore valido
  let retry = opts.maxRetry ?? 3;
  let msg = opts.message ?? "Caricamento...";
  return { timeout, retry, msg };
}

console.log(setup({ timeout: 0 }));
// { timeout: 0, retry: 3, msg: "Caricamento..." } ✅

console.log(setup({ timeout: 0 }).timeout || 3000);
// 3000 ⚠️ Con || avremmo perso lo 0

// Doppio NOT (!!)
console.log(!!"Hello"); // true (truthy)
console.log(!!42); // true
console.log(!!0); // false (falsy)
console.log(!!""); // false
console.log(!!null); // false
console.log(!!undefined); // false
console.log(!![]); // true (array vuoto è truthy)
console.log(!!{}); // true (oggetto vuoto è truthy)

// Come funziona !!
let valore = "test";
console.log(!valore); // false (NOT: truthy → false)
console.log(!!valore); // true (NOT NOT: false → true)

// Uso pratico
function haValore(x) {
  return !!x;
}
console.log(haValore("test")); // true
console.log(haValore("")); // false
console.log(haValore(0)); // false
console.log(haValore(null)); // false

// Alternativa più esplicita
function haValoreBis(x) {
  return Boolean(x); // stesso risultato di !!x
}

// !! è ridondante nelle condizioni
let input = "dati";
if (input) {
  // ✅ Preferibile
  console.log("Ha input");
}
if (!!input) {
  // Funziona ma superfluo
  console.log("Ha input");
}

// Utile per assegnamenti espliciti
let isValid = !!userData.email; // chiaro intento booleano
```

## Punti Chiave

1. **Ternario**: Utile per assegnamenti semplici. Evitare annidamenti complessi (usare if-else)

2. **?? vs ||**:
   - `??` → solo null/undefined
   - `||` → tutti i falsy
   - Preferire `??` quando `0`, `""`, `false` sono valori validi

3. **!!**: Conversione esplicita a booleano. Equivalente a `Boolean()`, ma più idiomatico in JavaScript

4. **!!** ridondante: Nelle condizioni if/while, la conversione è automatica

5. **Leggibilità**: Il ternario semplifica, ma non abusare. Se complesso, usa if-else

## Collegamenti

- [[operatori/logici]] - || è simile a ?? ma con comportamento diverso
- [[operatori/confronto-uguaglianza]] - Il ternario usa espressioni booleane
- [[../tipi/tipizzazione-dinamica]] - Valori falsy/truthy per !! e ??
