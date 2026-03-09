# Oggetti: Forma Letterale vs Forma Costruita

Esistono due modi principali per creare oggetti in JavaScript: la **forma letterale** (object literal) e la **forma costruita** (constructed form). La scelta tra le due ha implicazioni su leggibilità, praticità e prestazioni.

## Concetti Chiave

- **Forma letterale**: Sintassi dichiarativa `{ key: value }` che crea l'oggetto in un'unica espressione
- **Forma costruita**: Utilizzo di `new Object()` seguito da assegnazioni incrementali di proprietà
- **Risultato identico**: Entrambe producono lo stesso tipo di oggetto, ma differiscono nell'approccio
- **Best practice**: Preferire quasi sempre la forma letterale per semplicità e leggibilità

## Le Due Forme a Confronto

```javascript
/* FORMA LETTERALE (Raccomandata) */
// Tutto in un'unica espressione, chiara e concisa
let persona = {
  nome: "Mario",
  cognome: "Rossi",
  eta: 30,
  saluta: function () {
    console.log(`Ciao, sono ${this.nome}`);
  },
};

/* FORMA COSTRUITA (Rara) */
// Creazione in più passaggi, più verbosa
let personaCostruita = new Object();
personaCostruita.nome = "Mario";
personaCostruita.cognome = "Rossi";
personaCostruita.eta = 30;
personaCostruita.saluta = function () {
  console.log(`Ciao, sono ${this.nome}`);
};

/* Risultato identico */
console.log(typeof persona); // "object"
console.log(typeof personaCostruita); // "object"
console.log(persona.nome); // "Mario"
console.log(personaCostruita.nome); // "Mario"
```

## Perché Preferire la Forma Letterale?

### 1. Leggibilità e Concisione

La forma letterale mostra immediatamente la struttura completa dell'oggetto:

```javascript
// ✅ Chiaro: vedo subito tutte le proprietà
let config = {
  host: "localhost",
  port: 3000,
  timeout: 5000,
};

// ❌ Dispersivo: devo leggere più righe per capire la struttura
let configCostruita = new Object();
configCostruita.host = "localhost";
configCostruita.port = 3000;
configCostruita.timeout = 5000;
```

### 2. Meno Codice da Scrivere

La forma letterale elimina la ripetizione del nome della variabile:

```javascript
// ✅ 3 righe totali
let libro = {
  titolo: "1984",
  autore: "George Orwell",
};

// ❌ 4 righe per lo stesso risultato
let libroCostruito = new Object();
libroCostruito.titolo = "1984";
libroCostruito.autore = "George Orwell";
```

### 3. Coerenza con JSON

La sintassi letterale è praticamente identica a JSON (JavaScript Object Notation), facilitando il lavoro con dati serializzati:

```javascript
// ✅ Facile da convertire da/verso JSON
let datiUtente = {
  id: 123,
  username: "mario_rossi",
  attivo: true,
};

let json = JSON.stringify(datiUtente);
let parsed = JSON.parse(json); // Ottieni di nuovo un object literal
```

### 4. Supporta Proprietà Calcolate (ES6+)

La forma letterale permette chiavi dinamiche direttamente nella definizione:

```javascript
// ✅ Proprietà calcolata inline
let campo = "categoria";
let prodotto = {
  nome: "Laptop",
  [campo]: "Elettronica", // categoria: "Elettronica"
  [campo + "ID"]: "ELEC-001", // categoriaID: "ELEC-001"
};

// ❌ Con forma costruita serve bracket notation separata
let prodottoCostruito = new Object();
prodottoCostruito.nome = "Laptop";
prodottoCostruito[campo] = "Elettronica";
prodottoCostruito[campo + "ID"] = "ELEC-001";
```

## Quando Usare la Forma Costruita?

La forma costruita è utile in casi **molto rari**, tipicamente quando:

### 1. Costruzione Condizionale Complessa

Quando la struttura dell'oggetto dipende da logica runtime articolata:

