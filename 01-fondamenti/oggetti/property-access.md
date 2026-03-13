# [[../../../appunti-completi#accesso-alle-proprietà-degli-oggetti|Accesso alle Proprietà (Property Access)]]

JavaScript offre due sintassi per accedere alle proprietà degli oggetti: **dot notation** (`.`) e **bracket notation** (`[]`). La scelta tra le due dipende dalla natura del nome della proprietà e dal contesto di utilizzo.

## Concetti Chiave

- **Dot notation** (`.property`): Sintassi standard, leggibile, limitata a Identifier validi
- **Bracket notation** (`["property"]`): Flessibile, accetta qualsiasi stringa, permette accesso dinamico
- **Property names sono stringhe**: Tutti i nomi vengono convertiti automaticamente in stringhe
- **Accesso dinamico**: La bracket notation permette di costruire nomi a runtime
- **"Contents" è un modello**: I nomi delle proprietà sono riferimenti, non contenitori fisici

## Le Due Sintassi

```javascript
var myObject = {
  a: 2,
};

/* Dot notation (property access) */
myObject.a; // 2

/* Bracket notation (key access) */
myObject["a"]; // 2

/*
 * Entrambe accedono alla stessa posizione
 * e restituiscono lo stesso valore.
 * I termini sono intercambiabili,
 * ma "property access" è più comune.
 */
```

## Dot Notation: Semplicità e Leggibilità

La **dot notation** è la forma preferita quando possibile: concisa, leggibile, standard.

### Requisito: Identifier Validi

L'operatore `.` richiede un nome compatibile con le regole degli **Identifier** JavaScript:

- Inizia con lettera, `_` o `$`
- Contiene solo lettere, numeri, `_` o `$`
- NO spazi, trattini, caratteri speciali

```javascript
var persona = {
  nome: "Mario",
  cognome: "Rossi",
  eta: 30,
  _private: "dato interno",
  $special: "valore speciale",
};

/* ✅ Dot notation - nomi validi */
persona.nome; // "Mario"
persona.cognome; // "Rossi"
persona.eta; // 30
persona._private; // "dato interno"
persona.$special; // "valore speciale"

/* ❌ NON VALIDO con dot notation */
// obj.first-name;      // Syntax Error (trattino)
// obj.user name;       // Syntax Error (spazio)
// obj.123abc;          // Syntax Error (inizia con numero)
```

### Quando Usare Dot Notation

Usa dot notation come **default** quando:

- Il nome è **noto al momento della scrittura** del codice
- È un **Identifier valido**
- Si vuole codice **leggibile e conciso**

```javascript
var config = {
  host: "localhost",
  port: 3000,
  timeout: 5000,
};

/* ✅ Dot notation - chiara e diretta */
console.log(config.host); // "localhost"
console.log(config.port); // 3000
console.log(config.timeout); // 5000
```

## Bracket Notation: Flessibilità e Dinamicità

La **bracket notation** accetta **qualsiasi stringa UTF-8/Unicode** come nome di proprietà.

### Caratteri Speciali

```javascript
var obj = {
  "Super-Fun!": "valore speciale",
  "first-name": "Mario",
  "user name": "mario123",
  123: "numero",
  "😊": "emoji",
};

/* ✅ Bracket notation - accetta qualsiasi stringa */
obj["Super-Fun!"]; // "valore speciale"
obj["first-name"]; // "Mario"
obj["user name"]; // "mario123"
obj["123"]; // "numero"
obj["😊"]; // "emoji"

/* ❌ Impossibili con dot notation */
// obj.Super-Fun!;      // Syntax Error
// obj.first-name;      // Syntax Error
// obj.user name;       // Syntax Error
```

### Accesso Dinamico (Programmabile)

La vera forza della bracket notation: usare **variabili** per determinare quale proprietà accedere a **runtime**.

```javascript
var myObject = {
  a: 2,
  b: 3,
  c: 4,
};

/* Accesso dinamico con variabile */
var idx;

if (wantA) {
  idx = "a";
}

/*
 * La proprietà viene determinata a runtime,
 * non al momento della scrittura del codice
 */
console.log(myObject[idx]); // 2 (se wantA è true)

/* ❌ Con dot notation non funziona */
console.log(myObject.idx); // undefined
/*
 * Cerca letteralmente la proprietà "idx",
 * NON il valore della variabile idx
 */
```

### Costruzione Dinamica del Nome

