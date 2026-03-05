# [[../../appunti-completi#311-lidentificatore-this|Il Concetto di this]]

La keyword `this` è uno dei meccanismi più fraintesi in JavaScript. Si tratta di un identificatore speciale definito automaticamente nello scope di ogni funzione.

## 🎯 Concetti Chiave

- **Binding dinamico**: Il valore di `this` dipende da **come** la funzione viene chiamata (call-site), NON da dove è stata definita
- **Equivoco comune**: `this` NON si riferisce alla funzione stessa
- **Contesto implicito**: Fornisce un modo elegante per passare implicitamente un riferimento a un oggetto
- **Quattro regole**: Esistono 4 regole che determinano il valore di `this` (default, implicit, explicit, new)

## 💡 Perché this Esiste

Il meccanismo `this` permette di scrivere funzioni riutilizzabili che operano su oggetti diversi senza dover passare esplicitamente l'oggetto come parametro ogni volta.

**Vantaggio**: API più pulite e codice più elegante quando si lavora con pattern orientati agli oggetti.

## 💻 Esempio Motivazionale

### Approccio con this (più elegante)

```javascript
function identify() {
  return this.name.toUpperCase();
}

function speak() {
  var greeting = "Hello, I'm " + identify.call(this);
  console.log(greeting);
}

var me = { name: "Kyle" };
var you = { name: "Reader" };

identify.call(me); // KYLE
identify.call(you); // READER
speak.call(me); // Hello, I'm KYLE
speak.call(you); // Hello, I'm READER
```

### Approccio senza this (più verboso)

```javascript
function identify(context) {
  return context.name.toUpperCase();
}

function speak(context) {
  var greeting = "Hello, I'm " + identify(context);
  console.log(greeting);
}

identify(you); // READER
speak(me); // Hello, I'm KYLE
```

Più complesso diventa il pattern, più evidente diventa il vantaggio di `this`.

## ⚠️ Confusioni Comuni

- ❌ **"this si riferisce alla funzione stessa"**: FALSO. `this` punta a un oggetto esterno
- ❌ **"this dipende da dove scrivo la funzione"**: FALSO. Dipende da come viene chiamata (call-site)
- ❌ **"this è fisso quando definisco una function"**: FALSO. È un binding dinamico determinato alla chiamata

## ✅ Principio Fondamentale

**Quando una funzione contiene `this`, quel riferimento punta a un oggetto. L'oggetto dipende ESCLUSIVAMENTE dal call-site (come viene chiamata la funzione).**

Per capire `this`:

1. Trova il call-site (dove viene invocata la funzione)
2. Applica le regole di binding nell'ordine di precedenza
3. L'oggetto risultante è il valore di `this`

## 🔗 Collegamenti

**Prerequisiti**:

- [[funzioni]] - Comprendere le funzioni JavaScript
- [[../scope/lexical-scope-base]] - Differenza tra scope lessicale e binding dinamico

**Concetti Correlati**:

- [[this-binding-rules]] - Le quattro regole del binding
- [[this-call-apply-bind]] - Metodi per controllare this
- [[this-binding-problems]] - Problemi comuni e soluzioni

**Approfondimenti**:

- [[../oggetti/oggetti]] - This nei metodi degli oggetti
- [[../oggetti/prototypes]] - This nel contesto dei prototipi

## 📚 Riferimenti

- **You Don't Know JS**: Scope & Closures - Chapter "this Or That?"
- **MDN**: [this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
- **JavaScript.info**: [Object methods, "this"](https://javascript.info/object-methods)

## 📌 Note Personali

[Spazio per annotazioni personali su this]

---

**Tags**: `#javascript` `#this` `#binding` `#context` `#oggetti`
