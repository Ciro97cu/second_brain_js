# [[../../appunti-completi#esistenza-delle-proprietà|Esistenza delle Proprietà]]

L'accesso a una proprietà inesistente o a una che contiene esplicitamente `undefined` restituisce lo stesso valore (`undefined`). Per distinguere i due casi, è possibile verificare direttamente l'esistenza di una proprietà in un oggetto senza leggerne il valore.

## 🎯 Concetti Chiave

- **Operatore `in`**: Controlla l'esistenza del nome della proprietà nell'oggetto stesso e in tutta la sua catena dei prototipi (`[[Prototype]]`).
- **Metodo `hasOwnProperty()`**: Verifica in modo stretto se la proprietà esiste localmente nell'oggetto, ignorando la catena dei prototipi.
- **Eccezione `Object.create(null)`**: Poiché questi oggetti non hanno un prototipo, non ereditano `hasOwnProperty`. Si aggira con `Object.prototype.hasOwnProperty.call(oggetto, "prop")`.

## 💻 Esempi di Codice

### Controllo Esistenza Base

```javascript
let mioOggetto = { a: 2, c: undefined };

// Verifica con operatore 'in'
console.log("a" in mioOggetto); // true
console.log("b" in mioOggetto); // false
console.log("c" in mioOggetto); // true (esiste anche se è undefined!)

// Verifica con hasOwnProperty
console.log(mioOggetto.hasOwnProperty("a")); // true
console.log(mioOggetto.hasOwnProperty("b")); // false
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Usare `in` sugli array aspettandosi controlli sul valore**: L'istruzione `4 in [2, 4, 6]` restituisce `false` perché cerca _l'indice_ "4" e non il valore numerico 4 (i soli indici validi per quell'array sono 0, 1 e 2).
- ❌ **Invocare `hasOwnProperty` su oggetti "vuoti"**: Se l'oggetto è derivato da `Object.create(null)`, chiamare `obj.hasOwnProperty()` lancerà un TypeError.

## 🔗 Collegamenti

**Prerequisiti**:

- [[property-access]]
- [[prototypes]]

**Concetti Correlati**:

- [[enumerabilita]]

---

**Tags**: `#javascript` `#oggetti` `#properties` `#esistenza`
