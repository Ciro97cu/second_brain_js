# [[../../appunti-completi#25-blocchi-di-codice-code-blocks|Blocchi di Codice (Code Blocks)]]

Un **blocco** (block) è un gruppo di una o più istruzioni racchiuse tra parentesi graffe `{ ... }`. Raggruppa istruzioni che appartengono logicamente insieme, creando un'unità di codice trattata come singolo elemento.

## Uso con Strutture di Controllo

I blocchi sono tipicamente associati a **strutture di controllo** (`if`, `else`, `for`, `while`) per definire quali istruzioni eseguire in base a condizioni.

```javascript
// Blocco con if-else
let temperatura = 30;
if (temperatura > 25) {
  console.log("Fa caldo");
  console.log("Prendi dell'acqua");
} else {
  console.log("Temperatura normale");
}

// Blocco con ciclo
for (let i = 0; i < 3; i++) {
  console.log("Iterazione:", i);
}

// Blocchi annidati
if (numero > 0) {
  console.log("Positivo");
  if (numero > 10) {
    console.log("Maggiore di 10");
  }
}
```

## Block Scope

Le variabili dichiarate con `let` e `const` hanno **block scope**: esistono solo all'interno del blocco in cui sono dichiarate.

```javascript
{
  let x = 10;
  const y = 20;
  console.log(x, y); // ✅ 10, 20
}
// console.log(x); // ❌ ReferenceError

// var ha function scope (non block scope)
{
  var z = 30;
}
console.log(z); // ✅ 30 - accessibile fuori dal blocco
```

## Blocchi Autonomi

Raramente usati, ma utili per limitare lo scope di variabili temporanee:

```javascript
let totale = 0;
{
  let prezzo = 19.99;
  let quantita = 3;
  totale = prezzo * quantita;
}
console.log(totale); // ✅ 59.97
// console.log(prezzo); // ❌ Non accessibile
```

## Regola Punto e Virgola

I blocchi **non richiedono** punto e virgola (`;`) dopo la parentesi graffa di chiusura.

```javascript
if (true) {
  console.log("OK");
} // ← No ;

// Eccezione: assegnamenti richiedono ;
let funzione = function () {
  console.log("Funzione");
}; // ← Necessario (è un assegnamento)
```

## Collegamenti

- [[statement]] - I blocchi raggruppano statement
- [[../variabili/variabili]] - let/const hanno block scope
- [[../funzioni/funzioni]] - Le funzioni creano scope con blocchi
- [[expression]] - Le espressioni si usano nelle istruzioni dei blocchi
- [[../scope/scope]] - Block scope con let/const
