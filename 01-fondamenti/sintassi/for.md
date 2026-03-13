# [[../../appunti-completi#28-cicli-loops|Ciclo for]]

Quando il numero di iterazioni è noto in anticipo o si deve contare, il ciclo `for` è spesso la scelta più chiara e compatta. Serve a ripetere un blocco di codice in base a una condizione, fornendo un costrutto compatto per gestire l'inizializzazione, la verifica e l'aggiornamento di un contatore.

La sua sintassi concentra in un'unica espressione **tre parti fondamentali**:

1. **Inizializzazione** → Eseguita una sola volta prima del ciclo (es. `let i = 0`).
2. **Condizione** → Valutata prima di ogni iterazione. Se falsa, il ciclo termina (es. `i < 10`).
3. **Aggiornamento** → Eseguito alla fine di ogni iterazione (es. `i++`).

## Sintassi

```javascript
/*
 * Sintassi generale e un esempio base
 */
for (inizializzazione; condizione; aggiornamento) {
  // codice eseguito ad ogni iterazione
}

for (let i = 0; i < 5; i++) {
  console.log(i); // 0, 1, 2, 3, 4
}
```

## Flusso di Esecuzione

All'avvio, viene eseguita l'inizializzazione. Successivamente viene verificata la condizione: se risulta vera (`true`), viene eseguito il corpo del ciclo. Al termine dell'esecuzione del blocco interno, si passa all'istruzione di aggiornamento per poi ricalcolare la condizione.

```javascript
for (let i = 0; i < 3; i++) {
  console.log("Iterazione:", i);
}

// 1. Inizializzazione: let i = 0
// 2. Condizione: i < 3? (true) → Esegue blocco
// 3. Aggiornamento: i++
// Il ciclo prosegue fince' la condizione diventa false.
```

## Esempi Pratici

I cicli `for` offrono ampia flessibilita', potendo contare alla rovescia, usare incrementi maggiori di 1 o iterare sugli elementi di un array mediante l'indice.

```javascript
// Iterare all'indietro
for (let i = 5; i > 0; i--) {
  console.log(i); // 5, 4, 3, 2, 1
}

// Incrementi diversi
for (let i = 0; i <= 10; i += 2) {
  console.log(i); // 0, 2, 4, 6, 8, 10
}

// Iterare su array (approccio classico)
const colori = ["rosso", "verde", "blu"];
for (let i = 0; i < colori.length; i++) {
  console.log(colori[i]); // "rosso", "verde", "blu"
}
```

## Ottimizzazioni

Quando si itera su un array molto lungo, calcolare `array.length` ad ogni ciclo può ridurre le prestazioni in alcuni vecchi motori JavaScript, ma oggi e' quasi sempre ottimizzato. 

```javascript
// Approccio caching della lunghezza (efficienza teorica superiore)
const arr = [1, 2, 3, 4, 5];
for (let i = 0, len = arr.length; i < len; i++) {
  console.log(arr[i]);
}

// Alternativa moderna (suggerita nella maggior parte dei casi)
for (const item of arr) {
  console.log(item);
}
```

## Casi d'Uso

Il ciclo `for` è ideale quando:

- È noto il numero esatto di iterazioni da compiere.
- Occorre iterare compiendo passi multipli (es. `i += 2`) o decrescenti.
- È strettamente necessario accedere all'indice univoco degli elementi durante il ciclo.

## Collegamenti

- [[for-in-of]] - Cicli for in/of (iterare su oggetti e valori)
- [[while]] - Ciclo while (quando non si conosce il numero di iterazioni)
- [[break-continue]] - Interrompere o saltare iterazioni
- [[../../01-fondamenti/array/array-iterazione|Iterazione Array]]
