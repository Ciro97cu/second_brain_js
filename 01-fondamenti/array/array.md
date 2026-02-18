# [[../../appunti-completi#37-array|Array]]

Un **array** è un **tipo speciale di oggetto** progettato per contenere una **collezione ordinata di elementi**.

## Struttura

```javascript
let frutti = ["mela", "banana", "arancia"];
//           [  0  ,    1    ,     2     ]  ← indici

console.log(frutti[0]); // "mela"
console.log(frutti[1]); // "banana"
console.log(frutti.length); // 3
```

A differenza degli oggetti generici (chiavi testuali), negli array i valori sono posizionati tramite **indice numerico**.

## Caratteristiche

**Indicizzazione da 0**: primo elemento `[0]`, secondo `[1]`, ecc.

**Accesso con `[]`**: parentesi quadre con numero posizione.

**Proprietà `length`**: numero elementi, aggiornata automaticamente.

## Array vs Oggetti

```javascript
let numeri = [10, 20, 30]; // ✅ Array
let persona = { nome: "Mario", eta: 30 }; // ✅ Oggetto

console.log(typeof numeri); // "object"
console.log(Array.isArray(numeri)); // true
```

**Quando usare**:

- **Array**: collezioni ordinate con indice numerico (liste, serie dati)
- **Oggetti**: strutture con proprietà nominate (entità, configurazioni)

Regola: array per accesso numerico, oggetti per nomi significativi.

## typeof vs Array.isArray()

`typeof` restituisce `"object"` per gli array. Per verificare se è un array usare `Array.isArray()`.

```javascript
Array.isArray([1, 2, 3]); // true
Array.isArray({ a: 1 }); // false
```

## Collegamenti

- [[../oggetti/oggetti]] - Array sono oggetti speciali
- [[array-manipolazione]] - Aggiungere/rimuovere elementi
- [[array-iterazione]] - forEach, map, filter, reduce
- [[array-metodi]] - slice, includes, find
