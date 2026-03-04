# Closure: Pattern Pratici [[../../appunti-completi#closure|📚]]

## 📦 Factory Functions

Le closure permettono di creare **factory functions** che generano funzioni specializzate:

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

### Esempio: Formattatori

```javascript
function makeFormatter(prefix, suffix) {
  return function (str) {
    return prefix + str + suffix;
  };
}

const makeTag = makeFormatter("<p>", "</p>");
const makeBold = makeFormatter("<b>", "</b>");

console.log(makeTag("Hello")); // <p>Hello</p>
console.log(makeBold("World")); // <b>World</b>
```

## 🔒 Dati Privati (Incapsulamento)

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

La variabile `count` è **completamente privata**: l'unico modo per accedervi è attraverso i metodi pubblici (`increment`, `decrement`, `getValue`). Questo è incapsulamento vero.

### Esempio: Bank Account

```javascript
function createBankAccount(initialBalance) {
  let balance = initialBalance; // Privata

  return {
    deposit: function (amount) {
      if (amount > 0) {
        balance += amount;
        return balance;
      }
      throw new Error("Amount must be positive");
    },
    withdraw: function (amount) {
      if (amount > balance) {
        throw new Error("Insufficient funds");
      }
      balance -= amount;
      return balance;
    },
    getBalance: function () {
      return balance;
    },
  };
}

const account = createBankAccount(1000);
console.log(account.deposit(500)); // 1500
console.log(account.withdraw(200)); // 1300
// account.balance = 99999; // ❌ Non funziona, balance è privato!
```

## 🔄 Closure nei Loop (Problema Classico)

Un errore comune è non comprendere come le closure si comportano nei loop:

### ❌ Il Problema con `var`

```javascript
for (var i = 1; i <= 3; i++) {
  setTimeout(function () {
    console.log(i); // 4, 4, 4 (non 1, 2, 3!)
  }, i * 1000);
}
```

**Perché stampa `4, 4, 4`?**

- `var` ha **function scope** (non block scope)
- Tutte e 3 le closure fanno riferimento alla **stessa variabile `i`**
- Quando i setTimeout si attivano, il loop è già finito e `i` vale `4`

### ✅ Soluzione 1: Usa `let` (Block Scope)

```javascript
for (let i = 1; i <= 3; i++) {
  setTimeout(function () {
    console.log(i); // 1, 2, 3 ✅
  }, i * 1000);
}
```

**Perché funziona?**

- `let` ha **block scope**
- Ogni iterazione crea un **nuovo scope** con una nuova `i`
- Ogni closure cattura la propria copia di `i`

### ✅ Soluzione 2: IIFE (Immediately Invoked Function Expression)

```javascript
for (var i = 1; i <= 3; i++) {
  (function (j) {
    setTimeout(function () {
      console.log(j); // 1, 2, 3 ✅
    }, j * 1000);
  })(i);
}
```

**Perché funziona?**

- L'IIFE crea un **nuovo scope** per ogni iterazione
- `j` è un parametro della funzione, quindi ogni iterazione ha la sua copia
- La closure del setTimeout cattura `j`, non `i`

## ✅ Punti Chiave

1. **Factory Functions** - Creano funzioni specializzate con configurazione chiusa
2. **Dati Privati** - Incapsulamento vero senza classi
3. **Loop Problem** - `var` condivide scope, `let` crea nuovo scope per iterazione
4. **IIFE** - Crea scope isolati quando necessario

## 🔗 Collegamenti

- [[closure-concept|Concetto di Closure]] - Definizione e funzionamento base
- [[closure-transport-mechanisms|Meccanismi di Trasporto]] - Come le funzioni viaggiano
- [[iife|IIFE]] - Immediately Invoked Function Expression
- [[module-pattern|Module Pattern]] - Pattern basato su closure
- [[../../appunti-completi#closure|Closure Completo]]

## 📚 Risorse

- "You Don't Know JS" - Scope & Closures
- JavaScript Design Patterns

## 📌 Tag

#javascript #closure #factory-pattern #private-variables #iife #loop-closure #incapsulamento
