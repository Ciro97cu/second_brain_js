# Operatori di Assegnamento

Gli operatori di assegnamento memorizzano un valore in una variabile. L'operatore base è `=`, ma esistono anche operatori composti che combinano un'operazione con l'assegnamento.

## Operatori

- `=` → assegnamento base
- `+=` → addizione e assegnamento
- `-=` → sottrazione e assegnamento
- `*=` → moltiplicazione e assegnamento
- `/=` → divisione e assegnamento
- `%=` → resto e assegnamento
- `**=` → esponenziazione e assegnamento

## Funzionamento

L'operatore `=` valuta l'espressione a destra e memorizza il risultato nella variabile a sinistra.

Gli operatori composti (`+=`, `-=`, etc.) sono scorciatoie sintattiche: `x += 5` equivale a `x = x + 5`.

## Esempio di Riferimento

```javascript
/* Operatori di assegnamento */

// Assegnamento base
let x = 10;
let nome = "Mario";
let attivo = true;

// Assegnamento composto - addizione
let punteggio = 100;
punteggio += 50; // equivale a: punteggio = punteggio + 50
console.log(punteggio); // 150

// Sottrazione
let vite = 3;
vite -= 1; // vite = vite - 1
console.log(vite); // 2

// Moltiplicazione
let prezzo = 20;
prezzo *= 3; // prezzo = prezzo * 3
console.log(prezzo); // 60

// Divisione
let totale = 100;
totale /= 4; // totale = totale / 4
console.log(totale); // 25

// Resto (remainder)
let numero = 17;
numero %= 5; // numero = numero % 5
console.log(numero); // 2

// Esponenziazione
let base = 2;
base **= 3; // base = base ** 3
console.log(base); // 8

// Con stringhe (+=)
let messaggio = "Ciao";
messaggio += " mondo"; // concatenazione
console.log(messaggio); // "Ciao mondo"

// Catena di assegnamenti
let a, b, c;
a = b = c = 10; // tutti valgono 10
console.log(a, b, c); // 10 10 10
```

## Punti Chiave

1. **Direzione**: Il valore a destra viene assegnato alla variabile a sinistra

2. **Operatori composti**: Più concisi ma equivalenti alla forma estesa (`x += 5` vs `x = x + 5`)

3. **Concatenazione**: `+=` con stringhe esegue concatenazione, non somma numerica

4. **Catena**: Si può assegnare lo stesso valore a più variabili: `a = b = c = 10`

5. **Espressioni**: La parte destra è sempre un'espressione che viene valutata prima dell'assegnamento

## Collegamenti

- [[variabili]] - Gli operatori di assegnamento memorizzano valori nelle variabili
- [[expression]] - La parte destra di un assegnamento è un'espressione
- [[operatori/matematici]] - Gli operatori composti combinano matematica e assegnamento
