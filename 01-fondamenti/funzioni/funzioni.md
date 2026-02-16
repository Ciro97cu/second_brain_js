# Funzioni (Functions)

Una **funzione** è un blocco di codice riutilizzabile progettato per eseguire un compito specifico. Organizza il codice in pezzi logici evitando ripetizioni.

## Anatomia di una Funzione

```javascript
function somma(a, b) {
  // dichiarazione con parametri
  return a + b; // return restituisce valore
}

let risultato = somma(5, 3); // 5 e 3 sono argomenti
console.log(risultato); // 8
```

**Componenti**:

- **Dichiarazione**: `function` + nome
- **Parametri**: variabili tra `()` che ricevono valori
- **Corpo**: codice tra `{}`
- **Return**: restituisce valore e termina esecuzione

Senza `return` esplicito, la funzione restituisce `undefined`.

## First-Class Citizens

Le funzioni sono **oggetti speciali** che possono essere:

- Assegnate a variabili
- Passate come argomenti
- Restituite da altre funzioni
- Dotate di proprietà

```javascript
// Assegnare a variabile
const miaFunzione = function (x) {
  return x * 2;
};

// Passare come argomento
function esegui(fn, valore) {
  return fn(valore);
}
esegui(miaFunzione, 5); // 10

// Restituire da funzione
function creaMultiplicatore(n) {
  return function (x) {
    return x * n;
  };
}
let doppio = creaMultiplicatore(2);
doppio(5); // 10

console.log(typeof miaFunzione); // "function"
```

## Hoisting

Le **function declarations** vengono "sollevate" in cima allo scope, permettendo di chiamarle prima della loro definizione nel codice.

```javascript
console.log(quadrato(5)); // ✅ 25 (funziona!)

function quadrato(n) {
  return n * n;
}

// Function expressions NON vengono sollevate
// console.log(cubo(3));  // ❌ Errore!
const cubo = function (n) {
  return n ** 3;
};
```

## Esecuzione Diretta vs Indiretta

```javascript
function saluta() {
  console.log("Ciao!");
}

// Esecuzione diretta
saluta(); // Esegue immediatamente

// Passare riferimento (esecuzione indiretta)
let riferimento = saluta; // NON esegue
setTimeout(riferimento, 1000); // Esegue dopo 1 secondo

// Comune con event listeners
button.addEventListener("click", saluta); // ✅ riferimento
// button.addEventListener("click", saluta());  // ❌ esecuzione immediata
```

## Collegamenti

- [[../oggetti]] - Le funzioni sono oggetti speciali
- [[iife]] - Pattern di funzione autoinvocante
- [[../blocchi]] - Le funzioni creano blocchi di scope
- [[../variabili/hoisting]] - Comportamento hoisting delle funzioni
- [[../array/array-iterazione]] - Funzioni come callback in map/filter/reduce
- [[../scope]] - Le funzioni creano scope locale
