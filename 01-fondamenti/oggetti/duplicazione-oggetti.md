# [[../../appunti-completi#duplicazione-degli-oggetti|Duplicazione degli Oggetti]]

In JavaScript, la duplicazione di un oggetto è un'operazione complessa in quanto non esiste un metodo nativo universale `copy()`. La scelta dell'algoritmo dipende dalla necessità di eseguire una copia superficiale (_shallow copy_) o profonda (_deep copy_).

## 🎯 Concetti Chiave

- **Shallow Copy (Copia Superficiale)**: Crea un nuovo oggetto duplicando direttamente i valori primitivi, ma copiando solo i riferimenti per gli oggetti o array annidati.
- **Deep Copy (Copia Profonda)**: Duplica sia l'oggetto principale che tutti gli oggetti annidati. Può causare problemi strutturali in presenza di riferimenti circolari (_circular references_).
- **Problema delle Funzioni**: Non esiste un modo concettualmente standard per duplicare in modo affidabile una funzione, rendendo le _deep copy_ ancora più instabili.

## 💻 Esempi di Codice

### Il Problema dei Riferimenti

```javascript
var anotherObject = { c: true };
var myObject = {
  a: 2,
  b: anotherObject, // riferimento all'originale, non una copia!
};
```

### JSON-Safe Hack (Deep Copy Limitata)

Per gli oggetti che contengono solo dati serializzabili (senza funzioni, `undefined` o riferimenti circolari), si può sfruttare il parsing JSON:

```javascript
/*
 * Duplicazione rapida tramite serializzazione JSON.
 * Applicabile esclusivamente a oggetti JSON-safe.
 */
var newObj = JSON.parse(JSON.stringify(myObject));
```

### Lo Standard ES6: Object.assign()

L'approccio standardizzato in ES6 per la copia superficiale è `Object.assign()`, che itera e copia tutte le proprietà proprie (_owned keys_) ed enumerabili sull'oggetto di destinazione:

```javascript
/*
 * Duplicazione di tipo shallow-copy tramite Object.assign
 */
var targetObj = {};
var newObj = Object.assign(targetObj, myObject);

console.log(newObj.a); // 2 (primitivo copiato)
console.log(newObj.b === anotherObject); // true (stesso riferimento condiviso)
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Perdita dei Property Descriptors**: `Object.assign()` utilizza una banale assegnazione (`=`). Pertanto, non preserva le caratteristiche avanzate definite nell'oggetto sorgente, come l'attributo `writable: false` o implementazioni di getter/setter.
- ❌ **Effetti Collaterali Sugli Annidamenti**: Trattandosi di _shallow copy_, modificare il contenuto di `newObj.b.c` altererà inevitabilmente anche `myObject.b.c`.

## ✅ Best Practices

- ✓ **Preferire la Shallow Copy**: Poiché una copia profonda solleva dubbi irrisolvibili riguardo riferimenti circolari e chiusure funzionali, la shallow copy risulta notevolmente più sicura e prevedibile.
- ✓ **Gestione Manuale vs Librerie**: Se è indispensabile una deep copy per una struttura complessa, risulta spesso più sicuro utilizzare implementazioni consolidate (come il `cloneDeep` di librerie esterne) piuttosto che scriversi algoritmi ricorsivi personalizzati.

## 🔗 Collegamenti

**Prerequisiti**:

- [[oggetti]]
- [[../tipi/valori-tipi]]

**Correlati**:

- [[property-vs-method]]
- [[../array/array-come-oggetti]]
