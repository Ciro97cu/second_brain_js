# [[../../appunti-completi#sintassi-degli-oggetti|Oggetti: Forma Letterale]]

La **forma letterale** (object literal) è il metodo principale e consigliato per creare oggetti in JavaScript. Rappresenta una sintassi dichiarativa che permette di definire chiavi e valori all'interno di un'unica struttura delimitata da parentesi graffe `{}`.

```javascript
/* FORMA LETTERALE */
let persona = {
  nome: "Mario",
  cognome: "Rossi",
  eta: 30,
  saluta: function () {
    console.log(`Ciao, sono ${this.nome}`);
  }
};
```

## Vantaggi della Forma Letterale

La forma letterale è considerata la best practice assoluta per la definizione degli oggetti rispetto alla [[constructed-objects|forma costruita]], per via di notevoli vantaggi in termini di leggibilità e sintassi.

### 1. Leggibilità e Concisione

La forma letterale mostra immediatamente la struttura gerarchica dell'intero oggetto. È possibile riscontrare a colpo d'occhio tutte le proprietà definite nella struttura, migliorandone lo studio e la manutenibilità.

```javascript
// Struttura immediatamente chiara
let config = {
  host: "localhost",
  port: 3000,
  timeout: 5000
};
```

Questo paradigma riduce la quantità di codice necessaria, eliminando la ripetizione dell'identificatore principale durante l'assegnazione.

### 2. Coerenza con JSON

Questa sintassi è alla base del formato **JSON** (JavaScript Object Notation), rendendo naturale e fluido lo sviluppo con applicazioni orientate ai dati elaborati dalle REST API.

```javascript
let datiUtente = { id: 123, username: "mario_rossi", attivo: true };

// Parsing e conversione ritornano o accettano strutture letterali
let json = JSON.stringify(datiUtente);
let parsed = JSON.parse(json); 
```

### 3. Supporto a Proprietà Calcolate (Computed Properties)

La forma letterale implementa l'assegnazione nativa di chiavi dinamiche direttamente in fase di dichiarazione, usando l'espressione in parentesi quadre (`[ ]`).

```javascript
let campo = "categoria";
let prodotto = {
  nome: "Laptop",
  [campo]: "Elettronica",      // Inserisce 'categoria'
  [campo + "ID"]: "ELEC-001"   // Inserisce 'categoriaID'
};
```

## Prestazioni

Nei motori JavaScript moderni, l'inizializzazione letterale beneficia di ottimizzazioni avanzate. Il compilatore conosce da subito l'allocazione esatta dell'oggetto, portando le prestazioni a un livello pari o superiore rispetto all'aggiunta successiva di proprietà, consolidando questa sintassi come lo standard industriale dell'ecosistema JavaScript.

## Collegamenti

- [[object-literal-vs-constructed]] - Confronto complessivo 
- [[constructed-objects]] - La creazione tramite forma costruita
- [[oggetti]] - Maniplazione di base delle proprietà
