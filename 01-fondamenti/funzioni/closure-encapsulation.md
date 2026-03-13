# [[../../appunti-completi#39-scope-closure-e-illuminazione-enlightenment|Closure: Incapsulamento e Dati Privati]]

## 🔒 Dati Privati

Le closure permettono di creare **variabili private** in JavaScript, un meccanismo fondamentale per implementare l'incapsulamento senza ricorrere necessariamente alle classi.

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

// ❌ Non si può accedere direttamente a count
console.log(myCounter.count); // undefined
```

La variabile `count` è **completamente privata**: l'unico modo per accedervi o modificarla è attraverso i metodi pubblici restituiti (`increment`, `decrement`, `getValue`). Questo rappresenta un incapsulamento reale e sicuro.

### Esempio Pratico: Conto Bancario

Un caso d'uso classico è la protezione dei dati sensibili o dello stato critico di un oggetto:

```javascript
function createBankAccount(initialBalance) {
  let balance = initialBalance; // Variabile privata

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

// ❌ Tentativo di manipolazione diretta fallisce
// account.balance = 99999; (Non modifica il balance reale interno)
```

In questo design, la logica di validazione non può essere bypassata modificando direttamente il saldo, garantendo l'integrità dei dati.

## ✅ Punti Chiave

1. **Incapsulamento** - Protezione dello stato interno esponendo solo un'API pubblica.
2. **Sicurezza dei Dati** - Impossibilità di bypassare le logiche di validazione.
3. **Alternativa alle Classi** - Pattern per ottenere dati privati senza sintassi di classe complessa.

## 🔗 Collegamenti

- [[closure-concept|Concetto di Closure]]
- [[closure-factory-functions|Factory Functions]]
- [[module-pattern|Module Pattern]]

## 📚 Risorse

- "You Don't Know JS" - Scope & Closures
- JavaScript Design Patterns

## 📌 Tag

#javascript #closure #private-variables #incapsulamento #design-patterns
