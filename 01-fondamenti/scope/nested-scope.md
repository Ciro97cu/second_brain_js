# [[../../appunti-completi#scope-annidato-nested-scope|Scope Annidato (Nested Scope)]]

Gli scope annidati creano una **catena di ricerca** (scope chain) dove l'Engine risale livello per livello finché trova la variabile o raggiunge lo scope globale.

## 🎯 Concetto Chiave

Lo scope non è mai isolato: funzioni e blocchi creano scope **annidati** l'uno dentro l'altro. La ricerca delle variabili segue una direzione precisa: **dal locale verso il globale**.

### Il Processo di Ricerca

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

## 💻 La Conversazione Engine-Scope

Per comprendere il meccanismo, immaginiamo la **conversazione** tra Engine e i vari Scope:

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

## 🏢 La Metafora dell'Edificio

La scope chain può essere visualizzata come un **edificio a più piani**:

- **Piano terra** = Scope corrente (dove si esegue il codice)
- **Piani superiori** = Scope esterni
- **Attico** = Scope globale (ultimo piano)

L'Engine prende l'**ascensore** e sale piano per piano cercando la variabile.

```javascript
// EDIFICIO CON 4 PIANI
let piano4 = "Attico - Globale"; // Piano 4 (Top)

function entraNelPalazzo() { 
  let piano3 = "Terzo piano"; // Piano 3

  function scendiAlSecondo() {
    let piano2 = "Secondo piano"; // Piano 2

    function scendiAlPrimo() {
      let piano1 = "Piano terra"; // Piano 1 (Ground)

      // Dal piano terra, l'Engine può salire fino all'attico
      console.log(piano1); // ✅ Piano corrente (non serve l'ascensore)
      console.log(piano2); // ✅ Sale di 1 piano
      console.log(piano3); // ✅ Sale di 2 piani
      console.log(piano4); // ✅ Sale di 3 piani (attico)
    }

    scendiAlPrimo();

    // Dal secondo piano NON posso scendere al piano terra
    // console.log(piano1); // ❌ L'ascensore va solo verso l'alto!
  }

  scendiAlSecondo();
}

entraNelPalazzo();
```

**Regola chiave**: L'ascensore va **solo verso l'alto** (verso scope esterni), mai verso il basso.

## ⚠️ Errori Comuni

### ❌ Confondere direzione della ricerca

```javascript
function esterna() {
  let x = 10;

  function interna() {
    console.log(x); // ✅ OK, risale a esterna
  }

  interna();
}

console.log(x); // ❌ ReferenceError: non può scendere negli scope interni
```

### ❌ Aspettarsi accesso a variabili "fratello"

```javascript
function A() {
  let x = 10;
}

function B() {
  console.log(x); // ❌ ReferenceError: A e B sono "fratelli", non annidati
}
```

## ✅ Best Practices

**Comprendere la direzione**: La ricerca va sempre **dal locale al globale**, mai il contrario.

**Minimizzare livelli**: Troppi livelli di annidamento rendono difficile tracciare la scope chain.

**Naming esplicito**: Usa nomi significativi per evitare confusione negli scope annidati.

```javascript
// ❌ Troppi livelli annidati (difficile da seguire)
function a() {
  function b() {
    function c() {
      function d() {
        // Quale scope ha quale variabile?
      }
    }
  }
}

// ✅ Struttura più piatta e chiara
function elaboraDati(input) {
  const config = caricaConfig();
  return trasformaDati(input, config);
}

function trasformaDati(dati, config) {
  // Logica separata, scope chiaro
}
```

## 🔗 Collegamenti

- [[scope-chain]] - Meccanismo tecnico della scope chain
- [[scope]] - Concetti base dello scope
- [[../variabili/hoisting]] - Hoisting e scope
- [[../funzioni/closures]] - Closures sfruttano la scope chain

## 📚 Risorse Esterne

- [MDN: Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) - Scope chain nelle closures
- [YDKJS: Scope & Closures](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/README.md) - Approfondimento su scope

## 📌 Note Aggiuntive

- La scope chain è **determinata lessicalmente** (dove il codice è scritto), non dinamicamente (dove viene eseguito)
- Ogni funzione "ricorda" il suo scope esterno anche quando viene eseguita altrove (**closure**)
- Gli scope annidati sono la base per pattern avanzati come **module pattern** e **IIFE**
