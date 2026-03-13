# [[../../appunti-completi#le-bolle-di-scope-annidate|Gerarchia e Contenimento delle Bolle]]

La gerarchia delle bolle di scope stabilisce l'accessibilità logica e progressiva delle variabili lungo i diversi passaggi di annidamento.

È naturale visualizzare i differenti livelli di annidamento per comprendere in modo diretto e immediato il meccanismo della risalita di scope.

```javascript
// BOLLE ANNIDATE: 4 livelli

let globale = "Bolla 1 (Attico)";

function livello1() {
  let locale1 = "Bolla 2";

  function livello2() {
    let locale2 = "Bolla 3";

    function livello3() {
      let locale3 = "Bolla 4 (Piano Terra)";

      // Dal piano terra, si "sale" fino all'attico
      console.log(locale3); // Bolla corrente
      console.log(locale2); // Risale di 1 livello
      console.log(locale1); // Risale di 2 livelli
      console.log(globale); // Risale di 3 livelli
    }

    livello3();

    // Dal livello 2, si sale positivamente ma NON si scende verso la tre
    console.log(locale2); // Bolla corrente
    console.log(locale1); // Risale
    console.log(globale); // Risale
    // console.log(locale3); // Errore: non si può scendere
  }

  livello2();
}

livello1();
```

Il contenimento di una bolla all'interno del proprio perimetro gerarchico impone la chiusura tassativa. Una funzione non subisce sdoppiamenti trovandosi divisa tra due entità. Una eventuale bolla per tale entità troverà spazio totalmente dentro la prima.

```javascript
// Corretto: Annidamento completo
function esterna() {
  // Bolla esterna
  let x = 10;

  function interna() {
    // Bolla interna totalmente DENTRO esterna
    console.log(x); // Accede a bolla esterna regolarmente
  }
}
```

## 🔗 Collegamenti

- [[scope-bubbles]]
- [[nested-scope]]
- [[scope-lookup]]
