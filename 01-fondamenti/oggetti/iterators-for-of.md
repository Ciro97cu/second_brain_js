# [[../../appunti-completi#iterabilità-e-forof|Iterabilità e Ciclo for..of]]

Il meccanismo di iterazione sui _valori_ (in contrapposizione a quello sulle _chiavi_ gestito da `for..in`) si basa unicamente sull'esistenza di un apposito Iteratore interno collegato alla struttura dati, introdotto ufficialmente con l'avvento dei costrutti `for..of` su ECMAScript 6.

## 🎯 Concetti Chiave

- **Il costrutto `for..of`**: Permette di ciclare fluidamente sui _valori_ veri e propri contenuti in array, set, etc. bypassando l'estrazione e i passaggi manuali su indici tipici dei vecchi approcci.
- **L'interfaccia `@@iterator`**: Affinchè un tipo di struttura dati sia iterabile via `for..of`, necessita della proprietà interna `@@iterator`. È una funzione che ritorna un oggetto governato dal metodo `.next()`, col compito di sputare fuori il valore un passo dopo l'altro nel formato `{ value: ..., done: boolean }`.
- **Iteratori di Default**: Gli Array standard, le Stringhe e altri tipi di liste moderne espongono l'iteratore nativamente.
- **Oggetti normali non iterabili**: I comuni e semplici POJO (`{}`) **non** hanno nessun iteratore nativo attaccato. Un tentativo `for (v of {})` solleva errore.

## 💻 Esempi di Codice

### `for..of` su Iteratori Nativi (Array)

```javascript
let mioArray = [1, 2, 3];

// Iterazione dei VALORI, non delle chiavi (0,1,2).
for (let v of mioArray) {
  console.log(v);
}
// 1
// 2
// 3

// Esecuzione manuale mascherata da for..of
let iteratore = mioArray[Symbol.iterator]();
iteratore.next(); // { value: 1, done: false }
iteratore.next(); // { value: 2, done: false }
iteratore.next(); // { value: 3, done: false }
iteratore.next(); // { value: undefined, done: true }
```

### Costruire Iteratori Custom in Oggetti

Rendiamo un banale oggetto anonimo navigabile col `for..of`:

```javascript
let iterOggetto = {
  a: 2,
  b: 3,
};

Object.defineProperty(iterOggetto, Symbol.iterator, {
  enumerable: false,
  value: function () {
    let o = this;
    let chiavi = Object.keys(o);
    let id = 0;
    return {
      next: () => ({ value: o[chiavi[id++]], done: id > chiavi.length }),
    };
  },
});

for (let x of iterOggetto) {
  console.log(x); // '2', poi '3'. Inizierebbe a scorrere correttamente!
}
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Ordine garantito sugli oggetti**: L'ordine in cui un iteratore custom scorre le proprietà standard di un generico oggetto riflette le logiche del motore runtime Javascript: non ci si può affidare ad una precisione cronologica del 100% rispetto all'ordine inserito come codice scritto se confrontata in ambienti dissimili (per gli Array o le Map è invece garantito).
- ❌ **Loop su Iteratori "Infiniti"**: Si può implementare un iteratore a loop infinito che produce ID seriali all'infinito `{ next: () => ({value: Math.random()}) }`. Metterlo dentro a un `for..of` provocherebbe un blocco catastrofico a meno di un guard (`if (..) break;`).

## 🔗 Collegamenti

**Prerequisiti**:

- [[array]]
- [[oggetti]]

**Concetti Correlati**:

- [[enumerabilita]]

---

**Tags**: `#javascript` `#iterators` `#for-of`
