# [[../../../appunti-completi#311-lidentificatore-this|Default Binding (Regola 1)]]

La **default binding** è la prima regola del binding di `this` e rappresenta il caso più comune: l'invocazione standalone di una funzione senza contesto specifico. 

Per esaminare a fondo i vari aspetti della default binding, il tema è stato suddiviso nei seguenti approfondimenti atomici:

- [[this-default-intro|Introduzione alla Default Binding]]: Concetti chiave, chiamate plain function e il global object.
- [[this-default-strict-mode|Default Binding in Strict Mode]]: Come lo strict mode (nel call-site o nella funzione) altera il binding di `this`.
- [[this-default-gotchas|Gotchas e Best Practices]]: Differenze tra `var` e `let`/`const`, IIFE e le best practice per gestire la default binding in modo prevedibile.

## 🔗 Collegamenti

**Prerequisiti**:
- [[this-concept]] - Comprendere cos'è this
- [[../funzioni]] - Funzioni JavaScript base

**Regole Correlate**:
- [[this-binding-implicit]] - Implicit binding (regola 2)
- [[this-binding-explicit]] - Explicit binding (regola 3)
- [[this-binding-new]] - New binding (regola 4)
- [[this-binding-precedence]] - Ordine di precedenza delle regole

**Approfondimenti**:
- [[../../scope/strict-mode]] - Strict mode in dettaglio
- [[../../scope/lexical-scope-base]] - Scope lessicale vs this

## 📚 Riferimenti
- **You Don't Know JS**: this & Object Prototypes - Chapter 2
- **MDN**: [this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
- **MDN**: [Strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)

---
**Tags**: `#javascript` `#this` `#default-binding`
