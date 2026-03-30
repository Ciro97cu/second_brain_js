# [[../../appunti-completi#813-ispezione-delle-relazioni-introspezione|Introspezione e Relazioni Prototipali]]

In JavaScript, per comprendere o tracciare da chi erediti/deleghi un oggetto, esistono strumenti di introspezione. Si possono condurre ispezioni tramite operatori restrittivi o con metodi diretti più puri.

## 🎯 Concetti Chiave

- **L'operatore `instanceof`**: Valuta se il `.prototype` della funzione fornita esista in qualche punto della catena `[[Prototype]]` dell'oggetto. Limite: costringe ad affidarsi sempre ad una funzione tramite classe fittizia.
- **Il metodo `isPrototypeOf()`**: Offre un riscontro per interrogazione identico ad `instanceof`, ma consente lo screening passaggiando unicamente tra due oggetti diretti, senza obbligare all'uso delle signature per costruzione.
- **Dunder Proto (`.__proto__`)**: Storica proprietà _getter/setter_, formalizzata nello standard ES6, allocata in `Object.prototype`, con cui rintracciare ed esplorare manualmente e verticalmente l'iter dei prototipi. Corrisponde nativamente alla funzione standard `Object.getPrototypeOf()`.

## 💻 Esempi di Codice

### Differenze di intromissione e interrogazioni dirette

```javascript
function Foo() {}
const a = new Foo();

// 1. Tramite instanceof (serve mediazione della Funzione costruttrice)
console.log(a instanceof Foo); // true

// 2. Tramite isPrototypeOf (ideale per legami da oggetto a oggetto)
console.log(Foo.prototype.isPrototypeOf(a)); // true

const objPadre = {};
const objFiglio = Object.create(objPadre);
console.log(objPadre.isPrototypeOf(objFiglio)); // true

// 3. Estrapolazione fisica per analisi verticale
console.log(Object.getPrototypeOf(a) === Foo.prototype); // true
console.log(a.__proto__ === Foo.prototype); // true
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Limitazione di `instanceof` nel puro OLOO (Objects Linked to Other Objects)**: Creare codice che interroga deleghe tra oggetti semplici usando `instanceof` restituisce sempre errori di type, in quanto il lato di destra attende imperativamente un riferimento di Function.
- ❌ **Mutare in runtime le deleghe manipolando `.__proto__`**: Assegnare di continuo un valore alla dunder property causa un drastico crollo prestazionale perché impone all'engine interno del runtime di re-mappare tutti gli indici predittivi collegati sulla traccia dell'albero distrutto.

## ✅ Best Practices

- ✓ **Adopera `isPrototypeOf()` o `ES6 getPrototypeOf`**: In architetture disaccoppiate e prive di chiamate costruttrici `new`, affidati solidamente ad un ispezione pulita tra oggetti con `isPrototypeOf()`.
- ✓ **Legami immutabili in runtime**: Mantieni saldo il concetto per cui gli assegnamenti in traccia del prototipo devono essere intesi e letti concettualmente a modo "Sola-Lettura".

## 🔗 Collegamenti

**Prerequisiti**:

- [[ereditarieta-prototipale]]
- [[meccaniche-classi]]

**Concetti Correlati**:

- [[catena-prototipi]]
- [[costruttore]]

**Approfondimenti**:

- [[oggetti]]

## 📚 Riferimenti

- Libro: "You Don't Know JS"
- Capitolo: Prototypes

## 📌 Note Personali

[Spazio per riflessioni, domande, applicazioni personali]

---

**Tags**: `#javascript` `#prototipi` `#introspezione` `#reflection` `#ispezione`
