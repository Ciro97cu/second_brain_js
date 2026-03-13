# [[../../appunti-completi#39-scope-closure-e-illuminazione-enlightenment|Closure: Factory Functions]]

## 📦 Factory Functions

Le closure permettono di creare **factory functions** che generano funzioni specializzate:

```javascript
function makeAdder(x) {
  function add(y) {
    return x + y; // 'add' ricorda 'x'
  }
  return add;
}

let plusOne = makeAdder(1); // Closure che ricorda x = 1
let plusTen = makeAdder(10); // Closure che ricorda x = 10

console.log(plusOne(3));  // 4  (1 + 3)
console.log(plusTen(13)); // 23 (10 + 13)
```

**Come funziona**: Ogni chiamata a `makeAdder()` crea un **nuovo scope** con una propria copia della variabile `x`. La funzione `add` restituita "ricorda" il valore di `x` del suo scope specifico, anche dopo che l'esecuzione di `makeAdder` è terminata.

### Esempio Pratico: Formattatori HTML

Le factory function sono estremamente utili per creare utility riutilizzabili con configurazioni preimpostate:

```javascript
function makeFormatter(prefix, suffix) {
  return function(str) {
    return prefix + str + suffix;
  };
}

const makeTag = makeFormatter("<p>", "</p>");
const makeBold = makeFormatter("<b>", "</b>");

console.log(makeTag("Hello"));  // <p>Hello</p>
console.log(makeBold("World")); // <b>World</b>
```

In questo caso, `makeFormatter` agisce da "fabbrica" per creare funzioni più specifiche (`makeTag`, `makeBold`). Ciascuna di queste funzioni generate mantiene una closure sui propri argomenti `prefix` e `suffix`.

## ✅ Punti Chiave

1. **Factory Functions** - Creano funzioni specializzate con configurazione chiusa.
2. **Riutilizzo del Codice** - Permettono di generare molteplici varianti di una funzione base.
3. **Stato Persistente** - Ogni funzione generata mantiene il proprio stato indipendente (closure).

## 🔗 Collegamenti

- [[closure-concept|Concetto di Closure]]
- [[closure-encapsulation|Incapsulamento e Dati Privati]]
- [[closure-loops|Closure e Cicli]]

## 📚 Risorse

- "You Don't Know JS" - Scope & Closures

## 📌 Tag

#javascript #closure #factory-pattern #design-patterns
