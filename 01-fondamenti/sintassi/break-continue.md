# break e continue

JavaScript offre due parole chiave per controllare il flusso di esecuzione all'interno dei cicli: `break` per interrompere completamente un ciclo e `continue` per saltare l'iterazione corrente.

## break: Interrompere un Ciclo

A volte è necessario interrompere un ciclo **prima** che la sua condizione diventi falsa. Per questo si usa l'istruzione `break`.

Appena il programma incontra `break`, **esce immediatamente** dal ciclo e continua l'esecuzione dal codice successivo.

### Sintassi break

```javascript
/*
 * Uso di break in for
 */

for (let i = 0; i < 10; i++) {
  if (i === 5) {
    break; // Interrompe il ciclo quando i è 5
  }
  console.log(i);
}

// Output:
// 0
// 1
// 2
// 3
// 4
// (il ciclo si ferma, NON stampa 5, 6, 7, 8, 9)
```

### break con while

```javascript
/*
 * break per uscire da while
 */

let counter = 0;

while (true) {
  // Ciclo infinito!
  console.log(counter);
  counter++;

  if (counter >= 3) {
    break; // Uscita dal ciclo infinito
  }
}

console.log("Ciclo terminato");

// Output:
// 0
// 1
// 2
// "Ciclo terminato"
```

### Esempio Pratico: Cercare un Elemento

```javascript
/*
 * Cercare in un array e fermarsi quando trovato
 */

let numeri = [10, 20, 30, 40, 50];
let cercato = 30;
let trovato = false;

for (let numero of numeri) {
  if (numero === cercato) {
    trovato = true;
    console.log("Trovato:", numero);
    break; // Non serve continuare a cercare
  }
}

if (trovato) {
  console.log("Elemento presente");
}
```

## continue: Saltare un'Iterazione

L'istruzione `continue` **salta** l'iterazione corrente e passa alla successiva, senza uscire dal ciclo.

### Sintassi continue

```javascript
/*
 * Uso di continue
 */

for (let i = 0; i < 5; i++) {
  if (i === 2) {
    continue; // Salta quando i è 2
  }
  console.log(i);
}

// Output:
// 0
// 1
// (salta 2)
// 3
// 4
```

### Esempio Pratico: Filtrare Valori

```javascript
/*
 * Stampare solo numeri pari
 */

for (let i = 0; i < 10; i++) {
  if (i % 2 !== 0) {
    continue; // Salta i numeri dispari
  }
  console.log(i); // Stampa solo pari
}

// Output: 0, 2, 4, 6, 8
```

## Differenza break vs continue

| Istruzione | Comportamento                                      |
| ---------- | -------------------------------------------------- |
| `break`    | **Esce** completamente dal ciclo                   |
| `continue` | **Salta** l'iterazione corrente, prosegue il ciclo |

```javascript
/*
 * Confronto break vs continue
 */

// break - esce al primo dispari
for (let i = 0; i < 10; i++) {
  if (i % 2 !== 0) {
    break; // ESCE completamente
  }
  console.log(i);
}
// Output: 0

// continue - salta i dispari, prosegue
for (let i = 0; i < 10; i++) {
  if (i % 2 !== 0) {
    continue; // SALTA questa iterazione
  }
  console.log(i);
}
// Output: 0, 2, 4, 6, 8
```

## Casi d'Uso

**Usa `break` quando**:

- Devi fermarti appena trovi un risultato
- Vuoi uscire da un ciclo potenzialmente infinito
- La condizione di uscita è complessa e non può stare nel `while/for`

**Usa `continue` quando**:

- Devi saltare alcuni elementi ma continuare con gli altri
- Vuoi evitare nesting eccessivo di `if`
- Devi filtrare valori durante l'iterazione

## Collegamenti

- [[while]] - Ciclo while
- [[for]] - Ciclo for
- [[for-of]] - Ciclo for...of
- [[condizionali]] - Istruzioni condizionali (if)
