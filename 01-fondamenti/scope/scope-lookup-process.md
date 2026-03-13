# [[../../appunti-completi#il-processo-di-ricerca-look-up-nello-scope-lessicale|Processo di Look-up nello Scope]]

Il **processo di look-up** cerca le variabili partendo dalla bolla dello scope più intero e risalendo verso le bolle esterne.

## Concetto Chiave

Il motore JavaScript (Engine) cerca le variabili con una **ricerca a risalita**: inizia dalla bolla corrente e sale di livello in livello finché trova la variabile o raggiunge lo scope globale. Se non trova nulla nello scope globale, genera un `ReferenceError`.

### Ricerca Multi-Livello

```javascript
function foo(a) {
  let b = a * 2;

  function bar(c) {
    // Engine cerca 'a':
    // 1. Bolla bar → ❌ Non trovato
    // 2. Bolla foo → ✅ Trovato! (a = 2)

    // Engine cerca 'b':
    // 1. Bolla bar → ❌ Non trovato
    // 2. Bolla foo → ✅ Trovato! (b = 4)

    // Engine cerca 'c':
    // 1. Bolla bar → ✅ Trovato! (c = 12)

    console.log(a, b, c); // 2 4 12
  }

  bar(b * 3);
}

foo(2);
```

La ricerca si **ferma alla prima corrispondenza**.

## Esempio Pratico

Di seguito un esempio che mostra la propagazione del look-up attraverso diverse bolle annidate:

```javascript
let tassa = 0.22; // Bolla 1: Globale

function calcolaPrezzoFinale(prezzoBase) {
  // Bolla 2
  let margine = 0.3;

  function applicaTassa() {
    // Bolla 3

    // Look-up per 'prezzoBase':
    // Bolla 3 → ❌ | Bolla 2 → ✅ Trovato!
    let prezzoConMargine = prezzoBase * (1 + margine);

    // Look-up per 'tassa':
    // Bolla 3 → ❌ | Bolla 2 → ❌ | Bolla 1 → ✅ Trovato!
    let prezzoFinale = prezzoConMargine * (1 + tassa);

    return prezzoFinale;
  }

  return applicaTassa();
}

console.log(calcolaPrezzoFinale(100)); // 158.6
```

Il processo di look-up avviene interamente a tempo di esecuzione, ma le regole di associazione tra identificatori e scope sono definite in modo lessicale (durante il parsing).
