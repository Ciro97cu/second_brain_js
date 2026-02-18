# [[../../appunti-completi#28-cicli-loops|Ciclo for]]

Quando il numero di iterazioni è noto in anticipo o si deve contare, il ciclo `for` è spesso la scelta più chiara e compatta.

La sua sintassi concentra in un'unica riga **tre parti fondamentali**:

1. **Inizializzazione** → Eseguita una sola volta prima del ciclo (es. `let i = 0`)
2. **Condizione** → Valutata prima di ogni iterazione. Se falsa, il ciclo termina (es. `i < 10`)
3. **Aggiornamento** → Eseguito alla fine di ogni iterazione (es. `i++`)

## Sintassi

```javascript
/*
 * Sintassi for
 */

for (inizializzazione; condizione; aggiornamento) {
  // codice eseguito ad ogni iterazione
}

// Esempio base
for (let i = 0; i < 5; i++) {
  console.log(i);
}

// Output:
// 0
// 1
// 2
// 3
// 4
```

## Flusso di Esecuzione

```javascript
/*
 * Come funziona il ciclo for
 */

for (let i = 0; i < 3; i++) {
  console.log("Iterazione:", i);
}

// 1. let i = 0           → Inizializzazione (una volta)
// 2. i < 3?              → Condizione (true)
// 3. console.log(...)    → Esecuzione blocco
// 4. i++                 → Aggiornamento
// 5. i < 3?              → Condizione (true)
// 6. console.log(...)    → Esecuzione blocco
// 7. i++                 → Aggiornamento
// 8. i < 3?              → Condizione (true)
// 9. console.log(...)    → Esecuzione blocco
// 10. i++                → Aggiornamento
// 11. i < 3?             → Condizione (false) → FINE
```

## Esempi Pratici

```javascript
/*
 * Iterare all'indietro
 */

for (let i = 5; i > 0; i--) {
  console.log(i);
}
// Output: 5, 4, 3, 2, 1

/*
 * Incrementi diversi
 */

for (let i = 0; i <= 10; i += 2) {
  console.log(i);
}
// Output: 0, 2, 4, 6, 8, 10

/*
 * Iterare su array
 */

let colori = ["rosso", "verde", "blu"];

for (let i = 0; i < colori.length; i++) {
  console.log(colori[i]);
}
// Output: "rosso", "verde", "blu"
```

## Ottimizzazioni

```javascript
/*
 * ❌ Calcolo ripetuto (inefficiente)
 */

for (let i = 0; i < array.length; i++) {
  // array.length viene calcolato OGNI iterazione
  console.log(array[i]);
}

/*
 * ✅ Calcolo una volta (efficiente)
 */

let len = array.length;
for (let i = 0; i < len; i++) {
  console.log(array[i]);
}

/*
 * ✅ Alternativa moderna (usa for...of)
 */

for (let item of array) {
  console.log(item);
}
```

## Casi d'Uso

Il `for` è ideale quando:

- Si conosce il numero di iterazioni in anticipo
- Si deve contare (0 a N, N a 0)
- Si deve accedere agli indici degli array
- Si vogliono incrementi personalizzati

## Collegamenti

- [[for-of]] - Ciclo for...of (iterare su valori)
- [[while]] - Ciclo while (quando non si conosce il numero di iterazioni)
- [[break-continue]] - Interrompere o saltare iterazioni
- [[../array/array]] - Array e iterazione
