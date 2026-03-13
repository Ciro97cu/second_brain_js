# [[../../appunti-completi#enumerabilità|Enumerabilità]]

L'enumerabilità è una caratteristica (descrittore) delle proprietà degli oggetti che determina se esse debbano essere incluse o meno durante i cicli di iterazione (come il `for..in`).

## 🎯 Concetti Chiave

- **Proprietà Enumerabili**: Di default le proprietà di un oggetto lo sono, il che significa che verranno regolarmente lette ed esposte quando si scorrono le chiavi o le proprietà visibili dell'oggetto.
- **Nascondere Proprietà**: Utilizzando i descrittori (es. `Object.defineProperty(...)` con `enumerable: false`), la proprietà continua a esistere e resta accessibile direttamente, ma risulta invisibile al loop `for..in` e a `Object.keys()`.
- **Estrazione Proprietà**: È possibile ottenere array di sole chiavi enumerabili (`Object.keys()`) o di tutte le chiavi locali indifferentemente dal loro flag (`Object.getOwnPropertyNames()`).

## 💻 Esempi di Codice

### Nascondere all'iterazione

```javascript
let mioOggetto = {};

// Proprietà standard enumerabile
Object.defineProperty(mioOggetto, "a", { enumerable: true, value: 2 });
// Proprietà creata come non enumerabile
Object.defineProperty(mioOggetto, "b", { enumerable: false, value: 3 });

console.log(mioOggetto.b); // 3 (è perfettamente accessibile!)
console.log("b" in mioOggetto); // true (esiste davvero)

for (let k in mioOggetto) {
  console.log(k, mioOggetto[k]);
}
// Stampa SOLO: "a" 2. La chiave 'b' viene saltata all'interno dell'iteratore.
```

### Ispezionare Enumerabilità

```javascript
// La proprietà deve esistere direttamente nell'oggetto ed essere enumerabile
mioOggetto.propertyIsEnumerable("a"); // true
mioOggetto.propertyIsEnumerable("b"); // false

Object.keys(mioOggetto); // ["a"]
Object.getOwnPropertyNames(mioOggetto); // ["a", "b"]
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Usare il ciclo `for..in` sugli Array**: Poiché la loro enumerazione andrebbe a includere non soltanto gli indici numerici classici, ma anche eventuali proprietà enumerabili custom aggiunte casualmente all'array, produce comportamenti inattesi. Sugli array risulta preferibile utilizzare i classici cicli numerici o i più moderni iterator (`for..of`).

## 🔗 Collegamenti

**Prerequisiti**:

- [[property-descriptors]]
- [[esistenza-proprieta]]

**Concetti Correlati**:

- [[property-access]]

---

**Tags**: `#javascript` `#oggetti` `#enumerabilita` `#iterazione`
