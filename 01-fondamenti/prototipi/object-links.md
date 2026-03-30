# [[../../appunti-completi#814-collegamenti-tra-oggetti-object-links-e-objectcreate|Object Links e Object.create()]]

L'uso esclusivo di `Object.create(..)` incarna la vera essenza comportamentale di JavaScript: collegare direttamente gli oggetti (_Object Links_) eliminando ogni finzione semantica complessa legata alle classi (come `.prototype` isolati, costruttori e l'operatore `new`).

## 🎯 Concetti Chiave

- **Delega Diretta**: `Object.create(obj)` genera un oggetto vuoto il cui `[[Prototype]]` punta direttamente a `obj`, snellendo drasticamente tutta l'impalcatura che avvolge le false dinamiche di ereditarietà.
- **Dizionari (`Object.create(null)`)**: Passando `null`, il nuovo oggetto è privo di alcun link di risalita (non delega neanche a `Object.prototype`). Tale isolamento li rende contenitori "piatti" eccellenti e sicuri contro impatti/override indesiderati dall'ereditarietà base.
- **Polyfill Esistente**: Fino all'avvento definitivo di ES5, l'unico modo per simulare questa delega pulita passava attraverso una banale funzione temporanea il cui prototype era fatto puntare all'oggetto desiderato, prima di evocarne l'istanza.

## 💻 Esempi di Codice

### Link diretto bypassando Constructor ed Ereditarietà

```javascript
const foo = {
  something: function () {
    console.log("Accedo al metodo condiviso");
  },
};

// Crea bar, collegato internamente ({ [[Prototype]] }) a foo
const bar = Object.create(foo);

// Delega in azione: non avendolo su 'bar', risolve la chiamata su 'foo'
bar.something();
```

### Il Polyfill concettuale

```javascript
if (!Object.create) {
  Object.create = function (o) {
    function F() {}
    F.prototype = o;
    // Ritorna la simulazione che il metodo nativo compie nel core engine
    return new F();
  };
}
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Sovraccarico architetturale sfuggente**: Intrecciare un set spropositato di classi simulando il mondo Java (con `new Padri()`) aggiunge latenza relazionale e boilerplate, allontanandosi dal core object-oriented nativo che è semplicemente l'interrogazione tramite Link.

## ✅ Best Practices

- ✓ **Data Structuring con null**: Quando ti serve semplicemente una Map rudimentale o una borsa di dati esente dalla prototipazione globale (es. evitare che compaia `.toString()`), usa serenamente `var dic = Object.create(null)`.

## 🔗 Collegamenti

**Prerequisiti**:

- [[catena-prototipi]]
- [[ereditarieta-prototipale]]

**Concetti Correlati**:

- [[meccaniche-classi]]

**Approfondimenti**:

- [[introspezione-prototipi]]

## 📚 Riferimenti

- Libro: "You Don't Know JS"
- Capitolo: Prototypes

## 📌 Note Personali

[Spazio per riflessioni, domande, applicazioni personali]

---

**Tags**: `#javascript` `#prototipi` `#object-create` `#object-links` `#polyfill`
