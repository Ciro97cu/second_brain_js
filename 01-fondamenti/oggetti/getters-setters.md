# [[../../appunti-completi#getter-e-setter-metodi-di-accesso|Getter e Setter (Metodi di Accesso)]]

I _getter_ e _setter_ sono funzioni speciali che all'esterno si comportano come normali proprietà di un oggetto. Servono a intercettare silenziosamente il momento in cui un valore viene letto o modificato, permettendo di incapsulare e nascondere logiche interne (come validazioni o calcoli dinamici) mantenendo semplice l'interfaccia dell'oggetto.

## 🎯 Concetti Chiave

- **Accessor Descriptor**: Definendo get o set, la proprietà cambia "natura" (da _Data_ ad _Accessor_). Gli attributi base `value` e `writable` del descrittore vengono totalmente ignorati in favore delle funzioni fornite.
- **Sovrascrittura**: Queste funzioni non fanno altro che scavalcare e personalizzare le rigide operazioni predefinite del motore (`[[Get]]` per la lettura e `[[Put]]` per la scrittura).
- **Lavoro di Coppia**: È raccomandato definire sempre sia il getter che il setter. Avere solo un getter genera vulnerabilità silenziose alle scritture.
- **Convenzione pseudo-privata**: Molto spesso si incapsula il valore grezzo in una proprietà di appoggio col nome che inizia per underscore (es. `_a_`). Non è nativamente "privata", ma è una convenzione universale tra sviluppatori per indicare un dato "interno".

## 💻 Esempi di Codice

### Utilizzo combinato di Getter e Setter

Il modo più comune per definirli è tramite il formato object-literal base.

```javascript
/*
 * Utilizzo congiunto di Getter e Setter
 */
var myObject = {
  // Quando si legge "a", intercetta e restituisce "_a_"
  get a() {
    return this._a_;
  },

  // Quando si scrive "a", intercetta, raddoppia e salva in "_a_"
  set a(valore) {
    this._a_ = valore * 2;
  },
};

myObject.a = 2; // Scatta il setter: viene passato "2", ma salvato "4" in _a_
console.log(myObject.a); // 4 (Scatta il getter che va a leggerlo)
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Getter orfano**: Se si imposta **solo** un getter per una proprietà senza un relativo setter, eventuali tentativi futuri di assegnarle nuovi valori non scaturiranno in un errore bloccante, ma falliranno completamente in silenzio. Il comando di assegnazione verrà letteralmente cestinato.

## 🔗 Collegamenti

**Prerequisiti** (concetti da conoscere prima):

- [[property-descriptors]]
- [[get-put]]

**Concetti Correlati**:

- [[object-literal-vs-constructed]]
- [[property-access]]

## 📚 Riferimenti

- "You Don't Know JS: this & Object Prototypes" - Chapter 3: Objects

---

**Tags**: `#javascript` `#oggetti` `#getter` `#setter` `#accessor`
