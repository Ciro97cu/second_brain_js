# [[../../appunti-completi#815-link-tra-oggetti-come-fallback-e-delegazione|Delegazione Interna vs Fallback Magici]]

Sebbene la catena del `[[Prototype]]` permetta oggettivamente di trovare proprietà/metodi qualora non si trovino sull'oggetto di partenza, strutturare intenzionalmente un'API per sfruttare i prototipi solo per gestire i "metodi mancanti" (fallback) porta a interfacce implicite, inaspettate o "magiche", complicandone la manutenzione.

## 🎯 Concetti Chiave

- **Il Rischio del Codice "Magico"**: Sviluppare un'API che permetta allo sviluppatore di richiamare metodi inesistenti sul target — delegandoli nel buio della catena prototipale — rende oscuro il funzionamento interno e ostacola la leggibilità per futuri interventi.
- **La Soluzione della Delegazione Interna**: È preferibile dichiarare apertamente i metodi sull'oggetto target esposto all'API. All'interno di quest'ultimo si richiamerà esplicitamente l'oggetto di fallback (es. `this.metodoCondiviso()`) per inoltrare la responsabilità mantenendo un incapsulamento pulito.
- **L'Alternativa ES6 (Proxy)**: Laddove i fallback siano una scelta obbligata e cercata, la specifica ES6 introduce i **Proxy** in grado specificamente di intercettare richieste di proprietà inesistenti svincolandosi dalla classica trafila prototipale.

## 💻 Esempi di Codice

### ❌ API Magica e Implicita (Sconsigliata)

```javascript
const behavior = {
  cool: function () {
    console.log("cool!");
  },
};

const myObject = Object.create(behavior);

// L'API è magica: si chiama `cool` ma l'oggetto myObject non lo possiede
myObject.cool(); // "cool!"
```

### ✅ Delegazione Interna ed Esplicita (Consigliata)

```javascript
const behavior = {
  cool: function () {
    console.log("cool!");
  },
};

const myObject = Object.create(behavior);

// Aggiungiamo un metodo esplicito su myObject
myObject.doCool = function () {
  // Lasciamo che la delegazione resti un "trucco" per uso interno
  this.cool();
};

// Chi usa l'API interroga un metodo tangibile e auto-documentante
myObject.doCool(); // "cool!"
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Dichiarazioni opache**: Far pesare troppe responsabilità al puro concatenamento nascosto, perdendo il controllo delle dipendenze di design e disorientando a prima vista gli sviluppatori meno coscienti del workflow.

## ✅ Best Practices

- ✓ **API auto-esplicative**: Un componente rivolto all'esterno non dovrebbe esporre una delega nuda o forzarla a fungere da safety net. Piuttosto, implementa la logica sul modello di invio esplicito, dove il ricevitore intercetta validamente la richiesta per inoltrarla alle proprie trame interne.
- ✓ **Focus sul "Come" piuttosto del "Cosa"**: Lasciare che la delega si occupi di specificare i passaggi operativi complessi in coda ma interfacciarla sempre con trigger espliciti in testa all'oggetto in primo piano.

## 🔗 Collegamenti

**Prerequisiti** (concetti da conoscere prima):

- [[object-links]]
- [[ereditarieta-prototipale-delega]]

**Concetti Correlati**:

- [[illusione-classi]]

## 📚 Riferimenti

- [MDN - Object prototypes](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes)
- _You Don't Know JS_ - Cap. 5

---

**Tags**: `#javascript` `#prototipi` `#design-pattern` `#delegazione`
