# [[../../appunti-completi#26-istruzioni-condizionali-conditionals|Istruzioni Condizionali]]

Le **istruzioni condizionali** permettono a un programma di prendere decisioni, eseguendo blocchi di codice diversi in base al verificarsi o meno di una determinata condizione.

Sono fondamentali per creare programmi dinamici che si adattano a situazioni diverse.

## L'Istruzione if

L'istruzione `if` è la struttura condizionale più comune. La sua logica è: **"se una certa condizione è vera, allora esegui questo blocco di codice"**.

La condizione da valutare viene inserita tra parentesi `()` e deve produrre un risultato booleano (`true` o `false`).

```javascript
/*
 * Sintassi base if
 */

if (condizione) {
  // codice eseguito solo se condizione è true
}

// Esempio pratico
let eta = 18;

if (eta >= 18) {
  console.log("Sei maggiorenne");
}

let temperatura = 35;

if (temperatura > 30) {
  console.log("Fa molto caldo!");
}
```

Se la condizione è `false`, il blocco di codice viene **saltato** e l'esecuzione continua dopo la chiusura `}`.

```javascript
/*
 * Condizione falsa - blocco saltato
 */

let punteggio = 45;

if (punteggio >= 60) {
  console.log("Hai superato l'esame"); // NON viene eseguito
}

console.log("Fine programma"); // Viene sempre eseguito
```

## else: L'Alternativa

Spesso si vuole definire un comportamento alternativo da eseguire quando la condizione dell'`if` risulta falsa. Per questo si usa la clausola `else`.

```javascript
/*
 * if...else
 */

let eta = 15;

if (eta >= 18) {
  console.log("Sei maggiorenne");
} else {
  console.log("Sei minorenne");
}

// Output: "Sei minorenne"
```

L'`else` fornisce un **percorso alternativo**: esattamente uno dei due blocchi viene eseguito, mai entrambi.

```javascript
/*
 * Percorsi alternativi
 */

let oraCorrente = 14;

if (oraCorrente < 12) {
  console.log("Buongiorno");
} else {
  console.log("Buonasera");
}

// Output: "Buonasera"
```

## else if: Condizioni Multiple

Per gestire una serie di condizioni alternative in sequenza, si può usare `else if`. Il programma valuta le condizioni **una dopo l'altra** e si ferma non appena ne trova una vera, eseguendo solo il blocco di codice corrispondente.

```javascript
/*
 * Catena if...else if...else
 */

let voto = 85;

if (voto >= 90) {
  console.log("Eccellente");
} else if (voto >= 75) {
  console.log("Buono");
} else if (voto >= 60) {
  console.log("Sufficiente");
} else {
  console.log("Insufficiente");
}

// Output: "Buono"
```

**Importante**: Solo il **primo blocco** la cui condizione è `true` viene eseguito, anche se più condizioni potrebbero essere vere.

```javascript
/*
 * Solo il primo blocco true viene eseguito
 */

let numero = 100;

if (numero > 50) {
  console.log("Maggiore di 50"); // ✅ Eseguito
} else if (numero > 75) {
  console.log("Maggiore di 75"); // ❌ Saltato (anche se true!)
} else if (numero > 90) {
  console.log("Maggiore di 90"); // ❌ Saltato
}

// Output: Solo "Maggiore di 50"
```

Se **nessuna condizione** è vera, viene eseguito il blocco `else` finale, se presente.

```javascript
/*
 * Nessuna condizione vera - else eseguito
 */

let giorno = "sabato";

if (giorno === "lunedì") {
  console.log("Inizio settimana");
} else if (giorno === "venerdì") {
  console.log("Fine settimana");
} else {
  console.log("Altro giorno"); // ✅ Eseguito
}

// Output: "Altro giorno"
```

## Condizioni Complesse

Le condizioni possono essere combinate usando **operatori logici**.

```javascript
/*
 * Operatori logici nelle condizioni
 */

let eta = 25;
let haPatente = true;

// AND logico (&&) - entrambe devono essere true
if (eta >= 18 && haPatente) {
  console.log("Puoi guidare");
}

// OR logico (||) - almeno una deve essere true
let isWeekend = true;
let isVacanza = false;

if (isWeekend || isVacanza) {
  console.log("Giorno di riposo");
}

// NOT logico (!) - inverte il valore
let piove = false;

if (!piove) {
  console.log("Bel tempo!");
}
```

## Best Practices

**Sempre usare le parentesi graffe**

```javascript
// ❌ Evitare (fragile, errori facili)
if (eta >= 18) console.log("Maggiorenne");

// ✅ Preferire (chiaro e sicuro)
if (eta >= 18) {
  console.log("Maggiorenne");
}
```

**Condizioni chiare ed esplicite**

```javascript
// ❌ Condizione implicita (confusa)
let utente = "Mario";
if (utente) {
  // cosa stiamo verificando?
}

// ✅ Condizione esplicita (chiara)
if (utente !== null && utente !== "") {
  console.log("Utente valido");
}
```

**Evitare condizioni troppo annidate**

```javascript
// ❌ Troppi livelli (difficile leggere)
if (condizione1) {
  if (condizione2) {
    if (condizione3) {
      if (condizione4) {
        // codice
      }
    }
  }
}

// ✅ Usare early return o semplificare
if (!condizione1) return;
if (!condizione2) return;
if (!condizione3) return;
if (!condizione4) return;

// codice
```

**Ordinare condizioni dalla più specifica alla più generica**

```javascript
// ✅ Ordine corretto
if (voto >= 90) {
  console.log("Eccellente");
} else if (voto >= 75) {
  console.log("Buono");
} else if (voto >= 60) {
  console.log("Sufficiente");
} else {
  console.log("Insufficiente");
}

// ❌ Ordine errato (la prima cattura tutto!)
if (voto >= 60) {
  console.log("Sufficiente"); // Anche voti alti finiscono qui!
} else if (voto >= 75) {
  // Mai eseguito
} else if (voto >= 90) {
  // Mai eseguito
}
```

## Collegamenti

- [[statement]] - Statement in generale
- [[blocchi]] - Blocchi di codice e scope
- [[../operatori/operatori-confronto]] - Operatori di confronto per condizioni
- [[../operatori/operatori-logici]] - Operatori logici (&&, ||, !)
- [[../tipi/coercizione]] - Coercizione nelle condizioni
