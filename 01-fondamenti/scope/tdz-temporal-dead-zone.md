# [[../../appunti-completi#blocchi-come-scope-blocks-as-scopes|Temporal Dead Zone (TDZ)]]

## ⚠️ Differenza da var (Hoisting)

A differenza di `var`, le variabili `let` e `const` **non sono accessibili prima della dichiarazione**. A causa dell'hoisting, l'accesso a `var` prima della riga che la dichiara produce un risultato passabile ma ambiguo, mentre su variabili con block scope si ottiene un errore formale.

```javascript
console.log(a); // undefined (hoisting di var)
var a = 10;

console.log(b); // ❌ ReferenceError: Cannot access 'b' before initialization
let b = 20;

console.log(c); // ❌ ReferenceError: Cannot access 'c' before initialization
const c = 30;
```

## ⏳ Cos'è la TDZ

La **Temporal Dead Zone** è il periodo (nel flusso di esecuzione e all'interno del proprio blocco) tra l'inizio del blocco e la dichiarazione vera e propria della variabile. Un blocco `{ ... }` inizia con il suo contesto locale e l'interprete javascript impedisce di accedere alle variabili ivi dichiarate tramite let/const fino a quando l'istruzione in questione non è valutata.

```javascript
{
  // TDZ inizia qui per 'x'

  console.log(x); // ❌ ReferenceError (in TDZ)

  let x = 10; // TDZ finisce qui

  console.log(x); // ✅ 10
}
```

La valutazione del codice "in esecuzione" blocca l'accesso e l'output è sempre `ReferenceError`, sebbene l'interprete in base allo spec lessicale sappia già dell'esistenza della variabile.

## 🚷 TDZ e typeof

La TDZ ha conseguenze sull'utilizzo dell'operatore condizionale `typeof`. Generalmente, `typeof` applicato ad una variabile assente produce la stringa `"undefined"` ed è definito come sicura ("safe"), cioè omettendo la violazione di reference.

Tuttavia, all'interno della Temporal Dead Zone di let e const, il `typeof` non protegge dall'eccezione: 

```javascript
// Con variabile non dichiarata
console.log(typeof variabileNonEsiste); // "undefined" (safe)

// Con let in TDZ
console.log(typeof x); // ❌ ReferenceError (in TDZ!)
let x = 10;
```

## 🔒 Perché Esiste la TDZ

La TDZ esiste per proteggere dal comportamento di fallimento subdolo (`NaN`, `undefined` nascosto e valori parziali) e favorisce una strutturazione corretta.

La TDZ **previene errori** obbligando a dichiarare la variabile prima del suo utilizzo, un atteggiamento di autoprotezione della sintassi del JavaScript.
