# [[../../appunti-completi#variazioni-del-pattern-iife|IIFE: Concetto Generale]]

## 🎯 Concetto

Le **IIFE** (Immediately Invoked Function Expressions) sono funzioni che si eseguono immediatamente dopo essere state definite. Esistono diverse variazioni sintattiche e pattern di utilizzo, tutte basate sullo stesso principio: creare uno scope privato ed eseguirlo subito.

**Pattern Base**: `(function() { /* codice */ })();`

## 💻 Forma Anonima vs Nominata

### Anonima (Comune)

```javascript
// IIFE anonima
(function () {
  var messaggio = "IIFE anonima";
  console.log(messaggio);
})();

// Stack trace: <anonymous>
```

### Nominata (Best Practice)

```javascript
// IIFE nominata
(function IIFE() {
  var messaggio = "IIFE nominata";
  console.log(messaggio);
})();

// Stack trace: IIFE ← Utile per debugging!
```

Il vantaggio principale dell'uso di una funzione nominata è che il nome risulta visibile negli stack trace facilitando il debugging, senza inquinare lo scope esterno con la dichiarazione della funzione. Questo pattern rappresenta una best practice rispetto all'uso di funzioni anonime.

## 📉 Pattern in Declino

Con l'avvento degli **ES6 modules** e l'utilizzo di **bundler moderni** (come Webpack o Vite), le IIFE sono diventate meno necessarie in quanto i moduli offrono uno scope privato nativo.
Tuttavia, il pattern risulta ancora utile e rilevante per l'esecuzione di script standalone e per garantire la compatibilità con sistemi legacy.

## 📌 Tag

#javascript #iife #concept #scope #encapsulation
