# [[../../appunti-completi#blocchi-come-scope-blocks-as-scopes|Block Scope: Concetto Base e Problemi con var]]

## 🎯 Concetto

Un **blocco** è una qualsiasi porzione di codice racchiusa tra parentesi graffe `{ ... }`. JavaScript moderno (ES6+) supporta il **block scope** con `let` e `const`, dove le variabili dichiarate in un blocco sono confinate a quel blocco e non visibili all'esterno.

**Prima di ES6**: Solo `var` (function scope, ignora i blocchi).
**Da ES6 in poi**: `let` e `const` (true block scope).

**Vantaggio**: Estende il **Principio del Minimo Privilegio**, permettendo di nascondere le informazioni all'interno di singoli blocchi di codice.

## 💻 Il Problema con var: Falso Block Scope

### Apparenza Ingannevole

```javascript
for (var i = 0; i < 5; i++) {
  // 'i' sembra confinata al loop...
  console.log(i);
}

console.log(i); // 5 - ⚠️ 'i' è ancora accessibile!
```

La variabile `i` viene dichiarata nell'intestazione del `for`, con l'intenzione di usarla solo nel ciclo. Tuttavia, a causa del **function scope** di `var`, la variabile appartiene allo scope che la contiene (funzione o globale), non al ciclo.

### Falso Block Scope nel Blocco if

```javascript
function foo(bar) {
  if (bar) {
    var baz = bar * 2;
    console.log(baz);
  }

  // ⚠️ 'baz' è accessibile qui!
  console.log(baz);
}
```

Questo è **falso block scope**: `baz` è dichiarata nel blocco `if`, ma con `var` la sua validità si estende a tutto lo scope della funzione. Questo si basa sull'autodisciplina dello sviluppatore per non riutilizzare `baz` altrove. Senza block scope, gli sviluppatori possono riutilizzare accidentalmente le variabili, causando bug difficili da tracciare.

## 🔐 try...catch: Il Primo Block Scope (ES3)

È un fatto poco noto che JavaScript, già a partire dalla specifica ES3, ha introdotto una forma di block scope per la variabile dichiarata nella clausola `catch` di un blocco `try...catch`.

```javascript
try {
  undefined(); // Genera un errore
} catch (err) {
  console.log(err); // TypeError
  // 'err' esiste SOLO in questo blocco
}

console.log(err); // ❌ ReferenceError
```

La variabile `err` esiste solo ed esclusivamente all'interno del blocco `catch`.
Alcuni linter segnalano errore in presenza di più blocchi `try...catch` con lo stesso nome di variabile `err`, ma tecnicamente sono in scope separati ed è un'operazione sicura.
