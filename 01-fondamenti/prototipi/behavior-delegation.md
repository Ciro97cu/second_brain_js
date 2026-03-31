# [[../../appunti-completi#91-verso-un-design-orientato-alla-delegazione|Behavior Delegation vs Teoria delle Classi]]

In JavaScript, l'architettura di sviluppo si allontana intimamente dal design a classi (basato sull'ereditarietà e sulle copie d'istanza) per spingersi verso un pattern chiamato **Behavior Delegation** (Delegazione del Comportamento). Questo design si focalizza sulla cooperazione tra oggetti direttamente collegati tra loro e non sulla riproduzione genetica da matrici preesistenti.

## 🎯 Concetti Chiave

- **Il Rifiuto delle Copie**: Mentre le classi tradizionali (ed i relativi pattern polimorfici basati su `super()`) distribuiscono fisicamente una copia o duplicato dei comportamenti per ciascuna istanza generata, l'astrazione via delegazione si limita e far _riferimento_ ad altri oggetti, risparmiando allocazione e ingarbugliamenti astratti.
- **Cambio di Mentalità (_Mindset Shift_)**: Capire come il target di JS consista unicamente nel legare nativamente "utensili ad altri utensili" svaluta radicalmente la necessità di ricorrere a costruttori astratti o finte classi madri generiche.
- **Rivalutare i Task**: Nel paradigma a classi, attività distinte ("XYZ" e "ABC") vengono per natura figlie di un macro-genitore astratto (`class Task`). Nel mondo OLOO (Objects Linked to Other Objects), si concepiscono i domini di competenza per via relazionale.

## 💻 Esempi di Codice

### Costrutto mentale a Classi (Pseudocodice)

```javascript
/* Architettura basata sull'istanziazione e specializzazione polimorfica */

class Task {
  Task(ID) {
    this.id = ID;
  }
}

class XYZ inherits Task {
  XYZ(ID, Label) {
    // Richiamo genitore prima della specializzazione
    super(ID);
    this.label = Label;
  }
}

// Interazione in cui myTask possiede COPIE vere di tutti metodi e campi
let myTask = new XYZ("001", "Primo Task");
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Sotterrare l'Architettura**: Spesso sviluppatori inesperti si appoggiano a "scatole nere" (librerie o sintassi ingannevole) per riprodurre a forza classi su JS, precludendosi l'adattamento ai concetti nativi dei prototipi.
- ❌ **Scartare interamente le buone pratiche ad Oggetti**: Passare alla delegazione _non svilisce_ meccaniche standard stabili come l'Incapsulamento (che funziona comunque nei modelli architetturali a cascata).

## ✅ Best Practices

- ✓ **Focalizzarsi unicamente sul Prototype**: Ricordare costantemente in fase architetturale che se JS non possiede un attributo di base proverà per sua natura una risalita fino a `Object.prototype`, ed organizzare la delega per intercettare i passaggi sensati a monte.

## 🔗 Collegamenti

**Prerequisiti** (concetti da conoscere prima):

- [[illusione-classi]]
- [[object-links]]
- [[delegazione-vs-ereditarieta]]

**Concetti Correlati**:

- [[catena-prototipi]]

## 📚 Riferimenti

- _You Don't Know JS_ - Cap. 6 (Behavior Delegation)

---

**Tags**: `#javascript` `#prototipi` `#design-pattern` `#delegazione`
