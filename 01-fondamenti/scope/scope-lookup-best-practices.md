# [[../../appunti-completi#best-practices-sul-look-up-nello-scope|Best Practices sul Look-up nello Scope]]

È fondamentale scrivere codice in cui la risoluzione degli identificatori risulti chiara e con una gerarchia di scope limitata.

## Comprendere l'Ordine di Ricerca

La ricerca procede sempre dall'interno verso l'esterno. Risulta utile evidenziare chiaramente la provenienza delle variabili:

```javascript
// ✅ Chiaro: si intuisce il look-up
function calcola(x) {
  let fattore = 2;

  function moltiplica() {
    return x * fattore; // Si capisce che derivano da scope esterni
  }

  return moltiplica();
}
```

## Evitare Shadowing Non Intenzionale

Si consiglia di usare nomi distinti per le variabili quando possibile, in modo da evitare confusione con lo shadowing.

```javascript
// ❌ Shadowing confuso
function outer() {
  let count = 10;

  function inner() {
    let count = 5; // Quale count viene usato?
    console.log(count);
  }
}

// ✅ Nomi distinti
function outer() {
  let totalCount = 10;

  function inner() {
    let localCount = 5; // Nessuna ambiguità
    console.log(totalCount, localCount);
  }
}
```

## Minimizzare i Livelli di Look-up

Dover risalire numerosi livelli per trovare una variabile peggiora la leggibilità e può avere un trascurabile ma presente impatto computazionale.

```javascript
// ❌ Look-up profondo e farraginoso
function a() {
  let x = 10;
  function b() {
    function c() {
      function d() {
        console.log(x); // Look-up attraverso 4 livelli
      }
    }
  }
}

// ✅ Più diretto
function a() {
  let x = 10;
  function b() {
    console.log(x); // Look-up attraverso solo 2 livelli
  }
}
```

Mantenere scope poco profondi garantisce codice più pulito, scalabile e facile da debuggare.