```javascript
var prefix = "user";
var id = 42;

var userData = {
  user42: { name: "Mario", role: "admin" },
  user99: { name: "Luigi", role: "user" },
};

/* ✅ Costruzione dinamica con concatenazione */
console.log(userData[prefix + id]);
// { name: "Mario", role: "admin" }

/*
 * Il nome viene costruito come stringa:
 * "user" + 42 → "user42"
 */

/* ❌ Impossibile con dot notation */
// userData.prefix + id;  // Syntax Error
```

### Loop su Proprietà

```javascript
var settings = {
  theme: "dark",
  language: "it",
  notifications: true,
};

/* ✅ Iterare dinamicamente su tutte le proprietà */
var keys = Object.keys(settings);

keys.forEach(function (key) {
  console.log(key + ": " + settings[key]);
});

/*
 * Output:
 * theme: dark
 * language: it
 * notifications: true
 */
```

### Input Utente o Dati Esterni

```javascript
/* Scenario: proprietà da input utente */
var config = {
  theme: "dark",
  lang: "it",
  notifications: true,
};

function getSetting(settingName) {
  /*
   * settingName proviene da input,
   * non è noto in anticipo
   */
  return config[settingName];
}

console.log(getSetting("theme")); // "dark"
console.log(getSetting("lang")); // "it"
```

## Quando Usare Quale Sintassi?

### Dot Notation (`.property`)

Usa quando:

1. Nome **noto e fisso** al momento della scrittura
2. **Identifier valido** (no spazi, trattini, caratteri speciali)
3. Si vuole codice **leggibile e conciso**

```javascript
/* ✅ Dot notation - caso standard */
var user = {
  name: "Mario",
  age: 30,
};

console.log(user.name);
console.log(user.age);
```

### Bracket Notation (`["property"]`)

Usa quando:

1. Nome contiene **caratteri speciali** (spazi, trattini, etc.)
2. **Accesso dinamico** (nome da variabile o espressione)
3. **Costruzione runtime** del nome (concatenazione)
4. **Loop su proprietà** (iterazione)
5. **Dati esterni** (API, input utente, configurazioni)

```javascript
/* ✅ Bracket notation - casi speciali */

// 1. Caratteri speciali
obj["first-name"];

// 2. Accesso dinamico
var field = getUserInput();
obj[field];

// 3. Costruzione runtime
obj["user" + id];

// 4. Loop
keys.forEach((k) => console.log(obj[k]));

// 5. Dati da API
var fieldName = api.getFieldName();
obj[fieldName];
```

## Property Names Sono Sempre Stringhe

Un aspetto fondamentale: negli oggetti, **i nomi delle proprietà sono sempre stringhe**, anche se sembrano numeri o altri tipi.

### Coercizione Automatica

Valori **non-stringa** vengono automaticamente **convertiti in stringa**.

```javascript
var myObject = {};

/* Assegnazione con chiavi non-stringa */
myObject[true] = "foo"; // true → "true"
myObject[3] = "bar"; // 3 → "3"
myObject[myObject] = "baz"; // oggetto → "[object Object]"

/* Accesso: le chiavi sono stringhe */
myObject["true"]; // "foo"
myObject["3"]; // "bar"
myObject["[object Object]"]; // "baz"

/*
 * Gli oggetti vengono convertiti con toString(),
 * che di default produce "[object Object]"
 */
```

### Numeri Come Chiavi

Anche i **numeri** (usati comunemente come indici array) sono trattati come stringhe:

```javascript
var arr = ["a", "b", "c"];

/* Indici numerici = stringhe internamente */
arr[0]; // "a"
arr["0"]; // "a" - stesso risultato!

arr[1]; // "b"
arr["1"]; // "b"

/* Verifica: Object.keys restituisce stringhe */
console.log(Object.keys(arr)); // ["0", "1", "2"]
console.log(typeof Object.keys(arr)[0]); // "string"
```

### Array vs Oggetti con Numeri

**ATTENZIONE**: Non confondere numeri come chiavi in **oggetti** vs **indici** in **array**.

```javascript
/* ARRAY: ottimizzato per indici numerici */
var arr = [10, 20, 30];

arr[0]; // 10 - accesso ottimizzato
arr.length; // 3 - gestito automaticamente
arr.push(40); // Metodi specifici per array

/*
 * Il motore sa che è un array e ottimizza
 * l'accesso con indici numerici
 */

/* OGGETTO: numeri convertiti in stringhe, NO ottimizzazione */
var obj = {};
obj[0] = 10;
obj[1] = 20;
obj[2] = 30;

obj[0]; // 10 - funziona ma non ottimizzato
obj.length; // undefined - NO gestione automatica
// obj.push(40);        // TypeError! NO metodo push

/*
 * È un normale oggetto con chiavi "0", "1", "2"
 * NON ha comportamenti speciali di array
 */
```

