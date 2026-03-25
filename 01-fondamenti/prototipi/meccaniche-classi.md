# [[../../appunti-completi#810-meccaniche-e-simulazione-delle-classi|Meccaniche e Simulazione delle Classi]]

Per simulare il paradigma orientato agli oggetti in JavaScript, si combinano il `this` interno per l'incapsulamento e la manipolazione del `.prototype` per i metodi condivisi. Quando si crea un'istanza tramite `new`, non avvengono copie, ma si stabilisce un collegamento `[[Prototype]]` che delega le richieste al prototipo.

## 🎯 Concetti Chiave

- **Il `this` interno**: Utilizzato per definire dati specifici (incapsulamento) per la singola istanza.
- **Manipolazione del `.prototype`**: Sfruttata per dichiarare metodi che tutte le istanze condivideranno.
- **Assenza di copia**: Le istanze create con `new` non ricevono una copia dei comportamenti, ma usano il `[[Prototype]]` invisibile per delegare le risoluzioni all'oggetto genitore.

## 💻 Esempi di Codice

### Esempio Base

```javascript
function Foo(name) {
  this.name = name; // Iniezione di incapsulamento (dati specifici dell'istanza)
}

// Iniezione di un metodo valido per tutte le istanze
Foo.prototype.myName = function () {
  return this.name;
};

const a = new Foo("a");
const b = new Foo("b");

console.log(a.myName()); // "a"
console.log(b.myName()); // "b"
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Falso mito della copia**: Istanziando un oggetto, si tende erroneamente a postulare una _copia_ del prototipo all'interno dell'istanza. Al contrario, JavaScript _delega_ unicamente l'accesso ai metodi condivisi residenti al piano gerarchico superiore.

## ✅ Best Practices

- ✓ **Separazione di competenze**: Mantieni le proprietà variabili incapsulate nel costruttore tramite `this` e delega sempre i metodi statici o funzionali al livello del `.prototype` per fare economia di memoria.

## 🔗 Collegamenti

**Prerequisiti**:

- [[costruttore]]
- [[catena-prototipi]]

**Concetti Correlati**:

- [[illusione-classi]]

**Approfondimenti**:

- [[inaffidabilita-constructor]]

## 📚 Riferimenti

- Libro: "You Don't Know JS"
- Capitolo: Prototypes

## 📌 Note Personali

[Spazio per riflessioni, domande, applicazioni personali]

---

**Tags**: `#javascript` `#prototipi` `#classi` `#simulazione`
