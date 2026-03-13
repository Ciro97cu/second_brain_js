# [[../../appunti-completi#blocchi-come-scope-blocks-as-scopes|let: Block Scope Moderno]]

## ✨ Attaccare Variabili ai Blocchi

ES6 ha introdotto la parola chiave `let` come alternativa a `var`. `let` **"attacca" la dichiarazione di una variabile allo scope di qualsiasi blocco** in cui è contenuta.

```javascript
var foo = true;

if (foo) {
  let bar = foo * 2;
  console.log(bar); // 2
}

console.log(bar); // ❌ ReferenceError: bar is not defined
// 'bar' esiste SOLO dentro il blocco if
```

La variabile `bar`, dichiarata con `let`, esiste solo all'interno del blocco `if`. Qualsiasi tentativo di accedervi dall'esterno risulta in un `ReferenceError`.

## 📦 Block Scope in Qualsiasi Blocco { ... }

La direttiva `let` si applica a qualsiasi tipo di blocco `{ ... }`:

```javascript
// Blocco in un if
if (true) {
  let x = 10;
  console.log(x); // 10
}
// console.log(x); // ❌ ReferenceError

// Blocco in un while
let count = 0;
while (count < 3) {
  let messaggio = `Iterazione ${count}`;
  console.log(messaggio);
  count++;
}
// console.log(messaggio); // ❌ ReferenceError

// Blocco arbitrario (standalone)
{
  let privato = "segreto";
  console.log(privato); // "segreto"
}
// console.log(privato); // ❌ ReferenceError
```

## 🚫 Ridichiarazione Vietata

A differenza di `var`, la ridichiarazione di una variabile con `let` nello stesso scope non è permessa e genera un `SyntaxError`.

```javascript
let y = 10;
let y = 20; // ❌ SyntaxError: Identifier 'y' has already been declared
```

Tuttavia, all'interno di scope **diversi**, `let` supporta lo shadowing (l'occultamento della variabile dello scope superiore):

```javascript
let x = 10;

{
  let x = 20; // ✅ OK, scope diverso (shadowing)
  console.log(x); // 20
}

console.log(x); // 10
```

Non è permesso mescolare `var` e `let` con lo stesso nome nel medesimo scope.
