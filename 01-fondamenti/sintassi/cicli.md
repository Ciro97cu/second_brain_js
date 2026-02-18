# [[../../appunti-completi#28-cicli-loops|Cicli (Loops)]]

I **cicli** (loops) sono strutture fondamentali in programmazione che permettono di eseguire un blocco di codice ripetutamente, finché una determinata condizione rimane vera.

Ogni esecuzione del blocco di codice all'interno di un ciclo è chiamata **iterazione** (iteration). I cicli sono essenziali per automatizzare compiti ripetitivi.

## Tipi di Cicli

JavaScript offre diversi tipi di cicli, ognuno con caratteristiche specifiche:

### Cicli Basici

- **[[while]]** - Esegue finché la condizione è vera (controlla prima)
- **[[do-while]]** - Esegue almeno una volta (controlla dopo)
- **[[for]]** - Quando il numero di iterazioni è noto

### Cicli per Iterabili (ES6+)

- **[[for-of]]** - Itera sui **valori** di array, stringhe, iterabili
- **[[for-in]]** - Itera sulle **chiavi** di oggetti

### Controllo del Flusso

- **[[break-continue]]** - Interrompere o saltare iterazioni

## Guida alla Scelta del Ciclo

```javascript
// ✅ for - quando sai quante iterazioni
for (let i = 0; i < 10; i++) {
  // contare, accedere a indici
}

// ✅ for...of - per iterare su array/stringhe
for (let item of array) {
  // valori diretti, codice leggibile
}

// ✅ for...in - per proprietà di oggetti
for (let key in object) {
  // iterare su chiavi oggetto
}

// ✅ while - quando non sai quante iterazioni
while (condizione) {
  // continua fino a evento
}

// ✅ do...while - eseguire almeno una volta
do {
  // menu, validazione input
} while (condizione);
```

## Best Practices

### Evitare Cicli Infiniti

```javascript
// ❌ Ciclo infinito
for (let i = 0; i < 10; ) {
  // MANCA i++!
  console.log(i);
}

// ✅ Incremento presente
for (let i = 0; i < 10; i++) {
  console.log(i);
}
```

### Usare const quando Possibile

```javascript
// ✅ const quando non riassegni
for (const item of array) {
  console.log(item);
}

// let solo se devi modificare
for (let item of array) {
  item = item * 2; // Riassegnazione
}
```

### Ottimizzare i Calcoli

```javascript
// ❌ Calcolo ripetuto
for (let i = 0; i < array.length; i++) {
  // array.length calcolato ogni volta!
}

// ✅ Calcolo una volta
let len = array.length;
for (let i = 0; i < len; i++) {
  // Più efficiente
}

// ✅ Oppure usa for...of
for (let item of array) {
  // Nessun calcolo length
}
```

## Tabella Riepilogativa

| Ciclo        | Quando Usare                        | Controllo Condizione |
| ------------ | ----------------------------------- | -------------------- |
| `for`        | Numero iterazioni noto, indici      | Prima                |
| `for...of`   | Iterare su valori (array, stringhe) | Automatico           |
| `for...in`   | Iterare su chiavi oggetti           | Automatico           |
| `while`      | Numero iterazioni ignoto            | Prima                |
| `do...while` | Eseguire almeno una volta           | Dopo                 |

## Collegamenti

- [[condizionali]] - Istruzioni condizionali (if, else, else if)
- [[switch]] - Switch statement
- [[blocchi]] - Blocchi di codice
- [[statement]] - Statement e istruzioni
- [[../array/array-iterazione]] - Metodi array (forEach, map, filter)
- [[../tipi/truthy-falsy]] - Truthy/falsy nelle condizioni dei cicli
