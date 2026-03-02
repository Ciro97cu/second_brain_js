# [[../../appunti-completi#scope-annidato-nested-scope|Scope Annidato e Scope Chain]]

Gli scope annidati creano una **catena di ricerca** (scope chain) dove l'Engine risale livello per livello finché trova la variabile o raggiunge lo scope globale.

## 🎯 Concetto Chiave

Lo scope non è mai isolato: funzioni e blocchi creano scope **annidati** l'uno dentro l'altro. La **scope chain** è il meccanismo che permette al codice di cercare variabili risalendo attraverso scope annidati. La ricerca delle variabili segue una direzione precisa: **dal locale verso il globale**.

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

## 🎭 Shadowing (Variabili Ombra)

Lo **shadowing** si verifica quando una variabile dichiarata in uno **scope locale** ha lo stesso nome di una variabile in uno **scope più esterno**. In questo caso, la variabile locale **"nasconde"** o **"mette in ombra"** (shadows) quella esterna.

### Shadowing Base

```javascript
let x = 10; // Scope globale

function esempio() {
  let x = 20; // Scope locale, "shadows" la x globale
  console.log(x); // 20 (usa la x locale)
}

esempio();
console.log(x); // 10 (usa la x globale, non modificata)
```

### Shadowing Annidato Multi-Livello

```javascript
let nome = "Globale";

function esterna() {
  let nome = "Esterna"; // Shadows globale
  console.log(nome); // "Esterna"

  function interna() {
    let nome = "Interna"; // Shadows esterna (e globale)
    console.log(nome); // "Interna"
  }

  interna();
  console.log(nome); // "Esterna" (non modificata)
}

esterna();
console.log(nome); // "Globale" (non modificata)
```

### Shadowing con Blocchi

Anche i blocchi `{}` con `let`/`const` creano shadowing:

```javascript
let x = 100;

if (true) {
  let x = 200; // Shadows x esterna
  console.log(x); // 200
}

console.log(x); // 100

for (let x = 0; x < 3; x++) {
  console.log(x); // 0, 1, 2 (shadows x esterna)
}

console.log(x); // 100 (non modificata)
```

**Nota Importante**: Non puoi ri-dichiarare la stessa variabile con `let`/`const` nello stesso scope, ma puoi farlo in scope diversi (shadowing).

```javascript
let y = 10;
// let y = 20;  // ❌ SyntaxError: già dichiarata

{
  let y = 20; // ✅ OK, diverso scope (shadowing)
  console.log(y); // 20
}

console.log(y); // 10
```

## ⚡ ReferenceError nella Scope Chain

**ReferenceError** si verifica quando si tenta di accedere a una variabile non disponibile nello scope corrente né in alcuno scope esterno:

```javascript
function test() {
  // console.log(inesistente);  // ❌ ReferenceError: inesistente is not defined
}

if (true) {
  let x = 10;
}
// console.log(x);  // ❌ ReferenceError: x is not defined (fuori block scope)
```

## ⚠️ Pericolo: Variabili Globali Accidentali

Un comportamento **pericoloso** di JavaScript (in modalità non-stretta) si verifica quando si assegna un valore a una variabile **non dichiarata** con `var`, `let` o `const`.

```javascript
function esempio() {
  x = 10; // ❌ Nessuna dichiarazione (var/let/const)
  // JavaScript risale la scope chain fino in cima
  // Non trova 'x' dichiarata da nessuna parte
  // Crea AUTOMATICAMENTE 'x' nello scope globale
}

esempio();
console.log(x); // 10 (variabile globale accidentale!)
console.log(window.x); // 10 (nel browser)
```

### Perché è Pericoloso

Questa è una **pessima pratica** perché:

1. **Inquinamento scope globale**: Variabili globali involontarie
2. **Bug difficili da tracciare**: Parti diverse del codice modificano la stessa variabile
3. **Conflitti di nomi**: Sovrascrittura accidentale di variabili esistenti

```javascript
let x = 100; // Variabile globale intenzionale

function funzioneA() {
  x = 200; // ✅ OK, modifica x globale (intenzionale, già dichiarata)
}

function funzioneB() {
  y = 50; // ❌ Crea y globale (accidentale!)
}

funzioneA();
console.log(x); // 200

funzioneB();
console.log(y); // 50 (variabile globale accidentale)
```

### Soluzione: Strict Mode

**Regola fondamentale**: Dichiara **sempre** formalmente le variabili con `let`, `const` o `var`.

Lo **strict mode** (`"use strict"`) previene questo problema trasformando assegnamenti non dichiarati in **errori**:

```javascript
"use strict";

function test() {
  x = 10; // ❌ ReferenceError: x is not defined
  // Strict mode impedisce la creazione automatica
}

// ✅ Soluzione corretta
function testCorretto() {
  let x = 10; // Dichiarazione esplicita
  console.log(x);
}
```

## 🔗 Collegamenti

- [[scope]] - Concetti base dello scope
- [[lexical-scope-base|Scope Lessicale]] - Scope determinato author-time
- [[scope-lookup|Scope Lookup]] - Dettagli sul processo di ricerca
- [[scope-bubbles|Bolle di Scope]] - Visualizzazione scope annidati
- [[scope-errors|Errori di Scope]] - ReferenceError e TypeError
- [[../../appunti-completi#scope-annidato-nested-scope|Scope Annidato Completo]]

## 📚 Risorse

- MDN: Closures - Scope chain nelle closures
- "You Don't Know JS" - Scope & Closures

## 📌 Tag

#javascript #scope #scope-chain #nested-scope #shadowing #global-leak #reference-error #strict-mode
