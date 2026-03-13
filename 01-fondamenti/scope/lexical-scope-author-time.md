# [[../../appunti-completi#scope-lessicale-lexical-scope|Lexical Scope: Author-Time vs Run-Time]]

Il concetto di **lexical scope** (scope lessicale o statico) si basa sul fatto che l'accesso alle variabili è determinato **dove il codice è stato scritto** e non da dove esso viene eseguito.

Tale struttura dell'ambiente lessicale è finalizzata durante la fase di **lexing** (ovvero la prima parte della compilazione o parsing) che produce l'AST (Abstract Syntax Tree), rimanendo quindi **fissa** e invariabile a runtime.

## 🎯 Author-Time vs Run-Time

L'informazione essenziale per lo scope lessicale è stabilita al momento della compilazione/parsing del codice sorgente (**author-time**), e quindi non muta al momento dell'esecuzione (**run-time**). Lo scope globale e le dichiarazioni di scope delle singole funzioni o blocchi sono note al momento in cui JavaScript costruisce la mappa lessicale del programma.

**Regola chiave**: Una funzione "ricorda" dove è stata costruita e definita nello spazio e nel codice, senza essere in alcun modo influenzata dal punto o contesto da cui viene successivamente invocata.

### Esempio Pratico

```javascript
let messaggio = "Globale";

function mostraMessaggio() {
  // Questa funzione è dichiarata (scritta) all'interno dello scope globale
  // Il suo ambiente lessicale "esterno" è lo scope globale.
  console.log(messaggio);
}

function test() {
  let messaggio = "Locale";

  // Nonostante venga chiamata all'interno di test,
  // la funzione mostraMessaggio non accede a questo scope 'locale',
  // ma continua a cercare nell'ambiente in cui è stata DEFINITA.
  mostraMessaggio(); // Stampa "Globale" (non "Locale")
}

test();
```

Il comportamento del codice conferma l'approccio autorale: `mostraMessaggio()` e il suo ambiente interno referenziano le variabili scoperte esaminando la catena degli scope verso l'esterno in modo statico e lessicale, non basato sullo stack di chiamate dinamico.

## ⚠️ Immutabilità e pattern Lexical

Una volta completata la fase di lexing e costruite le entità sintattiche (funzioni e blocchi), i legami lessicali determinati per i relativi scope risultanti restano sigillati e chiusi. Questo è il principio esatto alla base delle **closures**.

L'accesso a variabili definite in un determinato scope continuerà a funzionare anche quando la funzione che vi accede verrà esportata (come return value o passata come callback) ed invocata fuori dallo scope originale.

```javascript
// La definizione del lexical scope consente le closures
function creaMoltiplicatore(fattore) {
  // 'fattore' è limitato al lexical scope di creaMoltiplicatore

  return function (numero) {
    // La funzione ritornata conserva l'accesso lessicale a 'fattore'
    return numero * fattore;
  };
}

let doppio = creaMoltiplicatore(2);
let triplo = creaMoltiplicatore(3);

console.log(doppio(5)); // 10
console.log(triplo(5)); // 15
```

L'uso di istruzioni obsolete quali `eval()` e `with` allo scopo di modificare in fase di esecuzione lo scope preesistente costituisce una forte de-ottimizzazione per il motore JavaScript ed è **fortemente sconsigliato**.
