# [[../../appunti-completi#sintassi-degli-oggetti|Oggetti: Forma Costruita]]

Tra i modi per creare oggetti in JavaScript, la **forma costruita** (constructed form) utilizza l'invocazione di costruttori come `new Object()` associata ad assegnazioni incrementali di singole proprietà.

## Sintassi e Introduzione

Essa affonda le sue radici nei paradigmi di programmazione classici orientati agli oggetti, ma si differenzia molto per prolissità nel linguaggio.

```javascript
/* FORMA COSTRUITA */
// Creazione iterativa in più passaggi
let personaCostruita = new Object();
personaCostruita.nome = "Mario";
personaCostruita.cognome = "Rossi";
personaCostruita.eta = 30;
personaCostruita.saluta = function () {
  console.log(`Ciao, sono ${this.nome}`);
};

// typeof personaCostruita -> "object"
```

## Strutturare con new Object()

Utilizzare il costruttore base e appendere le proprietà allunga la struttura logica del programma. Il risultato computato alla fine è identico a livello di architettura ai **letterali** (`{}`).

```javascript
let configCostruita = new Object();
configCostruita.host = "localhost";
configCostruita.port = 3000;
configCostruita.timeout = 5000;
```

A differenza di una dichiarazione immediata, questo pattern sfavorisce la lettura contestuale. Rintracciare le singole operazioni nel codice richiede la scansione di diverse chiamate e l'uso prolungato della _dot-notation_ o _bracket-notation_ su singole variabili, frammentando le definizioni dell'oggetto.

## Quando Usare la Forma Costruita?

È opinione comune e accertata che l'uso della forma costruita andrebbe evitato come tecnica di instanziazione di default, favorendo le [[object-literals|forme letterali]].

La forma costruita conserva tuttavia alcuni pregi, solitamente molto settoriali.

### Costruzione Condizionale

Si può decidere quali proprietà applicare a un oggetto durante il runtime basandosi su una logica condizionale astratta:

```javascript
function creaConfigurazione(ambiente) {
  let config = new Object(); // Base vuota

  // Logica complessa separata in blocchi
  if (ambiente === "produzione") {
    config.host = "api.example.com";
    config.ssl = true;
  } else if (ambiente === "staging") {
    config.host = "staging.example.com";
    config.ssl = true;
  } else {
    config.host = "localhost";
    config.ssl = false;
  }

  return config;
}
```

Ma anche le alternative tramite logica condizionale a livello di struttura dati spesso risolvono queste sfide in modo più pulito.

### Aggiunta Incrementale per Finalità Didattiche

Il frazionamento forzato della dichiarazione viene scelto in contesti in cui risulta necessario focalizzare l'attenzione dello sviluppatore sulla modifica dinamica progressiva (es. pattern builder in fase di studio).

```javascript
let profilo = new Object();
console.log("1. Profilo vuoto:", profilo); // {}
profilo.username = "utente_01";
console.log("2. Con username:", profilo); // { username: "..." }
```

In definitiva, nella programmazione moderna l'utilizzo esplicito della forma a costruttore standard `new Object()` è quasi assente e considerata un'istruzione deprecabile per l'instanziazione base di routine.

## Collegamenti

- [[object-literal-vs-constructed]] - Confronto e linee guida per la creazione
- [[object-literals]] - Utilizzo di forma letterale
- [[oggetti]] - Funzionamento base degli oggetti in JS
