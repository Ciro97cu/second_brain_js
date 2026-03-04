# [[../../appunti-completi#funzioni-anonime-vs-funzioni-nominate|Funzioni Anonime vs Nominate]]

## 🎯 Concetto

Le **espressioni di funzione** possono essere **anonime** (senza nome) o **nominate** (con nome). Mentre le funzioni anonime sono comuni e veloci da scrivere, presentano svantaggi significativi. La **best practice** è nominare sempre le espressioni di funzione.

**Regola**: Le dichiarazioni di funzione DEVONO avere un nome; le espressioni possono essere anonime, ma DOVREBBERO avere un nome.

## 💻 Anonime vs Nominate

### Funzione Anonima (Comune ma Non Ottimale)

```javascript
// Callback anonimo
setTimeout(function () {
  console.log("Timeout");
}, 1000);

// Event listener anonimo
button.addEventListener("click", function () {
  console.log("Click");
});
```

### Funzione Nominata (Best Practice)

```javascript
// Callback nominato
setTimeout(function timeoutHandler() {
  console.log("Timeout");
}, 1000);

// Event listener nominato
button.addEventListener("click", function handleClick() {
  console.log("Click");
});
```

## ⚠️ Svantaggi delle Funzioni Anonime

### 1. Debugging Difficile

Stack trace mostra `<anonymous>` invece di un nome utile:

```javascript
// ❌ Anonima
setTimeout(function () {
  throw new Error("Errore!");
}, 100);
// Stack trace: at <anonymous>:2:9 ← Non utile!

// ✅ Nominata
setTimeout(function timeoutHandler() {
  throw new Error("Errore!");
}, 100);
// Stack trace: at timeoutHandler:2:9 ← Chiaro!
```

### 2. Auto-riferimento Impossibile

Ricorsione o rimozione di event handler richiedono il nome:

```javascript
// ❌ Anonima ricorsiva (fragile)
var fattoriale = function (n) {
  if (n <= 1) return 1;
  return n * fattoriale(n - 1); // Dipende dalla variabile esterna
};

var temp = fattoriale;
fattoriale = null;
// temp(5); // TypeError: fattoriale is not a function

// ✅ Nominata ricorsiva (robusta)
var fattorialeRobusto = function fatto(n) {
  if (n <= 1) return 1;
  return n * fatto(n - 1); // Usa nome interno
};

var temp2 = fattorialeRobusto;
fattorialeRobusto = null;
temp2(5); // 120 - Funziona!
```

### 3. Scarsa Leggibilità

Nome descrittivo auto-documenta il codice:

```javascript
// ❌ Anonime (cosa fanno?)
getData(function (data) {
  processData(data, function (result) {
    saveResult(result, function (response) {
      console.log("Fatto");
    });
  });
});

// ✅ Nominate (intento chiaro)
getData(function onDataReceived(data) {
  processData(data, function onDataProcessed(result) {
    saveResult(result, function onResultSaved(response) {
      console.log("Fatto");
    });
  });
});
```

## ✅ Vantaggi delle Funzioni Nominate

1. **Stack Trace Chiaro**: Nome visibile negli errori
2. **Auto-riferimento**: Ricorsione e rimozione event handler sicuri
3. **Leggibilità**: Nome descrive lo scopo
4. **Zero Inquinamento**: Nome non nello scope esterno
5. **Debugging**: Nome nei DevTools

## 🎯 Best Practice

**Nomina SEMPRE le espressioni di funzione**:

```javascript
// ✅ Callbacks
array.map(function raddoppia(n) {
  return n * 2;
});

// ✅ Event handlers
button.addEventListener("click", function handleClick(e) {
  /* ... */
});

// ✅ Timers
setTimeout(function cleanup() {
  /* ... */
}, 1000);

// ✅ IIFE
(function inizializzaApp() {
  // ...
})();
```

## 🔑 Regole di Sintassi

```javascript
// ❌ INVALIDO: Dichiarazione senza nome
// function() { /* ... */ } // SyntaxError

// ✅ VALIDO: Dichiarazione con nome
function nomeDichiarazione() {
  /* ... */
}

// ✅ VALIDO: Espressione anonima (ma sconsigliato)
var fn1 = function () {
  /* ... */
};

// ✅ VALIDO: Espressione nominata (CONSIGLIATO)
var fn2 = function nomeEspressione() {
  /* ... */
};
```

## 📊 arguments.callee (Deprecato)

```javascript
// ❌ NON USARE arguments.callee (deprecato)
var fattoriale = function (n) {
  if (n <= 1) return 1;
  return n * arguments.callee(n - 1); // DEPRECATO!
};

// ✅ USA nome interno
var fattoriale = function fatto(n) {
  if (n <= 1) return 1;
  return n * fatto(n - 1);
};
```

## 🔗 Concetti Correlati

- [[function-as-scope|Funzioni come Scope]] - Dichiarazioni vs espressioni
- [[iife-patterns|Pattern IIFE]] - IIFE nominate vs anonime
- [[hiding-in-scope|Hiding in Scope]] - Principio generale
- [[../../appunti-completi#funzioni-anonime-vs-funzioni-nominate|Funzioni Anonime Completo]]

## 📚 Risorse

- "You Don't Know JS" - Scope & Closures
- MDN: Function Expressions
- JavaScript: The Good Parts (Douglas Crockford)

## 📌 Tag

#javascript #functions #anonymous #named-functions #best-practices #debugging #stack-trace #recursion #readability
