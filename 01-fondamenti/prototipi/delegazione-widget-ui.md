# Delegazione e Widget UI (OLOO in pratica)

## Implementare un'interfaccia utente in JavaScript

Quando si progettano elementi dell'interfaccia utente, come dei semplici bottoni su schermo, si nota spesso la complessità dell'approccio basato sulle finte classi in JavaScript.

In un approccio **Orientato agli Oggetti (OO)** classico, si crea una "classe padre" (`Widget`) per il comportamento base e una "classe figlia" (`Button`) per lo specifico bottone. 

### I difetti dell'approccio classico (Pre-ES6 e ES6)

1. **Pre-ES6:** Il programmatore era costretto a pseudo-ereditare manualmente tramite ingombranti chiamate come `Widget.call(this)` e usare esplicitamente `Widget.prototype.render.call` per accedere ai metodi della classe base.
2. **Con ES6:** La nuova sintassi `class` e `super` ha nascosto questi problemi sotto uno zucchero sintattico. Sembra tutto più elegante, ma JavaScript non possiede vere classi: si basa ancora sui prototipi sotto il cofano. Creando l'illusione delle classi, il codice è esposto a bug quando ci si dimentica della reale natura delegata degli oggetti.

## Un Caso Pratico con OLOO (Objects Linked to Other Objects)

La soluzione naturale studiata dal linguaggio per risolvere l'esempio dei bottoni è la **delega pura tra oggetti**, ovvero il pattern **OLOO**.

In questo modello non esistono più classi astratte, concetti come ereditarietà, costruttori obbligati `new` o catene di pseudo-discendenza; si impiega la semplice creazione di oggetti che delegano tra loro.

### Esempio in Codice

```javascript
// Oggetto Base JS: Widget puro 
var Widget = {
  init: function (width, height) {
    this.width = width || 50;
    this.height = height || 50;
    this.$elem = null;
  },
  insert: function ($where) {
    if (this.$elem) {
      this.$elem.css({ width: this.width + "px", height: this.height + "px" }).appendTo($where);
    }
  },
};

// Nessuna classe o esplicitazione parentale: si crea 'Button' collegato a 'Widget'
var Button = Object.create(Widget);

Button.setup = function (width, height, label) {
  // Delega di comodo all'init di Widget 
  this.init(width, height);
  this.label = label || "Default";
  this.$elem = $("<button>").text(this.label);
};

Button.build = function ($where) {
  // Delega di comodo all'insert di Widget 
  this.insert($where);
  this.$elem.click(this.onClick.bind(this));
};

Button.onClick = function (evt) {
  console.log("Cliccato '" + this.label + "'!");
};

// Implementazione distaccata
$(document).ready(function () {
  var $body = $(document.body);

  // Fase 1: pura Creazione Oggetto
  var btn1 = Object.create(Button);
  
  // Fase 2: Configurazione Oggetto
  btn1.setup(125, 30, "Hello");
  btn1.build($body);
});
```

### Quali sono i benefici pratici dell'adozione dell'OLOO?

1. **Parità Estrema:** Nessun oggetto domina l'altro sotto logiche di classe. `Widget` sa come comportarsi in via generale e `Button`, se non sa cosa fare in quel momento, gli rivolge autonomamente la chiamata delegata.
2. **Nomi Chiari ed Evitati i Conflitti (No Shadowing):** Evitando la tentazione di usare sempre nomi generici e clonati (es. `render`), ci si affranca dai trucchi dei richiami. Definendo la creazione di `Widget` in `insert()` e quella di `Button` come `build()`, lo sviluppatore percepisce immediatamente la specificità logica del codice.
3. **Meno sintassi ingombrante:** Sparisce tutto l'accumulo di `new`, `prototype` e vari trucchi della `class`. E' solo codice nativo che rispecchia i pattern d'origine.
4. **Dividere Istanziazione e Configurazione:** Usare un normale stile `new Button` obbliga il settaggio e la creazione dei contenuti base ad occorrere nel medesimo istante. Usando l'OLOO, questa restrizione strutturale decade: la funzione base preparatoria `Object.create(Button)` si può richiamare quando si vuole, posticipando con scioltezza il momento del versamento dei parametri tramite `.setup(125, 30)` ore dopo (quando magari il server ha risposto col dato).
