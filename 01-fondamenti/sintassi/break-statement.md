# [[../../appunti-completi#28-cicli-loops|L'istruzione break]]

L'istruzione `break` è utilizzata all'interno dei costrutti iterativi (come i cicli) e nello statement `switch` per interrompere l'esecuzione e uscire immediatamente dal blocco corrente.

## Interrompere i Cicli

A volte è necessario interrompere un ciclo prima che la sua condizione di terminazione diventi falsa. Quando il motore JavaScript incontra un `break`, esce in maniera immediata dal ciclo e continua l'esecuzione partendo dal codice immediatamente successivo al blocco ciclico.

### Uso in un ciclo for

```javascript
for (let i = 0; i < 10; i++) {
  if (i === 5) {
    break; // Interrompe il ciclo quando i è 5
  }
  console.log(i);
}
// Vengono stampati i numeri da 0 a 4.
// Il ciclo si ferma prima di iterare con 5.
```

### Uso in un ciclo while

L'istruzione `break` è particolarmente utile per uscire da cicli potenzialmente infiniti in modo controllato.

```javascript
let counter = 0;

while (true) {
  console.log(counter);
  counter++;

  if (counter >= 3) {
    break; // Uscita dal ciclo
  }
}
// Stampa 0, 1, 2 e poi termina.
```

## Casi d'Uso Tipici

- Terminare un processo di ricerca appena si trova l'elemento desiderato in una collezione di dati.
- Uscire da un ciclo infinito quando avviene una determinata interazione dell'utente o un evento di sistema.
- Interrompere l'esecuzione dei `case` all'interno di un costrutto `switch`.
