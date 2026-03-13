# [[../../appunti-completi#blocchi-come-scope-blocks-as-scopes|const: Block Scope Immutabile]]

## 🔒 Immutabilità della Dichiarazione

`const` funziona come `let` e crea un binding all'interno di un blocco `{ ... }`, ma differisce per un aspetto fondamentale: **il valore non può essere riassegnato**.

```javascript
const PI = 3.14159;
console.log(PI); // 3.14159

PI = 3.14; // ❌ TypeError: Assignment to constant variable

if (true) {
  const MESSAGE = "Hello";
  console.log(MESSAGE); // "Hello"
}
// console.log(MESSAGE); // ❌ ReferenceError
```

La parola chiave `const` deve essere inizializzata al momento della dichiarazione. La sua ridichiarazione non è permessa e genera un `SyntaxError` se si trova nello stesso scope, al pari di `let`.

```javascript
const z = 10;
const z = 20; // ❌ SyntaxError: Identifier 'z' has already been declared
```

## 🔄 `const` Riassegnazione vs Mutazione

L'identificatore dichiarato tramite `const` impedisce la **riassegnazione**, ma **NON** rende il valore immutabile, nel caso di strutture complesse come oggetti e array.
Se il valore puntato dalla costante è mutabile, il codice può alterare le sue proprietà.

```javascript
const obj = { nome: "Mario" };

// ✅ Modifica delle proprietà consentita
obj.nome = "Luigi";
obj.eta = 30;
console.log(obj); // { nome: "Luigi", eta: 30 }

// ❌ Riassegnazione della referenza BLOCCATA
obj = { nome: "Peach" }; // TypeError: Assignment to constant variable
```

La medesima regola vale per gli Array:

```javascript
const arr = [1, 2, 3];
arr.push(4); // ✅ OK
arr[0] = 10; // ✅ OK
console.log(arr); // [10, 2, 3, 4]

// ❌ Riassegnazione della referenza BLOCCATA
arr = [5, 6]; // TypeError: Assignment to constant variable
```

Il fatto di proteggere contro la riassegnazione migliora la leggibilità: dichiarare una variabile con `const` trasmette l'intenzione che non deve cambiare in seguito nell'esecuzione del file.
