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

Prima di comprendere come `this` funziona, è fondamentale dissipare due equivoci comuni su come **NON** funziona.

### ❌ Confusione #1: "this = la funzione stessa"

Molti pensano che `this` si riferisca alla funzione stessa. **È FALSO**.

```javascript
function foo(num) {
  this.count++; // ❌ this NON è foo!
}

foo.count = 0;
foo(); // this.count++ crea variabile globale, non modifica foo.count
console.log(foo.count); // 0 (non cambia!)
```

In chiamata diretta `foo()`, `this` punta al **global object** (default binding), non alla funzione.

**Dettagli completi**: Vedi [[this-confusion-itself]] per esempi e soluzioni

### ❌ Confusione #2: "this = lo scope lessicale"

Alcuni pensano che `this` permetta di accedere allo scope lessicale. **È FALSO**.

```javascript
function foo() {
  var a = 2;
  this.bar(); // ❌ Non crea ponte tra scope!
}

function bar() {
  console.log(this.a); // ❌ Non accede alla 'a' di foo!
}
```

`this` e lexical scope sono **meccanismi completamente separati**. Non esiste ponte tra i due.

**Dettagli completi**: Vedi [[this-confusion-scope]] per la spiegazione approfondita

### Altre Confusioni Rapide

- ❌ **"this dipende da dove scrivo la funzione"**: FALSO. Dipende dal call-site
- ❌ **"this è fisso alla definizione"**: FALSO. È dinamico (call-time)
- ❌ **"this e scope sono collegati"**: FALSO. Sono meccanismi indipendenti

## ✅ Principio Fondamentale

**`this` è un runtime binding, non un author-time binding.**

Il valore di `this` non dipende da dove una funzione è dichiarata, ma da **come viene chiamata**. È contestuale e basato sulle condizioni dell'invocazione della funzione.

### Execution Context

Quando una funzione viene invocata, JavaScript crea un **execution context** (contesto di esecuzione) che contiene:

- **Call-stack**: Da dove è stata chiamata la funzione
- **Parametri**: Valori passati alla funzione
- **this reference**: Il binding di `this` per quella esecuzione
- Altre informazioni sul contesto

Il riferimento `this` viene determinato al momento dell'invocazione e rimane fisso per tutta la durata dell'esecuzione della funzione.

### Come Determinare this

Per capire quale sarà il valore di `this`:

1. **Trova il call-site** - Il punto nel codice dove la funzione viene invocata
2. **Applica le regole di binding** - Nell'ordine di precedenza (new > explicit > implicit > default)
3. **L'oggetto risultante è `this`** - Per tutta la durata dell'esecuzione

## 🔗 Collegamenti

**Prerequisiti**:

- [[funzioni]] - Comprendere le funzioni JavaScript
- [[../scope/lexical-scope-base]] - Differenza tra scope lessicale e binding dinamico

**Concetti Correlati**:

- [[this-confusion-itself]] - Confusione: "this = funzione stessa"
- [[this-confusion-scope]] - Confusione: "this = scope lessicale"
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
