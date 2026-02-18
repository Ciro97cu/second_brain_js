# [[../../appunti-completi#37-array|Manipolazione Array]]

Metodi per **aggiungere** o **rimuovere** elementi da un array. Tutti questi metodi **modificano l'array originale**.

## Push e Pop (fine array)

**`push()`** - Aggiunge elementi alla fine

```javascript
let numeri = [1, 2, 3];
numeri.push(4); // [1, 2, 3, 4]
numeri.push(5, 6); // [1, 2, 3, 4, 5, 6]
```

**`pop()`** - Rimuove l'ultimo elemento e lo restituisce

```javascript
let numeri = [1, 2, 3];
let ultimo = numeri.pop(); // ultimo = 3, numeri = [1, 2]
```

## Unshift e Shift (inizio array)

**`unshift()`** - Aggiunge elementi all'inizio

```javascript
let numeri = [2, 3];
numeri.unshift(1); // [1, 2, 3]
numeri.unshift(-1, 0); // [-1, 0, 1, 2, 3]
```

**`shift()`** - Rimuove il primo elemento e lo restituisce

```javascript
let numeri = [1, 2, 3];
let primo = numeri.shift(); // primo = 1, numeri = [2, 3]
```

## Splice (posizione specifica)

**`splice(inizio, quantità, ...nuovi)`** - Rimuove, sostituisce o aggiunge elementi

```javascript
let numeri = [1, 2, 3, 4, 5];

// Rimuovere 2 elementi dall'indice 1
numeri.splice(1, 2); // [1, 4, 5] (rimuove 2 e 3)

// Aggiungere senza rimuovere (quantità = 0)
numeri.splice(1, 0, 2, 3); // [1, 2, 3, 4, 5]

// Sostituire elementi
numeri.splice(2, 1, 99); // [1, 2, 99, 4, 5]
```

**Pattern Stack/Queue**:

- **Stack** (LIFO): `push()` + `pop()`
- **Queue** (FIFO): `push()` + `shift()`

## Collegamenti

- [[array]] - Concetti base array
- [[array-iterazione]] - Higher-order functions
- [[array-metodi]] - Altri metodi utili
