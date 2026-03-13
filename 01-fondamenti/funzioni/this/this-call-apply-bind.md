# [[../../../appunti-completi#311-lidentificatore-this|call(), apply() e bind()]]

JavaScript offre tre metodi nativi principali (presenti nel `Function.prototype`) per manipolare esplicitamente il binding dell'identificatore `this`. Questi metodi ignorano le normali regole di binding implicito e forzano una funzione ad adottare uno specifico oggetto come contesto di esecuzione.

## 🧭 Navigazione Sotto-Concetti

Questo argomento è stato suddiviso nei seguenti topic atomici:

- **[[this-call-apply|call() e apply()]]**: Per l'invocazione immediata di funzioni (Explicit Binding diretto), con "prestito" di metodi e array di argomenti.
- **[[this-bind-method|bind() e Hard Binding]]**: Per la creazione di callback "sicure", il congelamento permanente del contesto e il currying parziale dei parametri.

## 📊 Confronto Metodi

| Metodo    | Esecuzione | Argomenti | Ritorno            | Permanente |
| --------- | ---------- | --------- | ------------------ | ---------- |
| `call()`  | Immediata  | Lista     | Risultato funzione | No         |
| `apply()` | Immediata  | Array     | Risultato funzione | No         |
| `bind()`  | Nessuna    | Lista     | Nuova funzione     | Sì         |

## 🔗 Collegamenti

**Prerequisiti**:

- [[this-concept]] - Comprendere this
- [[this-binding-explicit]] - Regola di explicit binding generale

**Concetti Correlati**:

- [[this-binding-problems]] - Quando usare bind per risolvere problemi (come le callback distaccate)
- [[this-arrow-functions]] - Alternative moderne al binding per le callback
- [[funzioni]] - Funzioni JavaScript base e prototype

**Approfondimenti**:

- [[../avanzate/currying]] - Currying e partial application avanzati
- [[../avanzate/function-methods]] - Altri metodi delle funzioni nativi

## 📚 Riferimenti

- **MDN**: [Function.prototype.call()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)
- **MDN**: [Function.prototype.apply()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)
- **MDN**: [Function.prototype.bind()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
- **You Don't Know JS**: this & Object Prototypes - Chapter 2

## 📌 Note Personali

[Annotazioni sulla scelta tra call, apply e bind]

---

**Tags**: `#javascript` `#this` `#call` `#apply` `#bind` `#explicit-binding`
