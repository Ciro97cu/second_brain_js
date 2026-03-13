# [[../../appunti-completi#operazioni-interne-get-e-put|Operazioni Interne: [[Get]] e [[Put]]]]

In JavaScript, l'accesso e l'assegnamento dei valori di un oggetto non si limitano a una semplice lettura o scrittura in memoria. Queste azioni sono gestite da due sofisticate operazioni interne al motore del linguaggio: `[[Get]]` per il recupero e `[[Put]]` per l'assegnamento.

## 🎯 Concetti Chiave

- **Operazione `[[Get]]`**: È l'algoritmo interno che si innesca quando si cerca di leggere una proprietà. Cerca prima nell'oggetto target e, se non trova nulla, scala la catena del Prototype.
- **Tolleranza al fallimento**: Se `[[Get]]` non trova la proprietà in nessun luogo, restituisce silenziosamente `undefined`. Non emette errori bloccanti come il `ReferenceError` che avviene invece quando il Lexical Scope non trova una normale variabile.
- **Operazione `[[Put]]`**: È l'algoritmo che si attiva quando si assegna (o aggiorna) un valore. Valuta vari vincoli prima di permettere la scrittura.
- **Controlli di Sicurezza (`[[Put]]`)**: Se la proprietà esiste, `[[Put]]` verifica se c'è un `setter` in funzione o se c'è un blocco formale (`writable: false`). Se il blocco è attivo e si è in Strict Mode, fallirà lanciando un `TypeError`.

## 💻 Esempi di Codice

### Il comportamento silente di `[[Get]]`

```javascript
/*
 * Comportamento di [[Get]] rispetto al Lexical Scope
 */

var myObject = {
  a: 2,
};

// [[Get]] ispeziona myObject, trova "a" e restituisce il valore
console.log(myObject.a); // 2

// [[Get]] non trova "b" e restituisce il fallback di default in modo silente
console.log(myObject.b); // undefined

// ERRORE: il Lexical Scope fa collassare il programma se una normale variabile manca
// console.log(unaVariabileMaiCreata); // ReferenceError!
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Confondere undefined e proprietà mancante**: Siccome `[[Get]]` restituisce `undefined` per le proprietà inesistenti, non si può stabilire a colpo d'occhio, di fronte a un output come `myObject.b === undefined`, se la proprietà manca del tutto o se esiste ma il suo valore specifico salvato è letteralmente `undefined`.

## 🔗 Collegamenti

**Prerequisiti** (concetti da conoscere prima):

- [[property-access]]
- [[property-descriptors]]

**Approfondimenti** (concetti successivi):

- [[prototypes]]

## 📚 Riferimenti

- "You Don't Know JS: this & Object Prototypes" - Chapter 3: Objects

---

**Tags**: `#javascript` `#oggetti` `#get-put` `#motore-js`
