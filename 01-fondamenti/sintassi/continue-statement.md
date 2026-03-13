# [[../../appunti-completi#28-cicli-loops|L'istruzione continue]]

L'istruzione `continue` viene utilizzata all'interno dei cicli per saltare la porzione rimanente del blocco di codice per l'iterazione corrente e procedere direttamente con la valutazione dell'espressione successiva o del passo di iterazione.

## Saltare un'Iterazione

A differenza del `break` che esce in maniera definitiva dal ciclo, il `continue` ordina al motore JavaScript di ignorare qualsiasi istruzione successiva all'interno del blocco iterativo e passare alla prossima iterazione prevista.

### Uso in un ciclo for

Nel ciclo `for`, il `continue` esegue l'aggiornamento dell'iteratore e poi verifica nuovamente la condizione.

```javascript
for (let i = 0; i < 5; i++) {
  if (i === 2) {
    continue; // Salta quando i è 2
  }
  console.log(i);
}
// Output: 0, 1, 3, 4
// L'esecuzione per il valore 2 è stata saltata.
```

### Uso in un ciclo while

L'uso di `continue` in un `while` o `do...while` passa direttamente alla valutazione della condizione. Occorre prestare attenzione ad aggiornare l'iteratore prima di chiamare `continue`, per evitare cicli infiniti.

```javascript
let i = 0;
while (i < 5) {
  i++;
  if (i === 3) {
    continue;
  }
  console.log(i);
}
// Stampa: 1, 2, 4, 5
```

## Casi d'Uso Tipici

L'istruzione `continue` è indicata quando:
- È necessario escludere determinati valori durante la scansione di un array.
- Si vuole evitare l'annidamento eccessivo di blocchi condizionali `if` all'interno del ciclo iterativo principale.
