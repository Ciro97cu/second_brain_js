# [[../../appunti-completi#93-la-teoria-della-delegazione-e-il-pattern-oloo|Pattern OLOO (Objects Linked to Other Objects)]]

Il pattern OLOO sfrutta i prototipi nativi di JavaScript per creare architetture basate sulla **Behavior Delegation** (Delegazione del Comportamento). Invece di astrarre comportamenti in "classi base" da cui ereditare verticalmente, si creano singoli oggetti "alla pari" (peers) che si fanno carico di delegare utilità tra loro mediante un collegamento bidirezionale impostato con `Object.create()`.

## 🎯 Concetti Chiave

- **Sviluppo Orizzontale**: L'architettura non prevede genitori astratti né gerarchie di dominazione direzionale. Si concepiscono normali oggetti fratelli posizionati affiancati l'uno all'altro pronti a fornire o richiedere calcoli (Delegatori vs Delegati).
- **Stato sui Delegatori (Riceventi)**: I dati dello stato dell'applicazione appartengono e restano strettamente ancorati sull'oggetto ricevente di testa (il delegatore). Le utilità globali delegabili in coda offrono solo funzioni generaliste in risposta senza accavallare dati.
- **Evitare il Polimorfismo**: Nello sviluppo classico a classi si punta allo _Shadowing_ per "overridare" metodi col medesimo nome tra genitore e figlio. In OLOO si attribuiscono appositamente etichette diverse e descrittive ad ogni strato per scampare l'ambiguità logica ed unificare la catena visuale.

## 💻 Esempi di Codice

### Costrutto Architetturale a Singoli Oggetti

```javascript
// 1) L'oggetto Delegato offre le funzioni basilari ed è privo di costruttori
const Utility = {
  setName: function (name) {
    this.name = name;
  },
};

// 2) L'Oggetto Delegatore lo si collega a utilità.
// Da questo momento lui "sa" e "impara" a dirottare ai metodi in catena.
const UserEntity = Object.create(Utility);

// 3) L'etichettatura logica predilige non andare in Override con "setName" ma essere Specifica
UserEntity.prepareUser = function (userName) {
  // Avviata sull'Entity ma processata a monte col legame This solido
  this.setName(userName);
};
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Delegazione Multipla Interdetta**: In JavaScript l'engine non tollera i circoli d'influenza chiusi ($A \leftrightarrow B$). Passargli una delegazione reciproca a maglia finita farà collassare esplicitamente lo step in log-error. Solo una mappa rettilinea e ramificata è permessa.
- ❌ **Fissazione sui nomi in Console**: Ispezionando gli oggetti nei DevTools del browser, non vedrai più nomi come `UserEntity {}`, ma solo anonimi `Object {}`. Non cercare di ricreare le etichette con codice intricato: nel pattern OLOO conta solo verso "chi" deleghi i comportamenti, non il "nome della funzione" che ha creato l'oggetto.

## ✅ Best Practices

- ✓ **Self-Documenting Code**: Rinominare le proprietà delle utilities per differenziarsi al massimo dal trigger di delega. Anziché riutilizzare globalmente `login() / login() / login()`, è raccomandabile separarne la genesi con una sequenza logica come `doLoginContext() / initDefaultLog()`.

## 🔗 Collegamenti

**Prerequisiti** (concetti da conoscere prima):

- [[behavior-delegation]]
- [[object-links]]

**Concetti Correlati**:

- [[lidentificatore-this]]
- [[shadowing]]

## 📚 Riferimenti

- _You Don't Know JS_ - Cap. 6 (Behavior Delegation)

---

**Tags**: `#javascript` `#prototipi` `#design-pattern` `#delegazione` `#oloo`
