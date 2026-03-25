# [[../../appunti-completi#78-ereditarieta-multipla-multiple-inheritance|Ereditarietà Multipla]]

L'ereditarietà multipla è un design object-oriented che consente a una classe figlia di ereditare contemporaneamente da più classi genitore genitrici (come avviene biologicamente). Nonostante la sua utilità per la composizione del codice, JavaScript non ne supporta esplicitamente e nativamente l'implementazione.

## 🎯 Concetti Chiave

- **Il Desiderio di Comporre**: Ereditare assemblando comportamenti complessi da sorgenti multiple offrirebbe un inquadramento più realistico (sulla metafora Parent-Child) e un codice enormemente più flessibile e versatile.
- **Il Problema del Diamante**: Se una classe _D_ eredita da _B_ e _C_, ed entrambe queste dipendono a loro volta dallo stesso progenitore _A_, si crea una struttura a forma di rombo (o diamante). Se _B_ e _C_ sovrascrivono lo stesso metodo (es. `drive()`), al momento in cui _D_ deve richiamarlo intercorre un conflitto insormontabile: l'engine non può decidere quale dei due parent ha ragione di validità, provocando fatali ambiguità.
- **La Soluzione di JavaScript**: Per ovviare ai costi spropositati nell'ingegnerizzazione e risolvere drasticamente incomprensioni a runtime (come nel Diamante), ECMAScript/JavaScript blocca nativamente qualsiasi tentativo formale di ereditarietà multipla.

![Problema del Diamante](../../../assets/diamond-problem.png)

## 💻 Esempi di Codice

### Il Problema Concettuale

```javascript
/* Pseudocodice che mostra l'ambiguità del caso in esame */

class A {
  drive() {}
}

class B inherits A {
  drive() { output("Vado come B!"); }
}

class C inherits A {
  drive() { output("Vado come C!"); }
}

class D inherits B, C { } // Vietato in JS

let obj = new D();
obj.drive(); // Quale dovrebbe far scattare l'engine? (crash)
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Cercare di forzarla sfuggendo al compilatore**: Siccome JS non la supporta, spessissimo i programmatori usano utilità non native altamente problematiche.

## ✅ Best Practices

- ✓ **Aggirare con la Composizione**: In JavaScript si preferisce ampiamente la "Composizione" (creare oggetti mettendo insieme funzionalità non imparentate via link o deleghe, in gergo Object Composition) o i pattern specifici al posto dell'ereditarietà dura e pura.

## 🔗 Collegamenti

**Prerequisiti**:

- [[../../appunti-completi#71-teoria-delle-classi|Teoria delle Classi]]

**Approfondimenti**:

- [[mixin|Mixin ed Ereditarietà Parassita]]

## 📚 Riferimenti

- [MDN - Composition vs Inheritance](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain#composition_over_inheritance)

## 📌 Note Personali

---

**Tags**: `#javascript` `#classi` `#oop` `#composizione` `#ereditarieta`
