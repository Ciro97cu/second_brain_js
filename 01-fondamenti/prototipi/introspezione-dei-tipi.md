# [[../../appunti-completi#912-il-riconoscimento-degli-oggetti-introspezione|Introspezione (Controllo dei Tipi)]]

L'introspezione è l'atto di ispezionare un oggetto per capire da chi è stato creato o a chi è collegato, in modo da poter accertarsi di quali funzioni può compiere in totale sicurezza.

## 🎯 Concetti Chiave

- **L'inganno di instanceof**: L'operatore classico in JavaScript si usa sotto l'illusione di verificare se un oggetto derivi da una classe (`a instanceof Foo`). In realtà, controlla goffamente se è collegato all'entità separata `Foo.prototype`. Tra finti costruttori (padri e figli), impone la scrittura di complicate sintassi illegibili.
- **Il rischio del Duck Typing**: Controllare un oggetto solo verificando l'esistenza di un metodo ("se fa quack, è una papera" -> `if (a.metodo)`) è popolare ma pericoloso. Presume ciecamente natura e tipologia di una struttura dati basandosi su banali coincidenze di nomi, scatenando bug silenti.
- **La chiarezza di OLOO**: Togliendo i finti costruttori ereditati, l'introspezione tra semplici oggetti collegati orizzontalmente risulta dritta al punto e pulitissima. Basterà usare direttamente `isPrototypeOf()`.

## 💻 Esempi di Codice

### L'incubo OO vs La semplicità OLOO

```javascript
// ----------- 1. APPROCCIO A CLASSI (Confuso) ----------- //
function Padre() {}
function Figlio() {}
Figlio.prototype = Object.create(Padre.prototype);
var b1 = new Figlio();

// Come chiedere a JS se b1 è imparentato con Padre?
Padre.prototype.isPrototypeOf(b1); // Sintassi pesante e artificiale
Object.getPrototypeOf(b1) === Figlio.prototype; // Scomoda deviazione mentale

// ----------- 2. APPROCCIO OLOO (Puro) ----------- //
var Padre = {};
var Figlio = Object.create(Padre);
var b1 = Object.create(Figlio);

// Limpido all'inverosimile, l'interprete risponde a: "Padre è il delegato di b1?"
Padre.isPrototypeOf(b1); // true
Figlio.isPrototypeOf(b1); // true
Object.getPrototypeOf(b1) === Figlio; // true
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Fidarsi del Duck Typing senza reti**: Basare logiche critiche su un elementare `if (oggetto.salva)` può causare rotture o incidenti di sicurezza se per caso si passa al codice un oggetto sconosciuto che incidentalmente ha un metodo omonimo `salva()` adibito però ad altri scopi e funzionalità interne.
- ❌ **Confondere instanceof con l'ereditarietà netta**: Pensare che `instanceof` indichi una discendenza e un calco diretto (come in altri linguaggi OO tradizionali). In realtà JavaScript interroga solo l'apparato tecnico dei riferimenti ai prototipi.

## 🔗 Collegamenti

**Prerequisiti**:

- [[classi-vs-oggetti]]

**Concetti Correlati**:

- [[architettura-oloo]]
- [[limiti-design-oo]]

## 📚 Riferimenti

- [You Don't Know JS: This & Object Prototypes - Chapter 6](https://github.com/getify/You-Dont-Know-JS)

---

**Tags**: `#javascript` `#prototype` `#typing` `#design` `#oloo`
