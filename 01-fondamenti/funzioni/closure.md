# [[../../appunti-completi#39-closure-chiusura|Closure (Chiusura)]]

La **Closure** (o chiusura) è uno dei concetti più importanti in JavaScript. È la capacità di una funzione di **"ricordare"** e accedere al proprio scope anche dopo che la funzione esterna ha terminato l'esecuzione.

Una **funzione interna** mantiene un riferimento vivo alle variabili della **funzione esterna**.

## Esempio Base

```javascript
function makeAdder(x) {
  function add(y) {
    return x + y; // 'add' ricorda 'x'
  }
  return add;
}

let plusOne = makeAdder(1); // Closure che ricorda x = 1
let plusTen = makeAdder(10); // Closure che ricorda x = 10

console.log(plusOne(3)); // 4  (1 + 3)
console.log(plusTen(13)); // 23 (10 + 13)
```

**Come funziona**: Ogni chiamata a `makeAdder()` crea un **nuovo scope** con una propria copia di `x`. La funzione `add` restituita "ricorda" il valore di `x` del suo scope, anche dopo che `makeAdder` ha terminato.

## Uso Pratico: Dati Privati

Le closure permettono di creare **variabili private** in JavaScript:

```javascript
function counter() {
  let count = 0; // Variabile privata

  return {
    increment: function () {
      count++;
      return count;
    },
    decrement: function () {
      count--;
      return count;
    },
    getValue: function () {
      return count;
    },
  };
}

let myCounter = counter();
console.log(myCounter.increment()); // 1
console.log(myCounter.increment()); // 2
console.log(myCounter.getValue()); // 2

// ❌ Non posso accedere direttamente a count
console.log(myCounter.count); // undefined
```

## Closure nei Loop (Problema Classico)

Un errore comune è non comprendere come le closure si comportano nei loop:

```javascript
// ❌ Problema: tutte le funzioni condividono lo stesso 'i'
for (var i = 1; i <= 3; i++) {
  setTimeout(function () {
    console.log(i); // 4, 4, 4 (non 1, 2, 3!)
  }, i * 1000);
}

// ✅ Soluzione 1: Usa let (block scope)
for (let i = 1; i <= 3; i++) {
  setTimeout(function () {
    console.log(i); // 1, 2, 3
  }, i * 1000);
}

// ✅ Soluzione 2: Crea closure esplicita
for (var i = 1; i <= 3; i++) {
  (function (j) {
    setTimeout(function () {
      console.log(j); // 1, 2, 3
    }, j * 1000);
  })(i);
}
```

## Riepilogo

Le **closure** permettono:

- Funzioni che **ricordano** il loro scope lessicale
- Creazione di **variabili private** (incapsulamento)
- Implementazione di **factory functions** e **module pattern**

**Regola chiave**: Una funzione ha sempre accesso alle variabili del suo scope esterno, anche dopo che quello scope ha terminato l'esecuzione.

## Collegamenti

- [[funzioni]] - Le funzioni come first-class citizens
- [[module-pattern]] - Module Pattern basato su closure
- [[iife]] - IIFE per creare scope isolati
- [[../scope/scope]] - Scope lessicale e closure
