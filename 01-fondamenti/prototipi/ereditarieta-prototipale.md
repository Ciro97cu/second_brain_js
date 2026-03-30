# [[../../appunti-completi#812-ereditarieta-prototipale|Ereditarietà Prototipale]]

In JavaScript non esiste una vera e propria ereditarietà basata sulla copia tipica delle classi "genitore-figlio". Essa viene invece simulata tramite un sistema di delega comportamentale in cui l'oggetto `.prototype` di una funzione viene collegato gerarchicamente al `.prototype` di un'altra.

## 🎯 Concetti Chiave

- **Delega gerarchica**: I metodi non vengono trascritti e duplicati nelle "sottoclassi". Si stabilisce piuttosto un collegamento invisibile `[[Prototype]]` perché le chiamate mancanti vengano reindirizzate al livello superiore.
- **Creazione del collegamento (Pre-ES6)**: Viene classicamente usato `Object.create(MioPadre.prototype)`. Genera un nuovo oggetto vuoto e delega al genitore richiesto, gettando via l'originario prototipo isolato.
- **Modifica del collegamento (ES6+)**: `Object.setPrototypeOf(MioFiglio.prototype, MioPadre.prototype)` assegna il link al genitore senza forzare la creazione e distruzione di un intero oggetto.

## 💻 Esempi di Codice

### Aggancio tramite Object.create()

```javascript
function Foo(name) {
  this.name = name;
}
Foo.prototype.myName = function () {
  return this.name;
};

function Bar(name, label) {
  Foo.call(this, name);
  this.label = label;
}

// Scarta il vecchio Bar.prototype e lo collega propriamente a Foo.prototype
Bar.prototype = Object.create(Foo.prototype);

Bar.prototype.myLabel = function () {
  return this.label;
};

const b = new Bar("b", "oggetto b");
console.log(b.myName()); // Ereditato
console.log(b.myLabel()); // Metodo proprio
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Condivisione della referenza originaria `Figlio.prototype = Padre.prototype;`**: Non crea un nuovo strato ma clona l'indirizzo. Aggiungendo un metodo al `Figlio`, esso verrà irrimediabilmente iniettato e inquinato per chiunque sia legato al `Padre`.
- ❌ **Collegamento via costruttore `Figlio.prototype = new Padre();`**: Realizza il legame ma evoca gli eventuali log o alterazioni di stato codificati nel costruttore `Padre` fuori contesto e prematuramente.

## ✅ Best Practices

- ✓ **Usa `setPrototypeOf` oppure `Object.create`**: Preferisci `Object.setPrototypeOf` in codice moderno per mantenere efficiente la manipolazione. Usa `Object.create` ove occorra un ripristino intero e cross-browser sicuro pre-ES6.

## 🔗 Collegamenti

**Prerequisiti**:

- [[costruttore]]
- [[meccaniche-classi]]

**Concetti Correlati**:

- [[inaffidabilita-constructor]]
- [[ereditarieta]]

**Approfondimenti**:

- [[catena-prototipi]]

## 📚 Riferimenti

- Libro: "You Don't Know JS"
- Capitolo: Prototypes

## 📌 Note Personali

[Spazio per riflessioni, domande, applicazioni personali]

---

**Tags**: `#javascript` `#prototipi` `#ereditarietà` `#selezione`
