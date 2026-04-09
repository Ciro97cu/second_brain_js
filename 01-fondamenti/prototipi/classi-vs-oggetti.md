# [[../../appunti-completi#97-classi-vs-oggetti-un-caso-pratico-widget-ui|Classi vs Oggetti (Widget UI)]]

Per modellare scenari comuni come la creazione di elementi UI (es. un bottone), usare lo schema Object-Oriented (OO) in JS porta con sé inevitabili fardelli sintattici e concettuali, derivanti dalla forzatura di imporre "classi" in un linguaggio basato intrinsecamente sulla delegazione.

## 🎯 Concetti Chiave

- **Il pattern OO pre-ES6 è macchinoso**: Estendere comportamenti base richiede complesse esecuzioni esplicite (`Widget.prototype.render.call(this)`) per simulare artificialmente il comando "super" tra i livelli del prototipo.
- **Lo "Syntax Sugar" di ES6 nasconde senza risolvere**: Le keyword `class` ed `extends`, unitamente alla funzione `super()`, rendono l'aspetto estetico del codice moderno ma mascherano malamente lo stesso meccanismo `[[Prototype]]` sottostante.
- **Le Classi ES6 NON sono reali classi**: Continuano a presentare le stesse incongruenze mentali esplorate nei design pattern precedenti.
- **La scelta architetturale conta**: Decidere di imitare il concetto di classe in JS costringe il developer a lottare inconsciamente contro il modello nativo della macchina, alzando decisamente il livello della complessità e della confusione cognitiva.

## 💻 Esempi di Codice

### Costrutto "Super" Pre-ES6 (da evitare)

```javascript
// Metodo della classe figlia che invoca quello della classe madre
Button.prototype.render = function ($where) {
  // Chiamata "super" esplicita e verbosa
  Widget.prototype.render.call(this, $where);
  this.$elem.click(this.onClick.bind(this));
};
```

### Costrutto ES6 Sugar

```javascript
class Button extends Widget {
  render($where) {
    super.render($where); // Molto più pulito, ma è solo un'illusione (syntax sugar)
    this.$elem.click(this.onClick.bind(this));
  }
}
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Considerare ES6 "class" una vera funzionalità OO**: Pur assumendo sintassi di stampo Java/C++, JS continua a operare i collegamenti via delega dinamica, portando a inaspettati comportamenti a runtime se la progettazione ignora questa peculiarità.

## ✅ Best Practices

- ✓ Considerare sempre le conseguenze di design architetturale prima di avvalersi aprioristicamente del formato in classi per "comodità visiva", focalizzandosi, quando si può, su pattern OLOO puri per restare fedeli alla logica di derivazione dinamica nativa in JS.

## 🔗 Collegamenti

**Prerequisiti**:

- [[pattern-oloo]]
- [[illusione-classi]]

**Concetti Correlati**:

- [[costruttori-e-chiamate]]
- [[confronto-oo-oloo]]