```javascript
function creaConfigurazione(ambiente) {
  // Oggetto base vuoto
  let config = new Object();

  // Logica condizionale complessa
  if (ambiente === "produzione") {
    config.host = "api.example.com";
    config.ssl = true;
    config.timeout = 10000;
  } else if (ambiente === "staging") {
    config.host = "staging.example.com";
    config.ssl = true;
    config.timeout = 5000;
    config.debug = false;
  } else {
    config.host = "localhost";
    config.ssl = false;
    config.timeout = 3000;
    config.debug = true;
    config.verbose = true;
  }

  return config;
}

/*
 * Nota: Anche questo caso si risolve meglio con la forma letterale:
 */
function creaConfigMigliore(ambiente) {
  const configs = {
    produzione: { host: "api.example.com", ssl: true, timeout: 10000 },
    staging: {
      host: "staging.example.com",
      ssl: true,
      timeout: 5000,
      debug: false,
    },
    default: {
      host: "localhost",
      ssl: false,
      timeout: 3000,
      debug: true,
      verbose: true,
    },
  };

  return configs[ambiente] || configs.default;
}
```

### 2. Aggiunta Incrementale per Chiarezza

Quando si vuole evidenziare il processo di costruzione passo-passo (raro, più didattico):

```javascript
// Scenario: simulare costruzione di un profilo utente passo-passo
let profilo = new Object();

console.log("1. Creo profilo vuoto:", profilo); // {}

profilo.username = leggiInput();
console.log("2. Aggiungo username:", profilo); // { username: "..." }

profilo.email = validaEmail();
console.log("3. Aggiungo email:", profilo); // { username: "...", email: "..." }

profilo.ruolo = "utente";
console.log("4. Assegno ruolo:", profilo); // { username: "...", email: "...", ruolo: "utente" }
```

## Prestazioni

Entrambe le forme hanno prestazioni equivalenti nei motori JavaScript moderni. La forma letterale **non è più lenta** e in alcuni casi può essere leggermente ottimizzata meglio dal compilatore perché la struttura è nota immediatamente.

```javascript
// Benchmark concettuale (risultati simili)
console.time("literal");
for (let i = 0; i < 100000; i++) {
  let obj = { x: 1, y: 2, z: 3 };
}
console.timeEnd("literal"); // ~10ms

console.time("constructed");
for (let i = 0; i < 100000; i++) {
  let obj = new Object();
  obj.x = 1;
  obj.y = 2;
  obj.z = 3;
}
console.timeEnd("constructed"); // ~11ms (trascurabile)
```

## Linee Guida Pratiche

| Scenario                                        | Forma Raccomandata | Motivo                                   |
| ----------------------------------------------- | ------------------ | ---------------------------------------- |
| Oggetto con struttura nota                      | **Letterale**      | Leggibilità, concisione                  |
| Oggetto da JSON                                 | **Letterale**      | Compatibilità con JSON.parse()           |
| Oggetto con proprietà calcolate                 | **Letterale**      | Supporto inline per chiavi dinamiche     |
| Configurazione, opzioni, dati                   | **Letterale**      | Standard de facto                        |
| Costruzione condizionale molto complessa        | Costruita          | Chiarezza logica (ma raramente migliore) |
| Esempio didattico per mostrare fasi di crescita | Costruita          | Evidenzia processo incrementale          |

## Punti Chiave

1. **Preferire sempre la forma letterale** salvo casi eccezionali con logica molto complessa

2. **Risultato identico**: Entrambe creano lo stesso tipo di oggetto con stesse capacità

3. **Forma letterale più moderna**: Supporta sintassi ES6+ (proprietà calcolate, shorthand, spread)

4. **Prestazioni equivalenti**: Nessun overhead significativo in nessuna delle due forme

5. **Coerenza codebase**: La forma letterale è lo standard nelle codebase moderne

6. **Se in dubbio**: Usa la forma letterale. Quasi nessuno usa `new Object()` nel codice moderno

## Collegamenti

- [[oggetti]] - Manipolazione e accesso alle proprietà degli oggetti
- [[../tipi/tipi-e-sottotipi]] - Object come tipo fondamentale del sistema
- [[../tipi/typeof]] - Come verificare che un valore sia di tipo object
- [[prototypes]] - Sistema di ereditarietà prototipale degli oggetti

#oggetti #sintassi #best-practices #literal-form #constructed-form #object-creation
