# Ciclo while

**Appunti Completi**: [[../../appunti-completi#28-cicli-loops]]

Il ciclo `while` è una delle forme più semplici di ciclo. La sua logica è: **"mentre questa condizione è vera, continua a eseguire il blocco di codice"**.

La condizione viene controllata **prima** di ogni iterazione. Se la condizione risulta falsa fin dall'inizio, il blocco di codice non verrà mai eseguito.

## Sintassi

```javascript
/*
 * Sintassi while
 */

while (condizione) {
  // codice eseguito finché condizione è true
}
```

## Esempi

```javascript
/*
 * Esempio: contare da 1 a 5
 */

let i = 1;

while (i <= 5) {
  console.log(i);
  i++; // Fondamentale per evitare cicli infiniti!
}

// Output:
// 1
// 2
// 3
// 4
// 5
```

## ⚠️ Cicli Infiniti

Il ciclo `while` può creare **cicli infiniti** se la condizione non diventa mai falsa.

```javascript
/*
 * Ciclo infinito - EVITARE!
 */

let x = 1;

while (x <= 5) {
  console.log(x);
  // MANCA x++! Il ciclo non terminerà mai
}
```

## Casi d'Uso

Il `while` è ideale quando:

- Non si conosce il numero di iterazioni in anticipo
- La condizione dipende da fattori esterni (input utente, condizioni runtime)
- Si vuole continuare fino a un evento specifico

```javascript
/*
 * Esempio pratico: input utente
 */

let risposta = "";

while (risposta !== "si") {
  risposta = prompt("Vuoi continuare? (si/no)");
}

console.log("Grazie!");
```

## Collegamenti

- [[do-while]] - Ciclo do...while (esegue almeno una volta)
- [[for]] - Ciclo for (quando il numero di iterazioni è noto)
- [[break-continue]] - Interrompere o saltare iterazioni
- [[condizionali]] - Istruzioni condizionali
