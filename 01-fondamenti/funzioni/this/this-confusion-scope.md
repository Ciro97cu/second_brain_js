# [[../../appunti-completi#confusione-2-this-come-riferimento-allo-scope-lessicale|Confusione: this come Riferimento allo Scope Lessicale]]

Un equivoco molto comune in JavaScript è credere che `this` si riferisca allo scope lessicale della funzione. È una questione complicata perché i concetti sembrano simili (ad esempio permettere l'accesso a dati "esterni"), ma sono profondamente diversi e non comunicanti.

Questa confusione è stata suddivisa in argomenti più specifici:

- **[[this-scope-illusion]]**: Spiega l'equivoco, analizza il tipico codice che fallisce nel tentativo di "attraversare lo scope" e chiarisce perché lo "scope object" interno all'engine non è accessibile.
- **[[this-lexical-vs-this]]**: Analizza in dettaglio le differenze architetturali tra lo scope lessicale e le regole di binding di `this`, mettendo in luce perché non esista un ponte tra i due mondi.
- **[[this-scope-solutions]]**: Fornisce le soluzioni idiomatiche (Closure, Oggetti, passaggio esplicito di argomenti) da utilizzare al posto dei tentativi fallimentari di unire i due pattern.

## 🔗 Collegamenti

**Prerequisiti**:

- [[this-concept]] - Comprendere cos'è this
- [[../scope/lexical-scope-base]] - Scope lessicale
- [[../scope/closures]] - Closure

**Concetti Correlati**:

- [[this-confusion-itself]] - L'altra confusione comune
- [[this-binding-precedence]] - Come funziona this veramente

**Approfondimenti**:

- [[../scope/scope-chain]] - Come funziona la scope chain
- [[../avanzate/execution-context]] - Context vs Scope

## 📚 Riferimenti

- **You Don't Know JS**: this & Object Prototypes - Chapter 1 "Its Scope"
- **You Don't Know JS**: Scope & Closures - Chapter 2
- **MDN**: [Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
- **MDN**: [this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)

---

**Tags**: `#javascript` `#this` `#confusioni` `#lexical-scope` `#closure` `#separation-of-concerns`
