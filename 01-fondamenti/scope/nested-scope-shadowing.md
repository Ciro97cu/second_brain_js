# [[../../appunti-completi#scope-annidato-nested-scope|Shadowing (Variabili Ombra)]]

Lo **shadowing** si verifica quando una variabile dichiarata in uno **scope locale** viene definita con lo stesso nome di una variabile allocata in uno **scope più esterno**. In questo caso, l'Engine riconosce la variabile locale come primaria; essa **"nasconde"** o **"mette in ombra"** (shadows) quella di livello superiore.

## Shadowing Base e Effetti

```javascript
let x = 10; // Scope globale

function esempio() {
  let x = 20; // Scope locale, "shadows" la x globale
  console.log(x); // 20 (usa la x locale)
}

esempio();
console.log(x); // 10 (usa la x globale originaria che rimane intoccata)
```

## Shadowing Annidato Multi-Livello

Il fenomeno dello shadowing agisce bloccando anticipatamente la ricerca dell'Engine: non appena viene trovata una corrispondenza valida nello scope più vicino, la ricerca si ferma e termina istantaneamente, ignorando qualsiasi ulteriore variabile omonima allocata su livelli superiori della scope chain.

```javascript
let nome = "Globale";

function esterna() {
  let nome = "Esterna"; // Shadows globale
  console.log(nome); // "Esterna"

  function interna() {
    let nome = "Interna"; // Shadows esterna (e implicitamente la globale)
    console.log(nome); // "Interna"
  }

  interna();
  console.log(nome); // "Esterna" (non modificata dal blocco interno)
}

esterna();
console.log(nome); // "Globale" (non modificata dalle funzioni chiamate prima)
```

## Shadowing con Blocchi

Anche i semplici costrutti di blocco `{}` con l'ausilio di `let` e `const` creano ed estendono l'azione dello shadowing. 

```javascript
let x = 100;

if (true) {
  let x = 200; // Shadows della x esterna
  console.log(x); // 200
}

console.log(x); // 100
```

**Nota Importante sulle dichiarazioni**: Mentre non è accettato ri-dichiarare la stessa variabile con `let`/`const` rigorosamente nel medesimo scope, è prassi accettata e possibile farlo in scope diversi (attivando tecnicamente proprio il principio dello shadowing esposto in precedenza).

```javascript
let y = 10;
// let y = 20;  // ❌ SyntaxError: già regolarmente dichiarata

{
  let y = 20; // ✅ OK, ci si trova in un diverso scope
  console.log(y); // 20
}

console.log(y); // 10
```
