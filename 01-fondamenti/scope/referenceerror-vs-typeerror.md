# [[../../appunti-completi#errori|ReferenceError vs TypeError]]

Gli errori legati allo scope in JavaScript si dividono in due categorie principali: **ReferenceError** e **TypeError**.

## ReferenceError

Il **ReferenceError** si verifica a causa di un fallimento nella **risoluzione dello scope**. Indica che l'Engine non ha trovato una variabile in nessuno scope della catena (fino al globale). Questo errore viene generalmente identificato prima dell'esecuzione (durante la fase di compilazione o risoluzione).

**Esempio di ricerca RHS (recupero valore) fallita**:

```javascript
function foo(a) {
  console.log(a + b); // ❌ ReferenceError: b is not defined
}

foo(2);
```

**Esempio di utilizzo generico**:

```javascript
console.log(variabileInesistente); // ❌ ReferenceError: variabileInesistente is not defined

function test() {
  return altroNome * 2; // ❌ ReferenceError: altroNome is not defined
}
```

## TypeError

Il **TypeError** si verifica quando lo scope è stato risolto correttamente (la variabile è stata trovata), ma si tenta un'**operazione illegale** sul valore contenuto nella variabile. Questo avviene sempre durante l'esecuzione del codice.

**Esempi di operazioni illegali**:

```javascript
let numero = 42;
numero(); // ❌ TypeError: numero is not a function (esiste, ma non è una funzione)

let obj = null;
console.log(obj.proprieta); // ❌ TypeError: Cannot read property 'proprieta' of null

const PI = 3.14;
PI = 3.14159; // ❌ TypeError: Assignment to constant variable
```

## Distinzione Fondamentale

| Errore             | Significato                       | Causa                           |
| ------------------ | --------------------------------- | ------------------------------- |
| **ReferenceError** | "Non ho trovato la variabile"     | Problema di **scope**           |
| **TypeError**      | "Trovata, ma operazione illegale" | Problema di **tipo/operazione** |

**Nota bene**: Accedere a proprietà **non esistenti** di un oggetto esistente non genera un ReferenceError, bensì restituisce `undefined`.

## Best Practices di Gestione

È possibile gestire gli errori appropriatamente distinguendo il loro tipo nel costrutto try-catch:

```javascript
try {
  console.log(variabileTest);
} catch (error) {
  if (error instanceof ReferenceError) {
    console.log("Variabile non dichiarata");
  } else if (error instanceof TypeError) {
    console.log("Operazione illegale");
  }
}
```
