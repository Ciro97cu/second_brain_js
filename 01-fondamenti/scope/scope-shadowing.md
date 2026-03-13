# [[../../appunti-completi#lo-shadowing-delle-variabili|Shadowing delle Variabili nello Scope]]

Lo **shadowing** si verifica quando una bolla di scope interna dichiara un identificatore con lo stesso nome presente in una bolla esterna. Poiché il processo di ricerca (look-up) si ferma alla prima corrispondenza utile, la variabile interna "fa ombra" (shadows) su quella esterna.

## Effetto dello Shadowing

Una volta che si incontra l'identificatore nello scope più interno, il motore si ferma. L'identificatore esterno risulta inaccessibile da quel punto in poi.

```javascript
function foo(a) {
  let b = a * 2;

  function bar(c) {
    let a = 100; // ⚠️ Shadows il parametro 'a' di foo

    // Look-up per 'a':
    // 1. Bolla bar → ✅ Trovato: a = 100
    // (Non arriva mai alla bolla foo dove a = 2)

    console.log(a, b, c); // 100 4 12 (non 2 4 12)
  }

  bar(b * 3);
}

foo(2);
```

### Shadowing Multi-Livello

Lo shadowing può propagarsi su più livelli annidati. Ogni livello più interno coprirà i successivi andando verso l'esterno.

```javascript
let x = "Globale";

function livello1() {
  let x = "Livello 1"; // Shadows globale

  function livello2() {
    let x = "Livello 2"; // Shadows livello1 e globale

    // Look-up per 'x':
    // 1. Bolla livello2 → ✅ Trovato: "Livello 2"
    console.log(x); // "Livello 2"
  }

  livello2();
  console.log(x); // "Livello 1" (usa il SUO x, dichiarato in livello1)
}

livello1();
console.log(x); // "Globale" (usa il SUO x, globale)
```

Occorre prestare attenzione poiché l'uso di identificatori identici in scope concentrici potrebbe creare confusione nella leggibilità e nell'intento del codice.
