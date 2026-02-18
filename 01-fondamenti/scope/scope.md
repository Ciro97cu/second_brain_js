# [[../../appunti-completi#44-scope-ambito|Scope (Ambito)]]

Lo **scope** (ambito lessicale) definisce il **contesto in cui una variabile è visibile** e accessibile.

## Concetto Fondamentale

Le variabili "vivono" in specifici ambiti. Il programma accede solo a variabili nel **proprio scope** o **scope esterno**.

```javascript
function negozioA() {
  let prodottoA = "Laptop";
  console.log(prodottoA); // ✅ Accessibile
}

function negozioB() {
  let prodottoB = "Mouse";
  // console.log(prodottoA);  // ❌ Non accessibile (scope diverso)
}
```

**Metafora**: Come un negozio vende solo prodotti del proprio magazzino, il codice accede solo a variabili del proprio scope.

## I Tre Attori (Metafora)

**Engine**: Responsabile compilazione ed esecuzione (il "capo").

**Compiler**: Analizza codice e genera eseguibile.

**Scope**: Mantiene lista variabili e regole di accessibilità (il "guardiano").

```javascript
let nome = "Mario"; // Compiler registra 'nome' nello Scope
console.log(nome); // Engine chiede a Scope il valore di 'nome'
```

## Scope Globale vs Locale

**Scope Globale**: variabili fuori da funzioni, accessibili ovunque.

**Scope Locale**: variabili dentro funzioni, accessibili solo lì.

```javascript
// Scope Globale
let globale = "Ovunque";

function fn() {
  // Scope Locale
  let locale = "Solo qui";

  console.log(globale); // ✅ Accede esterno
  console.log(locale); // ✅ Accede proprio
}

fn();
// console.log(locale);  // ❌ ReferenceError
```

**Regola**: Interno accede esterno, esterno NON accede interno.

## Block Scope (let/const vs var)

Mentre `var` crea uno **scope a livello di funzione**, le parole chiave moderne `let` e `const` introducono il concetto di **Block Scope**. Una variabile dichiarata con `let` o `const` è **confinata al blocco di codice `{...}`** in cui è definita (ad esempio un `if`, un ciclo `for` o anche un blocco autonomo).

```javascript
if (true) {
  let blocco = "Block scoped";
  const COSTANTE = 42;
  var funzione = "Function scoped";
}

// console.log(blocco);    // ❌ Errore (let)
// console.log(COSTANTE);  // ❌ Errore (const)
console.log(funzione); // ✅ var ignora blocchi
```

**`let` e `const`**: Rispettano **block scope** (blocchi `{}`).

**`var`**: Rispetta solo **function scope**, ignora i blocchi.

```javascript
function esempio() {
  if (true) {
    let x = 10;
    var y = 20;
  }

  // console.log(x);  // ❌ ReferenceError (fuori block scope)
  console.log(y); // ✅ 20 (var ignora blocchi, scope di funzione)
}

// Blocco autonomo
{
  let messaggio = "Solo qui";
  const PI = 3.14;
  console.log(messaggio); // ✅ Accessibile
}
// console.log(messaggio);  // ❌ ReferenceError
```

Block scope permette un **controllo più preciso** sulla visibilità delle variabili.

## Collegamenti

- [[../variabili/variabili]] - Dichiarazione e ambito variabili
- [[scope-chain]] - Scope annidati e catena degli scope
- [[../funzioni/funzioni]] - Le funzioni creano scope locale
- [[../sintassi/blocchi]] - Blocchi e block scope
- [[../variabili/hoisting]] - Hoisting e scope
