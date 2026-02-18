# [[../../appunti-completi#27-switch|Switch]]

Quando si ha la necessità di confrontare una singola variabile o espressione con una serie di valori specifici, una lunga catena di `if...else if` può diventare verbosa.

In questi scenari, l'istruzione **switch** offre un'alternativa più pulita e strutturata. La sua logica è: **"valuta questa espressione e, in base al suo valore, esegui il blocco di codice corrispondente"**.

## Sintassi Base

```javascript
/*
 * Struttura dello switch
 */

switch (espressione) {
  case valore1:
    // codice eseguito se espressione === valore1
    break;
  case valore2:
    // codice eseguito se espressione === valore2
    break;
  case valore3:
    // codice eseguito se espressione === valore3
    break;
  default:
  // codice eseguito se nessun case corrisponde
}
```

La struttura si basa su:

- **`case`** → Un'etichetta che rappresenta un possibile valore per l'espressione
- **`break`** → Un'istruzione che interrompe l'esecuzione dello switch (fondamentale!)
- **`default`** → Un caso opzionale eseguito se nessun `case` corrisponde

## Esempio Pratico

```javascript
/*
 * Switch per giorni della settimana
 */

let giorno = "Lunedì";

switch (giorno) {
  case "Lunedì":
    console.log("Inizio settimana");
    break;
  case "Mercoledì":
    console.log("Metà settimana");
    break;
  case "Venerdì":
    console.log("Quasi weekend!");
    break;
  case "Sabato":
  case "Domenica":
    console.log("È il weekend!");
    break;
  default:
    console.log("Un giorno normale");
}

// Output: "Inizio settimana"
```

## Confronto con if...else if

**Usando if...else if**:

```javascript
/*
 * Approccio con if...else if
 */

let colore = "rosso";

if (colore === "rosso") {
  console.log("Stop");
} else if (colore === "giallo") {
  console.log("Rallenta");
} else if (colore === "verde") {
  console.log("Vai");
} else {
  console.log("Colore non valido");
}
```

**Usando switch** (più pulito per confronti di uguaglianza):

```javascript
/*
 * Approccio con switch
 */

let colore = "rosso";

switch (colore) {
  case "rosso":
    console.log("Stop");
    break;
  case "giallo":
    console.log("Rallenta");
    break;
  case "verde":
    console.log("Vai");
    break;
  default:
    console.log("Colore non valido");
}
```

## L'Importanza del break

Il **`break`** è fondamentale per evitare il **fall through** (caduta) nel caso successivo.

```javascript
/*
 * Senza break - Fall Through (comportamento pericoloso)
 */

let numero = 1;

switch (numero) {
  case 1:
    console.log("Uno"); // ✅ Eseguito
  // MANCA break!
  case 2:
    console.log("Due"); // ⚠️ Eseguito anche se numero !== 2
  // MANCA break!
  case 3:
    console.log("Tre"); // ⚠️ Eseguito anche se numero !== 3
    break;
  default:
    console.log("Altro");
}

// Output:
// "Uno"
// "Due"
// "Tre"
```

**Con break** (comportamento corretto):

```javascript
/*
 * Con break - Comportamento normale
 */

let numero = 1;

switch (numero) {
  case 1:
    console.log("Uno"); // ✅ Eseguito
    break; // ✅ Esce dallo switch
  case 2:
    console.log("Due"); // ❌ NON eseguito
    break;
  case 3:
    console.log("Tre"); // ❌ NON eseguito
    break;
  default:
    console.log("Altro");
}

// Output: "Uno"
```

## Raggruppare i case

Una caratteristica utile dello switch è la possibilità di **raggruppare più case** per eseguire lo stesso blocco di codice, omettendo deliberatamente il `break`.

```javascript
/*
 * Raggruppamento case - Fall Through Intenzionale
 */

let giorno = "Sabato";

switch (giorno) {
  case "Lunedì":
  case "Martedì":
  case "Mercoledì":
  case "Giovedì":
  case "Venerdì":
    console.log("Giorno lavorativo");
    break;
  case "Sabato":
  case "Domenica":
    console.log("È il weekend!");
    break;
  default:
    console.log("Giorno non valido");
}

// Output: "È il weekend!"
```

In questo esempio, se `giorno` è `"Sabato"`, l'esecuzione "cade" fino al blocco di codice del caso `"Domenica"` ed esegue `console.log("È il weekend!")`.

**Altri esempi pratici**:

```javascript
/*
 * Raggruppamento per mesi e stagioni
 */

let mese = "Gennaio";

switch (mese) {
  case "Dicembre":
  case "Gennaio":
  case "Febbraio":
    console.log("Inverno");
    break;
  case "Marzo":
  case "Aprile":
  case "Maggio":
    console.log("Primavera");
    break;
  case "Giugno":
  case "Luglio":
  case "Agosto":
    console.log("Estate");
    break;
  case "Settembre":
  case "Ottobre":
  case "Novembre":
    console.log("Autunno");
    break;
  default:
    console.log("Mese non valido");
}

// Output: "Inverno"
```

