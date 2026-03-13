# [[../../appunti-completi#scope-lessicale-vs-accesso-a-proprietà|Differenze tra Ricerca dello Scope e Accesso a Proprietà]]

La ricerca dello scope e l'accesso alle proprietà sono meccanismi diversi con regole e comportamenti distinti in JavaScript.

## Concetto Chiave

Quando viene valutata un'espressione come `oggetto.proprietà.valore`, lo scope lessicale si applica solo per risolvere il primo identificatore (`oggetto`). Successivamente, subentra il meccanismo di accesso alle proprietà per la restante parte della catena (`proprietà` e `valore`).

```javascript
let obj = {
  livello1: {
    valore: 42,
  },
};

function test() {
  // SCOPE LESSICALE: cerca 'obj'
  // 1. Scope di test → non trovato
  // 2. Scope globale → trovato

  // ACCESSO A PROPRIETÀ: accede a 'livello1' e 'valore'
  console.log(obj.livello1.valore); // 42
}

test();
```

## Comportamento degli Errori

Gli errori differiscono notevolmente tra la risoluzione dello scope e l'accesso alle proprietà.

Se un identificatore non viene trovato nello scope lessicale, il motore JavaScript genera un `ReferenceError`. Se invece un oggetto viene risolto ma la proprietà richiesta non è presente su di esso (e nemmeno nella sua catena dei prototipi), l'espressione restituisce `undefined` senza lanciare errori.

| Situazione      | Scope Lessicale  | Proprietà Oggetto |
| --------------- | ---------------- | ----------------- |
| Non trovato     | `ReferenceError` | `undefined`       |
| Tipo di ricerca | Scope chain      | Prototype chain   |
| Si ferma a      | Scope globale    | `null` prototype  |

```javascript
let dict = { x: 10 };

// PROPRIETÀ OGGETTO: proprietà non trovata → restituisce undefined
console.log(dict.proprietaNonEsiste); // undefined (nessun errore)

// SCOPE LESSICALE: variabile non trovata in nessuno scope → ReferenceError
// console.log(variabileNonEsiste); // lancia ReferenceError
```

La distinzione in fase di debugging è essenziale: un `ReferenceError` indica tipicamente un problema di scope (variabile non dichiarata e non risolvibile). Al contrario, l'uso errato di un valore inesistente di una proprietà (ovvero l'accesso in catena a partire da `undefined` o `null`) porterà a un `TypeError`.