**Regola**: Per collezioni **ordinate** con **indici numerici**, usa sempre **array**, non oggetti con chiavi numeriche.

```javascript
/* ✅ GIUSTO: Array per sequenze */
var scores = [85, 92, 78];
scores.forEach((score) => console.log(score));
scores.sort();
scores.length; // 3

/* ❌ SBAGLIATO: Oggetto con numeri */
var scores = {};
scores[0] = 85;
scores[1] = 92;
scores[2] = 78;

// scores.forEach(...);  // ❌ TypeError
// scores.sort();        // ❌ TypeError
scores.length; // undefined ❌
```

## Il Modello "Contents" È Impreciso

Si parla di **"contenuti"** dell'oggetto, ma questo è solo un **modello concettuale** semplificato.

### Realtà Tecnica

In realtà:

- Il motore memorizza valori in modi **dipendenti dall'implementazione**
- I valori spesso **non sono "dentro" l'oggetto**
- L'oggetto memorizza **nomi delle proprietà** come **riferimenti** (puntatori) verso dove i valori sono realmente memorizzati

```javascript
var myObject = {
  a: 2,
};

/*
 * Modello concettuale (semplificato):
 * "myObject contiene il valore 2 nella proprietà 'a'"
 *
 * Realtà tecnica (più accurata):
 * "myObject memorizza 'a' come riferimento
 *  che punta al valore 2 memorizzato altrove"
 */
```

Questa distinzione è rilevante per comprendere **riferimenti** in JavaScript:

```javascript
var obj1 = { x: 10 };
var obj2 = obj1; // obj2 contiene riferimento allo stesso oggetto

obj2.x = 20;
console.log(obj1.x); // 20 - Modificato tramite obj2!

/*
 * obj1 e obj2 non "contengono l'oggetto",
 * contengono riferimenti allo stesso oggetto in memoria
 */
```

## Esempio Combinato

```javascript
var config = {
  host: "localhost",
  port: 3000,
  "api-key": "abc123", // Carattere speciale
  timeout: 5000,
};

/* ✅ Dot notation per nomi semplici */
console.log(config.host); // "localhost"
console.log(config.port); // 3000

/* ✅ Bracket notation per carattere speciale */
console.log(config["api-key"]); // "abc123"

/* ✅ Bracket notation per accesso dinamico */
function getConfigValue(key) {
  return config[key];
}

console.log(getConfigValue("timeout")); // 5000

/* ✅ Loop con bracket notation */
var keys = ["host", "port", "timeout"];
keys.forEach(function (key) {
  console.log(key + ": " + config[key]);
});

/*
 * Output:
 * host: localhost
 * port: 3000
 * timeout: 5000
 */
```

## Punti Chiave

1. **Due sintassi**: Dot (`.property`) e bracket (`["property"]`)

2. **Dot notation limitata**: Solo Identifier validi (no spazi/trattini/caratteri speciali)

3. **Bracket notation flessibile**: Qualsiasi stringa UTF-8, accesso dinamico

4. **Preferenza dot notation**: Più leggibile quando possibile

5. **Bracket necessaria per**:
   - Caratteri speciali nel nome
   - Accesso dinamico (nome da variabile)
   - Costruzione nome a runtime
   - Loop su proprietà
   - Dati esterni/input

6. **Property names sempre stringhe**: Conversione automatica per numeri e altri tipi

7. **Array ≠ Oggetto con numeri**: Array ottimizzati per indici, oggetti no

8. **"Contents" è modello**: Nomi sono riferimenti a valori memorizzati altrove

## Collegamenti

- [[oggetti]] - Manipolazione base e proprietà degli oggetti
- [[object-literal-vs-constructed]] - Creazione di oggetti con proprietà
- [[../tipi/valori-tipi]] - Tipi di valori memorizzabili nelle proprietà
- [[../tipi/coercizione]] - Conversione automatica dei nomi in stringhe
- [[../array/array]] - Array come alternativa per sequenze ordinate

#property-access #dot-notation #bracket-notation #dynamic-access #oggetti #identifier
