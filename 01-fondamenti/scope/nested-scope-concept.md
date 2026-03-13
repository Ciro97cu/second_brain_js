# [[../../appunti-completi#scope-annidato-nested-scope|Concetto di Scope Annidato]]

Gli scope annidati creano una **catena di ricerca** (scope chain) dove l'Engine risale livello per livello finché trova la variabile o raggiunge lo scope globale.

## Il Processo di Ricerca

Lo scope non è mai isolato: funzioni e blocchi creano scope **annidati** l'uno dentro l'altro. La **scope chain** è il meccanismo che permette al codice di cercare variabili risalendo attraverso scope annidati. La ricerca delle variabili segue una direzione precisa: **dal locale verso il globale**.

Quando l'Engine cerca una variabile:
1. **Parte dallo scope corrente**
2. **Non trova?** Sale allo scope esterno
3. **Continua a risalire** finché trova la variabile
4. **Scope globale è il limite**: se non trova lì, genera `ReferenceError`

```javascript
// Esempio di ricerca multi-livello
let a = 10; // Globale

function foo() {
  // 'b' non è qui, ma l'Engine lo trova nel globale
  console.log(a + b); // Cerca 'a' → ✅ trovato | Cerca 'b' → ✅ trovato
}

let b = 20; // Globale
foo(); // Output: 30
```

## La Conversazione Engine-Scope

Per comprendere il meccanismo, si immagini la **conversazione** tra Engine e i vari Scope in un ambiente isolato:

```javascript
let nome = "Mario"; // Dichiarato nello scope globale

function saluta() {
  // Engine cerca 'nome':
  // Engine: "Scope di saluta, hai 'nome'?"
  // Scope: "No, prova più in alto"
  // Engine: "Scope globale, hai 'nome'?"
  // Scope globale: "Sì! Ecco: 'Mario'"

  let messaggio = "Ciao";

  function completaSaluto() {
    // Engine cerca 'messaggio':
    // 1. Scope di completaSaluto → ❌ Non trovato
    // 2. Scope di saluta → ✅ Trovato!

    // Engine cerca 'nome':
    // 1. Scope di completaSaluto → ❌
    // 2. Scope di saluta → ❌
    // 3. Scope globale → ✅ Trovato!

    console.log(messaggio + ", " + nome); // "Ciao, Mario"
  }

  completaSaluto();
}

saluta();
```
