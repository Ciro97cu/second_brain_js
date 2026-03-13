# [[../../appunti-completi#accesso-dinamico-alle-proprietà|Accesso Dinamico alle Proprietà]]

La vera potenza della **bracket notation** in JavaScript risiede nella possibilità di determinare il nome della proprietà da accedere (o assegnare) a **runtime**, utilizzando variabili o espressioni.

## Accesso Tramite Variabili

Mentre la dot notation richiede un identificatore letterale fisso, la bracket notation valuta l'espressione all'interno delle parentesi quadre (`[]`).

```javascript
var myObject = {
  a: 2,
  b: 3,
};

var idx = "a";

/* La proprietà viene risolta a runtime */
console.log(myObject[idx]); // 2

/* Con dot notation si cercherebbe la proprietà "idx" */
console.log(myObject.idx); // undefined
```

## Costruzione Dinamica del Nome

È possibile usare qualsiasi espressione valida all'interno delle parentesi, inclusa la concatenazione di stringhe per comporre nomi di proprietà al volo.

```javascript
var prefix = "user_";
var id = 42;

var userData = {
  user_42: { name: "Mario" },
  user_99: { name: "Luigi" },
};

/* Costruzione dinamica con concatenazione */
console.log(userData[prefix + id]); // { name: "Mario" }
```

## Casi d'Uso Comuni

L'accesso dinamico è indispensabile in svariati scenari di programmazione:

### Iterazione sulle Proprietà (Loop)

Quando si passano in rassegna le chiavi di un oggetto, il nome della chiave corrente è contenuto in una variabile ad ogni ciclo, rendendo obbligatoria la bracket notation.

```javascript
var settings = { theme: "dark", language: "it" };
var keys = Object.keys(settings);

keys.forEach(function (key) {
  // 'key' assume i valori "theme", "language" nei vari cicli
  console.log(key + ": " + settings[key]);
});
```

### Dati Esterni e Input Utente

Se la chiave da leggere proviene dall'esterno (es. parametro di una funzione, risposta API, o input dell'utente), il suo nome non è noto a compile-time.

```javascript
var config = { theme: "dark", notifications: true };

function getSetting(settingName) {
  // settingName è dinamico
  return config[settingName];
}

console.log(getSetting("theme")); // "dark"
```

## Alternative in Creazione

Così come la bracket notation consente l'accesso dinamico in lettura/scrittura, la sintassi ES6 dei _computed property names_ (es. `{[nomeDinamico]: valore}`) offre una capacità simile durante le fasi di dichiarazione di un oggetto letterale.

## Collegamenti

- [[dot-vs-bracket-notation]] - Sintassi base tra dot e bracket notation.
- [[computed-property-names]] - Costruzione di chiavi in fase di inizializzazione.
