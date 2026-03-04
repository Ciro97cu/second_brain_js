# [[../../appunti-completi#funzioni-come-scope|Funzioni come Scope]]

## 🎯 Concetto

Avvolgere codice in una funzione lo "nasconde" creando uno scope privato. Tuttavia, **dichiarare** una funzione inquina lo scope esterno. Le **espressioni di funzione** (function expressions) risolvono questo problema: il nome della funzione non è registrato nello scope esterno, ma rimane accessibile solo internamente.

**Pattern Chiave**: `(function foo() { /* ... */ })()` - Nome privato, esecuzione immediata (IIFE).

## 💻 Dichiarazione vs Espressione

### Dichiarazione (Inquina Scope)

```javascript
// ❌ 'foo' diventa globale
function foo() {
  var a = 3;
  console.log(a);
}

foo(); // Chiamata esplicita
console.log(typeof foo); // "function" ← INQUINAMENTO
```

### Espressione (Scope Pulito)

```javascript
// ✅ 'foo' NON è globale
(function foo() {
  var a = 3;
  console.log(a); // 3
})(); // Esecuzione immediata

// console.log(typeof foo); // ReferenceError ← NESSUN INQUINAMENTO
```

## 🔑 Regola Chiave

**Se `function` è la PRIMA parola** → Dichiarazione (nome nello scope esterno)  
**Altrimenti** (es. tra parentesi) → Espressione (nome privato)

```javascript
// DICHIARAZIONE
function bar() {
  /* ... */
}

// ESPRESSIONI
(function baz() {
  /* ... */
});
var fn = function qux() {
  /* ... */
};
```

## 💡 Nome della Funzione: Dove Va?

### Dichiarazione

```javascript
function nomeDichiarazione() {
  /* ... */
}
console.log(nomeDichiarazione.name); // Accessibile fuori
```

### Espressione

```javascript
var varEsterna = function nomeEspressione() {
  // 'nomeEspressione' accessibile SOLO qui
  console.log(nomeEspressione.name);
};

console.log(varEsterna.name); // "nomeEspressione" (proprietà)
// console.log(nomeEspressione); // ReferenceError (NON nello scope!)
```

## 🔄 Ricorsione con Nome Privato

```javascript
var fattoriale = function fatto(n) {
  if (n <= 1) return 1;
  return n * fatto(n - 1); // Usa 'fatto' internamente
};

fattoriale(5); // 120
// fatto(5); // ReferenceError

// Anche se riassegno, la ricorsione funziona
var temp = fattoriale;
fattoriale = null;
temp(5); // 120 - usa 'fatto' interno!
```

## 🎯 Pattern IIFE (Immediately Invoked Function Expression)

```javascript
var a = 2;

(function IIFE() {
  var a = 3;
  var b = 4;

  function helper() {
    return a + b;
  }

  console.log(helper()); // 7
})(); // Parentesi finali = esecuzione immediata

console.log(a); // 2 (NON inquinato)
// console.log(b); // ReferenceError (privato)
// console.log(IIFE); // ReferenceError (nome privato)
```

## 💼 Caso d'Uso Reale

### Inizializzazione Complessa

```javascript
var config = (function () {
  // Variabili PRIVATE
  var env = "production";
  var apiKeys = { dev: "dev123", prod: "prod456" };

  function getKey() {
    return apiKeys[env];
  }

  // Ritorna solo configurazione finale
  return {
    apiUrl: "https://api.com/api",
    apiKey: getKey(),
    timeout: 5000,
  };
})();

// Solo 'config' è esposto
config.apiUrl; // Accessibile
// env; // ReferenceError (privato)
```

## ⚖️ Confronto: Dichiarazione vs Espressione

| Aspetto                      | Dichiarazione | Espressione |
| ---------------------------- | ------------- | ----------- |
| Nome nello scope esterno     | ✅ Sì         | ❌ No       |
| Esecuzione automatica        | ❌ No         | ✅ Con IIFE |
| Inquinamento scope           | ⚠️ Sì         | ✅ No       |
| Ricorsione interna           | ✅ Sì         | ✅ Sì       |
| Debugging (nome nello stack) | ✅ Sì         | ✅ Sì       |

## ⚠️ Problemi Risolti

1. **Inquinamento Scope**: Nome funzione non accessibile esternamente
2. **Chiamata Esplicita**: Con IIFE, esecuzione automatica
3. **Privacy**: Dettagli implementativi nascosti
4. **Collisioni**: Nome non registrato nello scope esterno

## ✅ Vantaggi

- **Zero Inquinamento**: Nessun nome nello scope esterno
- **Esecuzione Immediata**: Pattern IIFE
- **Privacy Reale**: Variabili e helper veramente privati
- **Ricorsione Sicura**: Nome interno per chiamate ricorsive
- **Debugging**: Nome visibile nello stack trace

## 🔗 Concetti Correlati

- [[hiding-in-scope|Hiding in Scope]] - Principio generale
- [[lexical-scope-base|Scope Lessicale]] - Meccanismo sottostante
- [[scope-namespaces|Namespace Globali]] - Pattern alternativo
- [[module-management|Module Management]] - Evoluzione moderna
- [[../../appunti-completi#funzioni-come-scope|Funzioni come Scope Completo]]

## 📚 Risorse

- "You Don't Know JS" - Scope & Closures, Chapter 3
- MDN: Function Expressions
- IIFE Pattern (Immediately Invoked Function Expression)

## 📌 Tag

#javascript #scope #function-expressions #iife #declarations #encapsulation #privacy #patterns
