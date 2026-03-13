# [[../../appunti-completi#funzioni-come-scope|Funzione come Scope: Concetto Generale]]

## 🎯 Concetto

Avvolgere il codice all'interno di una funzione permette di "nasconderlo", creando così uno scope privato. Tuttavia, la **dichiarazione** convenzionale della funzione inquina lo scope esterno. Le **espressioni di funzione** (function expressions) risolvono questo problema: il nome della funzione non viene registrato nello scope globale o esterno, ma rimane accessibile solo all'interno della funzione stessa.

**Pattern Chiave**: `(function foo() { /* ... */ })()` - Nome privato ed esecuzione immediata (IIFE).

## 💻 Dichiarazione vs Espressione

### Dichiarazione (Inquina lo Scope)

```javascript
// ❌ 'foo' diventa globale
function foo() {
  var a = 3;
  console.log(a);
}

foo(); // Chiamata esplicita necessaria
console.log(typeof foo); // "function" ← INQUINAMENTO DELLO SCOPE
```

### Espressione (Scope Pulito)

```javascript
// ✅ 'foo' NON diventa globale
(function foo() {
  var a = 3;
  console.log(a); // 3
})(); // Esecuzione immediata (IIFE)

// console.log(typeof foo); // ReferenceError ← NESSUN INQUINAMENTO
```

## 🔑 Regola Chiave

La distinzione sintattica tra dichiarazione ed espressione si basa sulla posizione della parola chiave `function`:

- **Se `function` è la PRIMA parola nell'istruzione** → Si tratta di una Dichiarazione (il nome viene inserito nello scope esterno).
- **Altrimenti** (ad esempio, inserita tra parentesi o passata come argomento) → Si tratta di un'Espressione (il nome rimane privato e accessibile solo internamente).

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

## 🔗 Riferimenti e Correlazioni

- [[hiding-in-scope|Hiding in Scope]] - Principio generale
- [[lexical-scope-base|Scope Lessicale]] - Meccanismo sottostante
- [[function-scope-naming-recursion|Nomi e Ricorsione in Scopes Privati]]
- [[function-scope-iife-patterns|Pattern IIFE e Incapsulamento]]

## 📌 Tag

#javascript #scope #function-expressions #declarations #encapsulation
