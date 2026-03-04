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

## 🔄 Cicli e Closure

L'esempio più comune e canonico utilizzato per illustrare la Closure coinvolge un semplice ciclo for. Spesso, questo scenario confonde gli sviluppatori, portando i Linters a segnalare errori quando si definiscono funzioni all'interno di cicli. Tuttavia, comprendendo la Closure, è possibile sfruttare questa struttura correttamente.

Si consideri il seguente codice, dal quale ci si aspetterebbe logicamente la stampa dei numeri da 1 a 5, uno al secondo:

```javascript
for (var i = 1; i <= 5; i++) {
  setTimeout(function timer() {
    console.log(i);
  }, i * 1000);
}
```

### Il Problema

Eseguendo questo codice, il risultato è sorprendente: viene stampato il numero **6 per cinque volte**.

Il motivo risiede nel fatto che la callback timer viene eseguita solo dopo che il ciclo ha terminato la sua esecuzione. La condizione di terminazione del ciclo è che i non sia più <= a 5, il che accade quando i diventa 6. Quindi, quando i timer scattano, accedono al valore corrente di i, che è appunto 6.

L'errore concettuale sta nel pensare che ogni iterazione del ciclo catturi una propria "copia" di "i". In realtà, a causa di come funziona lo Scope (specialmente con var), tutte e cinque le funzioni condividono lo stesso ambito globale e, di conseguenza, lo stesso riferimento all'unica variabile i.

### Soluzione con IIFE

Per risolvere il problema, è necessario creare uno Scope nuovo e dedicato per ogni iterazione del ciclo. Come visto in precedenza, l'IIFE è uno strumento eccellente per creare Scope.

Un primo tentativo potrebbe essere semplicemente avvolgere la funzione in una IIFE:

```javascript
for (var i = 1; i <= 5; i++) {
  (function () {
    setTimeout(function timer() {
      console.log(i);
    }, i * 1000);
  })();
}
```

**Questo non funziona ancora!** Il problema persiste.

Affinché la soluzione funzioni, il nuovo Scope creato dall'IIFE non deve essere vuoto: deve contenere una propria variabile che memorizzi il valore di i in quel preciso momento dell'iterazione. Si può passare i come argomento all'IIFE, creando così una variabile locale (nell'esempio chiamata j) che "congela" il valore:

```javascript
for (var i = 1; i <= 5; i++) {
  (function (j) {
    setTimeout(function timer() {
      console.log(j);
    }, j * 1000);
  })(i);
}
```

L'uso di un IIFE all'interno di ogni iterazione crea un nuovo Scope per ogni passaggio, offrendo alle funzioni di callback l'opportunità di effettuare una Closure su un valore specifico e corretto per quella iterazione.

### Block Scoping Rivisitato

Analizzando la soluzione precedente basata sulle IIFE, si nota che l'obiettivo fondamentale era creare un nuovo Scope per ogni iterazione del ciclo. In altre parole, era necessario uno Scope di blocco (Block Scope) per ogni iterazione.

Il Capitolo 3 ha introdotto la dichiarazione let, che permette di dichiarare una variabile valida limitatamente a un blocco. Questo trasforma essenzialmente il blocco in uno Scope su cui è possibile applicare la Closure. È quindi possibile semplificare il codice inserendo una dichiarazione let all'interno del ciclo for che utilizza ancora var nell'intestazione:

```javascript
for (var i = 1; i <= 5; i++) {
  let j = i; // Crea un nuovo scope di blocco per ogni iterazione
  setTimeout(function timer() {
    console.log(j);
  }, j * 1000);
}
```

Tuttavia, esiste un comportamento speciale e ancora più potente definito per le dichiarazioni let utilizzate direttamente nell'intestazione di un ciclo for.

Questo comportamento prevede che la variabile non venga dichiarata una sola volta per tutto il ciclo (come accade con var), ma venga dichiarata nuovamente per ogni singola iterazione. Inoltre, l'Engine si occupa di inizializzare la variabile ad ogni iterazione successiva con il valore che aveva alla fine dell'iterazione precedente.

Questo permette di ottenere il risultato desiderato senza l'uso di variabili d'appoggio o IIFE:

```javascript
for (let i = 1; i <= 5; i++) {
  setTimeout(function timer() {
    console.log(i);
  }, i * 1000);
}
```

In questo scenario, Block Scoping e Closure lavorano di concerto, risolvendo in modo elegante uno dei problemi più comuni nello sviluppo JavaScript.

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
