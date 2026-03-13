# [[../../appunti-completi#scope-lessicale-lexical-scope|Lexical vs Dynamic Scope]]

JavaScript utilizza esclusivamente il **lexical scope** (scope lessicale), come la maggior parte dei linguaggi di programmazione moderni. Il termine "lessicale" si riferisce alla fase di lexing, che è parte del processo di compilazione in cui il codice sorgente viene analizzato e suddiviso in token.

## Lexical vs Dynamic Scope

La differenza fondamentale risiede nel criterio utilizzato per risolvere i riferimenti alle variabili non dichiarate localmente:

| Tipo        | Di base su                                                                | Esempi di linguaggi         |
| ----------- | ------------------------------------------------------------------------- | --------------------------- |
| **Lexical** | **Dove** la funzione è stata definita (struttura statica del codice)      | JavaScript, C, Java, Python |
| **Dynamic** | **Da dove** la funzione è stata invocata (catena dinamica delle chiamate) | Bash, alcuni dialetti Lisp  |

### Esempio di Confronto

Nel seguente esempio, viene mostrato come JavaScript risolve lo scope mediante l'approccio lessicale. Se JavaScript usasse il dynamic scope, il risultato sarebbe diverso:

```javascript
let valore = "globale";

function mostraValore() {
  // Con lexical scope, 'valore' viene risolto in base a dove questa
  // funzione è definita (scope globale in questo caso)
  console.log(valore);
}

function test() {
  let valore = "locale";
  mostraValore(); // Invocazione
}

test();
// LEXICAL SCOPE (JavaScript): stampa "globale"
// → mostraValore() è DEFINITA nello scope globale, quindi 'valore' si riferisce alla variabile globale.

// DYNAMIC SCOPE (ipotetico, es. in Bash): stamperebbe "locale"
// → mostraValore() viene CHIAMATA dall'interno di test(), dove 'valore' vale "locale".
```

## Struttura e Immutabilità

Poiché il lexical scope si basa sulla struttura statica del codice sorgente, esso è **immutabile** durante l'esecuzione (runtime). Una volta che il codice è stato analizzato (fase di lexing/parsing), i confini degli scope non cambiano, a meno che non si utilizzino costrutti sconsigliati come `eval` o `with`, che modificano lo scope dinamichemente ma introducono forti inefficienze e imprevedibilità.

```javascript
function esterna() {
  let x = 10;

  function interna() {
    // La funzione 'interna' può accedere a 'x' in modo prevedibile
    // perché è scritta fisicamente all'interno di 'esterna'
    console.log(x); // 10
  }

  return interna;
}

let fn = esterna();
fn(); // Stampa 10 - 'interna' ricorda l'ambiente in cui è stata definita
```
