# [[../../appunti-completi#310-module-pattern|Module Pattern]]

L'uso più comune della closure in JavaScript è il **Module Pattern**. Permette di definire dettagli **privati** (variabili e funzioni nascoste) e un'**interfaccia pubblica** (API esposta). È una tecnica fondamentale per l'**incapsulamento** e l'**organizzazione del codice**.

## Esempio Base

```javascript
function User() {
  // Variabili private
  let username;
  let password;

  // Funzione privata
  function doLogin(user, pw) {
    username = user;
    password = pw;
    console.log("Login effettuato per:", username);
  }

  // API pubblica
  let publicAPI = {
    login: doLogin,
  };

  return publicAPI;
}

let fred = User();
fred.login("fred", "12Battery34!"); // OK

// ❌ Non accessibili
console.log(fred.username); // undefined
console.log(fred.doLogin); // undefined
```

**Come funziona**: La funzione `User()` crea uno **scope privato**. Le variabili e funzioni interne sono nascoste. Solo `publicAPI` viene esposto. La closure mantiene vivo l'accesso alle variabili private anche dopo che `User()` termina.

```javascript
// Ogni chiamata crea un'istanza separata
let user1 = User();
let user2 = User();

user1.login("alice", "pass123");
user2.login("bob", "pass456");
// user1 e user2 sono completamente indipendenti
```

## Module Pattern con IIFE (Singleton)

Una variante comune usa una **IIFE** per creare un modulo **singleton** (istanza unica):

```javascript
let bankAccount = (function () {
  // Stato privato
  let balance = 0;
  let transactions = [];

  // Funzioni private
  function recordTransaction(type, amount) {
    transactions.push({ type, amount, date: new Date() });
  }

  // API pubblica
  return {
    deposit: function (amount) {
      balance += amount;
      recordTransaction("deposit", amount);
      return balance;
    },
    withdraw: function (amount) {
      if (amount > balance) {
        console.log("Fondi insufficienti");
        return balance;
      }
      balance -= amount;
      recordTransaction("withdraw", amount);
      return balance;
    },
    getBalance: function () {
      return balance;
    },
    getTransactions: function () {
      return [...transactions]; // Copia per sicurezza
    },
  };
})();

bankAccount.deposit(500);
bankAccount.withdraw(100);
console.log(bankAccount.getBalance()); // 400

// ❌ Dati privati non accessibili
console.log(bankAccount.balance); // undefined
```

## Vantaggi

- **Incapsulamento** → Dati privati veramente privati
- **Organizzazione** → Codice strutturato e modulare
- **Namespace** → Evita inquinamento dello scope globale
- **Manutenibilità** → Modifiche interne senza impatto esterno

## Riepilogo

Il **Module Pattern** sfrutta le closure per creare **stato privato** e un'**interfaccia pubblica**. È un pattern fondamentale pre-ES6 per organizzare il codice, ora sostituito dai **moduli ES6** (`import`/`export`) che offrono la stessa separation of concerns con sintassi nativa.

## Collegamenti

- [[closure]] - Le closure permettono il Module Pattern
- [[iife]] - IIFE per creare singleton modules
- [[funzioni]] - Funzioni come factory
- [[../scope/scope]] - Scope privato e pubblico
