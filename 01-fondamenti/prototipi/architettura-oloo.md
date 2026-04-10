# [[../../appunti-completi#910-architettura-del-codice-la-semplicit-di-oloo|Architettura OLOO (Objects Linked)]]

Mentre l'istanziazione di codice tramite il formato a Oggetti (Classi `OO`) può appesantire gravemente l'architettura di progetti ampi costringendo l'inserimento arbitrario di logiche di parentela ed ereditarietà fasulla, il design OLOO si presenta come la soluzione logica e limpida per strutturare un software in JavaScript.

Applicando il design **OLOO** (Objects Linked to Other Objects), si smantellano le architetture monoblocco a favore di oggetti semplici ("alla pari" l'uno con l'altro) collegati puramente in cascata da `Object.create()`.

## 🎯 Concetti Chiave

- **Semplificazione dei Collegamenti**: Non serve creare tre finte "Classi Elemento" (es. Classe Gedeone, Classe Padre, Classe Figlia). Bastano due semplici e banali oggetti collegati logicamente e orizzontalmente in modo da passarsi le informazioni.
- **Assenza di Composizione Forzata**: Per farsi parlare due oggetti non devono possedersi "passandosi" referenze da una Classe all'altra in `this`. Basta creare una comune delega pura in modo che l'uno assista l'altro in base alla necessità e senza vincoli ferrei parentali.
- **Denominazioni Uniche e Libere da Overrides**: In stile Classe il `success()` figlio sovrascrive malamente il `success()` padre obbligandoci a trucchi osceni. Nel OLOO chiameremo semanticamente `accepted()` nell'oggetto A e richiameremo `success()` dell'oggetto delegato base B senza fatica e senza confusioni, garantendone la limpida tracciabilità a vista d'occhio.

## 💻 Esempi di Codice

### Costruire Entità Paritetiche ed Indipendenti

```javascript
var ModuloWeb = {
  controllaScrittura: function () {
    /* ... */
  },
  mostraSuccesso: function () {
    /* ... */
  },
};

// Nessun super() o extend(): è puramente un Object legato logicamente al primo:
var AutenticazioneServer = Object.create(ModuloWeb);

AutenticazioneServer.accettato = function () {
  // Richiama senza "trucchi di istanziazione padre" la funzione dell'oggetto compagno!
  this.mostraSuccesso("Tutto Apposto!");
};

// ... Innesco Immediato ...
// Nessun bisogno di faticare richiamando complessi new Componente(...this)
AutenticazioneServer.accettato();
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Creare ereditarietà per comportamenti comuni**: Creare enormi super-classi solamente perché svariati oggetti hanno 2-3 funzioni identiche. Meglio collegarli in delega piuttosto che costringerli in un vincolo parentale in JavaScript.
- ❌ **Costruire Overriding Scomodi**: Sovrascrivere nomi identici `render()` in oggetti padri/figli fa saltare all'occhio quanto poi sia faticoso specificare quale dei due stai chiamando tramite `Padre.render.call()`. Basta scegliere nomi unici descrittivi!

## ✅ Best Practices

- ✓ Mantenere gli oggetti delegati "piatti", affiancandoli orizzontalmente e non strutturandoli quasi mai come immense ramificazioni top-down.

## 🔗 Collegamenti

**Prerequisiti**:

- [[classi-vs-oggetti]]
- [[limiti-design-oo]] (problema strutturale pre-OLOO)

**Correlati**:

- [[delegazione-widget-ui]] (applicazione OLOO ai pannelli web)

## 📚 Riferimenti

- Libro: _You Don't Know JS - This & Object Prototypes_

---

**Tags**: `#javascript` `#struttura` `#oop` `#design` `#oloo`
