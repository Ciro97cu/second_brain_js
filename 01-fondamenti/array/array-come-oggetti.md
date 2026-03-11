# [[../../appunti-completi#gli-array-nell-ecosistema-degli-oggetti|Array come Oggetti]]

In JavaScript, gli **array sono internamente implementati come oggetti**. Proprio per questo motivo, condividono la possibilità di farsi assegnare proprietà testuali, sebbene siano nati per gestire prevalentemente indici numerici ordinati.

## Concetti Chiave

- **Proprietà personalizzate**: È possibile aggiungere normali proprietà a un array come se fosse un oggetto generico.
- **La proprietà `length`**: L'aggiunta di proprietà con nomi non numerici _non_ incrementa il conteggio del valore `length` nativo dell'array.
- **Stringhe numeriche**: Se si assegna una stringa che è convertibile in un numero intero positivo (es. `"3"`), l'array la elabora e accetta come un vero indice numerico.

## Aggiunta di Proprietà Testuali

Si possono assegnare proprietà a un array utilizzando la sintassi classica (dot notation o bracket notation). Questo rende l'array un ibrido logico, ma operare in questo modo non variazioni la sua dimensione "ufficiale".

```javascript
var myArray = ["foo", 42, "bar"];

/*
 * L'aggiunta di una pura stringa come chiave
 * non altera la lunghezza computata in length
 */
myArray.baz = "baz";

console.log(myArray.length); // 3 (Resta invariata)
console.log(myArray.baz); // "baz"
```

## Attenzione alla Coercizione di Stringhe Numeriche

Se la stringa passata come proprietà appare come un indice numerico perfettamente valido per la struttura interna (per es. la cifra testuale `"3"` o `"25"`), il motore non la percepirà come stringa arbitraria, ma spingerà a inquadrarla come un inserimento indicizzato, alterando la dimensione vitale dell'array.

```javascript
var myArray = ["foo", 42, "bar"];

/*
 * Una stringa che assume sembianze numeriche
 * sarà mappata verso un indice formale.
 */
myArray["3"] = "baz";

/*
 * Questo comportamento ricalcola lo span dell'array
 * modificandone la lunghezza totale.
 */
console.log(myArray.length); // Espanso a 4
console.log(myArray[3]); // "baz"
```

## ⚠️ Gotcha

- ❌ **Usare un Array per memorizzare coppie chiave-valore**: Se non verranno inserite logiche per indici, il tool non sta lavorando nei perimetri delle sue ottimizzazioni. È **consigliato ricorrere a un normale Oggetto** per immagazzinare associazioni chiave-valore.

## 🔗 Collegamenti

**Prerequisiti**:

- [[array]] - Il concetto basilare per memorizzare i dati
- [[../oggetti/oggetti]] - Comprendere al meglio la struttura a "dizionario"
- [[../oggetti/property-access]] - Regole sull'accesso a base punto vs parentesi quadre

**Concetti Correlati**:

- [[../tipi/coercizione]] - Meccanismi d'adeguamento tra stringhe e numeri

#array #oggetti #sintassi #coercizione
