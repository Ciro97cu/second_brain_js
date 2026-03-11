# Nomi di Proprietà Computati (Computed Property Names)

I **nomi di proprietà computati** (Computed Property Names) consentono di specificare dinamicamente i nomi delle proprietà direttamente durante la dichiarazione di un oggetto letterale (object-literal), valutando un'espressione a runtime. Sono stati introdotti con ES6.

## Concetti Chiave

- **Sintassi**: Utilizzano le parentesi quadre `[ ]` contenenti un'espressione nella posizione del nome chiave (es. `[expr]: valore`).
- **Accesso vs Dichiarazione**: Simili concettualmente all'accesso tramite [bracket notation](property-access.md), ma applicati nella fase di _dichiarazione_.
- **Addio workaround prefissati**: Permettono di superare la pre-esistente limitazione dell'object-literal, che imponeva l'uso di assegnazioni sequenziali per i nomi di chiave da comporre programmaticamente.
- **Supporto Symbol**: È il metodo primario per includere i `Symbol` all'interno della forma letterale.

## Utilizzo e Vantaggi Sintattici

La sintassi si serve di un blocco valutabile racchiuso tra parentesi quadre quadre (`[ ]`) usato laddove tipicamente siede una stringa predeterminata o un identifier. L'espressione lì racchiusa viene elaborata a runtime in una stringa che diverrà il reale nome della proprietà:

```javascript
var prefix = "foo";

/*
 * Dichiarazione coerente e concisa
 * grazie ai Computed Property Names
 */
var myObject = {
  [prefix + "bar"]: "hello", // Valutata dinamicamente come "foobar"
  [prefix + "baz"]: "world", // Valutata dinamicamente come "foobaz"
};

myObject["foobar"]; // "hello"
myObject.foobaz; // "world" (se l'identificatore generato è valido, come lo è per 'foobaz', si può usare dot-notation)
```

## Il Confronto con l'Approccio Pre-ES6

Prima dell'introduzione in ES6 di questo meccanismo, se occorreva usare chiavi di struttura variabile, era obbligatorio staccarsi dalla stesura dell'object-literal:

```javascript
/*
 * APPROCCIO PRE-ES6
 */
var userType = "admin";
var userId = 405;

var accessTable = {
  active: true,
  // Impossibile determinare nomi dinamicamente in questo blocco
};

// Bisognava affidarsi as assegnazioni in bracket separatamente
accessTable[userType + "_" + userId] = "Full Access";
```

Con le _computed properties_ è supportata una definizione nativa condensata, la quale rende il blocco letterale decisamente più compatto e descrittivo.

```javascript
/*
 * APPROCCIO ES6 E SUCCESSIVI
 */
var userType = "admin";
var userId = 405;

var accessTable = {
  active: true,
  [userType + "_" + userId]: "Full Access", // Direttamente nella dichiarazione!
};
```

## L'impiego per gestire i Symbol

Il più comune pattern d'uso dei _computed property names_ incontra un'altra "novità" (da ES6) di sistema, i primitivi **Symbols**.

I _Symbols_ sono impiegati per erigere identificatori rigorosamente univoci. Dal momento che il loro valore reale di stringa è ritenuto "opaco", insondabile e tecnicamente persino variabile a fronte di implementazioni diverse dei motori di JavaScript, operare col la stringa interna del _Symbol_ è precluso o sconsigliato. Ci si interfaccia con il nome astratto del parametro tenente la referenza.

In questa evenienza, la sintassi _computed_ fornisce esattamente il legante per appiccicarli in un oject-literal:

```javascript
var myConstant = Symbol.for("chiave_segreta");
var uniqueProperty = Symbol("speciale");

/*
 * Senza le parentesi graffe, assegneremmo
 * la proprietà fisicale di nome stringa "uniqueProperty"
 */
var dataLayer = {
  defaultName: "Base Layer",
  [myConstant]: "Valore configurazione",
  [uniqueProperty]: [1, 2, 3],
};

console.log(dataLayer[myConstant]); // "Valore configurazione"
console.log(dataLayer[uniqueProperty][0]); // 1
```

## Collegamenti

- [[property-access]] - Bracket e dot notation per l'accesso e l'assegnazione alle chiavi
- [[object-literal-vs-constructed]] - Modalità di stesura dell'object-literal format
- [[../tipi/valori-tipi]] - Approfondimenti riguardanti i formati primitivi (es. Symbols)

#es6 #computed-properties #object-literal #sintassi #oggetti