## Il caso default

Il `default` è **opzionale** ma consigliato per gestire valori inaspettati.

```javascript
/*
 * Uso di default
 */

let voto = "C";

switch (voto) {
  case "A":
    console.log("Eccellente");
    break;
  case "B":
    console.log("Buono");
    break;
  case "C":
    console.log("Sufficiente");
    break;
  case "D":
  case "F":
    console.log("Insufficiente");
    break;
  default:
    console.log("Voto non riconosciuto");
}
```

Il `default` non deve necessariamente essere alla fine, ma è una convenzione:

```javascript
/*
 * default può stare ovunque (ma meglio alla fine)
 */

switch (valore) {
  default: // Valido ma poco convenzionale
    console.log("Default");
    break;
  case 1:
    console.log("Uno");
    break;
  case 2:
    console.log("Due");
    break;
}
```

## Confronto Strict (===)

**Importante**: Lo switch usa il confronto **strict** (`===`), non il confronto loose (`==`).

```javascript
/*
 * Switch usa ===
 */

let numero = "2"; // stringa

switch (numero) {
  case 2: // number
    console.log("Due (number)"); // ❌ NON eseguito
    break;
  case "2": // string
    console.log("Due (string)"); // ✅ Eseguito
    break;
}

// Output: "Due (string)"
```

## Switch con Espressioni

Lo switch può valutare espressioni, non solo variabili:

```javascript
/*
 * Switch con espressioni
 */

let a = 5;
let b = 10;

switch (a + b) {
  case 10:
    console.log("Somma è 10");
    break;
  case 15:
    console.log("Somma è 15"); // ✅ Eseguito
    break;
  case 20:
    console.log("Somma è 20");
    break;
  default:
    console.log("Somma diversa");
}
```

## Quando Usare switch vs if...else

**Usa switch quando**:

- Confronti una **singola variabile/espressione** con molti valori specifici
- I confronti sono di **uguaglianza** (`===`)
- Hai **3 o più casi** da gestire
- Vuoi codice più **leggibile e strutturato**

```javascript
// ✅ Buon caso per switch
switch (comandoUtente) {
  case "start":
    avviaGioco();
    break;
  case "stop":
    fermaGioco();
    break;
  case "pause":
    mettiInPausa();
    break;
  case "reset":
    resettaGioco();
    break;
  default:
    mostraErrore();
}
```

**Usa if...else quando**:

- Hai **condizioni complesse** (range, confronti multipli)
- Usi **operatori diversi** (`>`, `<`, `>=`, `&&`, `||`)
- Hai **pochi casi** (1-2)

```javascript
// ✅ Buon caso per if...else
if (eta >= 18 && haPatente) {
  console.log("Puoi guidare");
} else if (eta >= 16) {
  console.log("Puoi guidare con supervisione");
} else {
  console.log("Non puoi guidare");
}

// ❌ Cattivo uso di switch (impossibile!)
// switch non può gestire condizioni complesse
```

## Best Practices

**Sempre usare break** (tranne in caso di raggruppamento intenzionale):

```javascript
// ✅ Corretto - break in ogni case
switch (valore) {
  case 1:
    console.log("Uno");
    break; // ✅
  case 2:
    console.log("Due");
    break; // ✅
}

// ❌ Pericoloso - break dimenticato
switch (valore) {
  case 1:
    console.log("Uno");
  // break dimenticato!
  case 2:
    console.log("Due"); // Eseguito anche se valore === 1
    break;
}
```

**Includere sempre default**:

```javascript
// ✅ Con default (robusto)
switch (azione) {
  case "salva":
    salva();
    break;
  case "elimina":
    elimina();
    break;
  default:
    console.log("Azione non riconosciuta");
}
```

**Evitare logica complessa nei case**:

```javascript
// ❌ Troppa logica nel case
switch (stato) {
  case "attivo":
    let utente = trovaUtente();
    if (utente.isAdmin) {
      mostraAdmin();
    } else {
      mostraUtente();
    }
    break;
}

// ✅ Estrarre in funzioni
switch (stato) {
  case "attivo":
    gestisciUtenteAttivo();
    break;
}
```

**Documentare fall through intenzionale**:

```javascript
// ✅ Commentare fall through intenzionali
switch (livello) {
  case "admin":
    abilitaGestioneUtenti();
  // fall through - admin ha anche permessi editor
  case "editor":
    abilitaModificaContenuti();
  // fall through - editor ha anche permessi lettore
  case "lettore":
    abilitaLettura();
    break;
}
```

## Collegamenti

- [[condizionali]] - Istruzioni condizionali (if, else, else if)
- [[statement]] - Statement e istruzioni
- [[blocchi]] - Blocchi di codice
- [[../tipi/coercizione]] - Confronto strict vs loose
- [[../tipi/truthy-falsy]] - Valutazione booleana nelle condizioni
