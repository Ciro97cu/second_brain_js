# [[../../appunti-completi#35-boxing-e-metodi-dei-primitivi|Il Concetto di Boxing]]

In JavaScript, i tipi primitivi (`string`, `number`, `boolean`) espongono metodi e proprietà utili per manipolarli, nonostante non siano oggetti.

## Metodi dei Tipi Primitivi

```javascript
let testo = "javascript";
console.log(testo.length); // 10 (proprietà)
console.log(testo.toUpperCase()); // "JAVASCRIPT" (metodo)

let numero = 3.14159;
console.log(numero.toFixed(2)); // "3.14" (metodo)
```

Sembra strano: i primitivi non sono oggetti, come possono avere metodi?

## Il Meccanismo del Boxing

Il **boxing** è il processo automatico con cui JavaScript "avvolge" temporaneamente un valore primitivo in un oggetto wrapper per permettere l'accesso a proprietà e metodi.

Quando si tenta di accedere a una proprietà o a un metodo su un primitivo, il motore JavaScript esegue i seguenti passaggi in background:

1. Crea un oggetto wrapper temporaneo (es. `new String()`, `new Number()`, `new Boolean()`).
2. L'oggetto wrapper contiene i metodi e le proprietà richieste.
3. Il metodo viene eseguito (o la proprietà viene letta).
4. L'oggetto wrapper temporaneo viene immediatamente scartato.

```javascript
let strPrimitive = "ciao";
// strPrimitive.toUpperCase() → cosa succede:
// 1. Viene creato un oggetto String("ciao") temporaneamente
// 2. Viene chiamato String.prototype.toUpperCase() sull'oggetto
// 3. Il risultato "CIAO" viene restituito
// 4. L'oggetto String temporaneo viene eliminato per il garbage collection

console.log(strPrimitive.toUpperCase()); // "CIAO"
console.log(typeof strPrimitive); // "string" (rimane un primitivo!)
```

Questo processo è trasparente per lo sviluppatore.

## Primitivi Sono Immutabili

Un valore primitivo "I am a string" non è un oggetto: è semplicemente un valore letterale primitivo e immutabile. Per eseguire operazioni come controllare la lunghezza o accedere a certi caratteri, servirebbe in teoria un oggetto `String` completo. Ma JavaScript risolve questa necessità con il boxing automatico, mantenendo i vantaggi in termini di prestazioni dei tipi primitivi base, fornendo al contempo l'utilità degli oggetti built-in.

## Collegamenti

- [[native-wrappers-vs-primitives]] - Wrapper objects vs primitivi
- [[object-wrappers-caveats]] - Problemi con i wrapper espliciti
- [[valori-tipi]] - Tipi primitivi vs Object
