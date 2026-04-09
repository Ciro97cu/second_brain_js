# [[../../appunti-completi#99-architettura-del-codice-i-limiti-del-design-oo|Complessità Strutturale del Design OO]]

L'approccio Orientato agli Oggetti (OO) in JavaScript, sebbene nasconda meccaniche fittizie sotto nomi familiari (classi), porta spesso ad architetture estremamente rigide quando i progetti si ampliano.

## 🎯 Concetti Chiave

- **Gerarchie forzate**: Si tende a creare classi base generiche (es. `Controller`) su cui far appoggiare tutte le sottoclassi più specifiche, obbligando di fatto il codice a piegarsi rigidamente all'idea del genitore/figlio.
- **Dissonanza metodologica**: Pur di ri-utilizzare funzionalità presenti nella classe base (chiamate parenti), una funzione derivata in JS è forzata all'istradamento scomodo tramite goffe funzioni come `ClassePadre.prototype.metodo.call(this)`.
- **Ereditarietà mista a Composizione**: Se due elementi sorelle (due controller distinti) devono interagire, l'ereditarietà non ha senso pratico. In questi ambiti diviene obbligatorio ricorrere alla "composizione", passando letteralmente un'istanza completata dentro all'altra, rendendo lo sviluppo contorto.

## 💻 Esempi di Codice

### Costrutti scomodi per simularne il genitore (super)

```javascript
LoginController.prototype.failure = function (err) {
  // Una macchinosa chiamata esplicita per simulare "super" nell'oggetto base
  // Serve l'accoppiamento manuale .call(this, ... ) solo per usare un banale console error
  Controller.prototype.failure.call(this, "Login errato: " + err);
};
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Forzare l'ereditarietà tra elementi paritetici**: Rendere una classe erede dell'altra solo per comodità di funzioni al suo interno distrugge la logica semantica.
- ❌ **Creare architetture a monolite base**: Raggruppare tutto in una mega-classe padre fittizia, finendo per rendere i piccoli componenti figli vincolati a procedure elefantesche e distanti dalla loro piccola specializzazione.

## 🔗 Collegamenti

**Prerequisiti**:

- [[limiti-ereditarieta-sviluppo]] (se presente)
- [[classi-vs-oggetti]]

**Correlati**:

- [[delegazione-widget-ui]]
- [[architettura-oloo]] (prossimo approccio)

## 📚 Riferimenti

- Libro: _You Don't Know JS - This & Object Prototypes_

---

**Tags**: `#javascript` `#struttura` `#oop` `#design`
