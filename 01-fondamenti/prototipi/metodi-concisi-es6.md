# [[../../appunti-completi#911-oloo-e-sintassi-es6-metodi-concisi-e-limiti|Metodi Concisi ES6 e OLOO]]

Con ES6, la comodità estetica di rimuovere la parola `function` nella definizione dei metodi non è un'esclusiva delle classi. È possibile adottare la sintassi dei "metodi concisi" all'interno di normali oggetti letterali (tra parentesi graffe), ripulendo notevolmente il codice in stile OLOO.

## 🎯 Concetti Chiave

- **Sintassi Superflua Rimossa**: Eliminando i due punti `:` e la parola `function`, assegnare un'azione a un oggetto risulta immediato (es: `checkAuth() { ... }`).
- **Post-Assegnazione Strutturale**: Scrivendo un intero oggetto letterale pulito in prima battuta, è successivamente possibile congiungerlo al suo delegato tramite `Object.setPrototypeOf(A, B)`.
- **Limiti dell'Anonimato Lessicale**: Un metodo conciso diviene internamente una comune funzione anonima. Questo ostacola i processi di _auto-referenziazione_, essenziali se la funzione deve chiamare se stessa (ricorsione) o auto-rimuoversi da un `addEventListener()`.

## 💻 Esempi di Codice

### Creazione Fluida di un Delegato OLOO

```javascript
// La sintassi concisa ES6 rende il modulo pulitissimo
var AuthController = {
  checkAuth() {
    /* codice omesso */
  },
  server(url, data) {
    /* codice omesso */
  },
};

// Connessione delegata all'amico LoginController
Object.setPrototypeOf(AuthController, LoginController);
```

### Il fallimento nei cicli Ricorsivi

```javascript
var Foo = {
  // Essendo anonimo, "bar" non possiede il proprio nome all'interno!
  bar(x) {
    if (x < 10) {
      // Devo affidarmi al percorso Foo.bar(x), una mossa mortale
      // se l'oggetto venisse rinominato o il this si disperdesse!
      return Foo.bar(x * 2);
    }
  },

  // Torno alla faticosa forma estesa ma prevengo ogni bug futuri:
  baz: function baz(x) {
    if (x < 10) {
      // Avendo un nome lessicale garantito (baz), non fallirò mai
      return baz(x * 2);
    }
  },
};
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Sfruttare percorsi esterni a rischio**: Sfruttare `Foo.bar()` da dentro un blocco conciso (per simulare una ricorsione) equivale a innescare bug se il `this` assume valori diversi.
- ❌ **Abuso dei metodi concisi**: Scegliere la veste grafica snella sacrificando meccanismi stabili (come il self-reference per unbinding di eventi in DOM).

## ✅ Best Practices

- ✓ La "concise method syntax" è preferibile e raccomandata in OLOO.
- ✓ Rinunciarvi temporaneamente, ricadendo a `nome: function nome() {..}`, **solo** in presenza di ricorsioni interne necessarie o agganci complessi.

## 🔗 Collegamenti

**Prerequisiti**:

- [[architettura-oloo]]

**Correlati**:

- [[delegazione-widget-ui]]
- [[identificatore-this]] (impatto sulle funzioni interne)

## 📚 Riferimenti

- Libro: _You Don't Know JS - This & Object Prototypes_

---

**Tags**: `#javascript` `#es6` `#oloo` `#sintassi`
