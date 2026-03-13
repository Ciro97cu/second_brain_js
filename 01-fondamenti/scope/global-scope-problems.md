# [[../../appunti-completi#variabili-globali-e-loggetto-window|Inquinamento dello Scope Globale e Shadowing Bypass]]

Quando si lavora con variabili globali in JavaScript, è facile incorrere in problemi legati a inquinamento dello scope (pollution) e bypass dello shadowing, in particolare se dichiarate con `var`.

## 💻 Bypass dello Shadowing

È possibile "bypassare" lo shadowing di variabili **globali** dichiarate con `var` accedendo alla proprietà di `window`.

```javascript
var varGlobale = "Sono globale";

function test() {
  var varGlobale = "Sono locale"; // Shadows

  console.log(varGlobale); // "Sono locale" (scope locale)
  console.log(window.varGlobale); // "Sono globale" (bypass shadowing)
}

test();
```

⚠️ **Limitazione**: Funziona **solo** per variabili globali con `var`, non per `let`/`const`.

### Non Funziona con let/const

```javascript
let globaleLet = "let globale";

function test() {
  let globaleLet = "let locale"; // Shadows

  console.log(globaleLet); // "let locale"
  console.log(window.globaleLet); // undefined (NON funziona)
  // Non c'è modo di accedere alla 'globaleLet' originale
}

test();
```

## ⚠️ Non Funziona per Variabili Non Globali

L'utilizzo di `window` fallisce se la variabile esterna non è nel contesto globale:

```javascript
function esterna() {
  var x = 10;

  function interna() {
    var x = 20; // Shadows

    console.log(x); // 20
    console.log(window.x); // undefined (x non è globale)
    // console.log(esterna.x); // ❌ Non esiste

    // La x di 'esterna' è INACCESSIBILE qui dentro
  }

  interna();
}

esterna();
```

## 🚫 Inquinamento dello Scope Globale

Dichiarare variabili nel globale con `var` causa l'inquinamento delle proprietà dell'oggetto `window` (o `global`).

```javascript
// ❌ var inquina window
var config = { api: "..." };
console.log(window.config); // { api: "..." }

function test() {
  // Potenziale conflitto con window.config
  console.log(config); // Ambiguo e non sicuro
}

// ✅ let/const NON inquinano window
let config2 = { api: "..." };
console.log(window.config2); // undefined (sicuro)
```

### Rischio di Conflitti con API Native

Le dichiarazioni con `var` sovrascrivono silentemente i metodi nativi di `window`.

```javascript
// ❌ PERICOLOSO: Sovrascrivere API native come alert
var alert = function () {
  console.log("Custom alert");
};

// Ora window.alert è sovrascritto permanentemente!
alert("test"); // Custom alert (non l'alert nativo)
```

## ✅ Best Practices

È raccomandato seguire queste pratiche:

1. **Utilizzare let/const invece di var**: Previene inquinamenti di `window` o accidentali sovrascritture.
2. **Non utilizzare window per bypassare shadowing**: Risulta confuso; conviene usare nomi variabili meno ambigui (es. `let globaleX` vs `let localeX`).
3. **Preferire moduli o namespace**: Minimizzare la dichiarazione di variabili globali (es. `const App = { ... };`).
4. **Adoperare globalThis per codice portatile** (ES2020+) qualora si necessiti davvero globalità universale trasversale ad ambienti JS.

## 📌 Note Aggiuntive

- Il bypass dello shadowing globale con `window` diviene inaccessibile quando si utilizzano blocchi rigorosi tramite `let` o `const`.
- Prevenire l'inquinamento di `window` abbassa drasticamente la possibilità di incroci accidentali tra procedure asincrone, moduli importati e API native del browser.
