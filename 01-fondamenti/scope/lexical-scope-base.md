# [[../../appunti-completi#scope-lessicale-lexical-scope|Scope Lessicale (Lexical Scope)]]

Lo **scope lessicale** determina l'accesso alle variabili in base a **dove il codice è scritto** (author-time), non dove viene eseguito (run-time).

## 🎯 Concetto Chiave

JavaScript usa lo **scope lessicale**: lo scope di una funzione è determinato dalla sua **posizione nel codice sorgente**, non da dove o come viene invocata. Questa struttura è definita durante la fase di **lexing** (compilazione) e rimane **immutabile**.

### Author-Time vs Run-Time

Lo scope lessicale è determinato **quando scrivi il codice**, non quando viene eseguito.

```javascript
// Scope determinato da DOVE è SCRITTA la funzione
let messaggio = "Globale";

function mostraMessaggio() {
  // Questa funzione è SCRITTA nello scope globale
  console.log(messaggio);
}

function test() {
  let messaggio = "Locale";
  mostraMessaggio(); // "Globale" (non "Locale")
}

test();
// mostraMessaggio() cerca 'messaggio' dove è STATA DEFINITA (globale),
// NON dove viene CHIAMATA (test)
```

**Regola chiave**: La funzione "ricorda" dove è stata definita, non dove viene invocata.

## 🔍 Lexical vs Dynamic Scope

JavaScript usa **solo** lexical scope (come la maggior parte dei linguaggi moderni).

```javascript
let valore = "globale";

function mostraValore() {
  console.log(valore);
}

function test() {
  let valore = "locale";
  mostraValore(); // Cosa stampa?
}

test();
// LEXICAL SCOPE (JavaScript): "globale"
// → mostraValore() è DEFINITA nello scope globale

// DYNAMIC SCOPE (ipotetico): "locale"
// → mostraValore() è CHIAMATA da test()
```

### Differenza Fondamentale

| Tipo        | Basato su                     | Usato in                    |
| ----------- | ----------------------------- | --------------------------- |
| **Lexical** | **Dove** il codice è scritto  | JavaScript, C, Java, Python |
| **Dynamic** | **Dove** il codice è chiamato | Bash, alcuni Lisp           |

```javascript
// Esempio pratico: closure con lexical scope
function creaContatore(iniziale) {
  let contatore = iniziale;

  return function incrementa() {
    // 'incrementa' ricorda il SUO scope lessicale
    contatore++;
    return contatore;
  };
}

let contatore1 = creaContatore(0);
let contatore2 = creaContatore(100);

console.log(contatore1()); // 1 (ricorda il SUO scope lessicale)
console.log(contatore1()); // 2
console.log(contatore2()); // 101 (ricorda il SUO diverso scope lessicale)
console.log(contatore2()); // 102

// Ogni funzione 'incrementa' ricorda dove è stata CREATA
```

## ⚠️ Immutabilità dello Scope Lessicale

Una volta che il codice è stato analizzato (fase di lexing), la struttura dello scope **non cambia mai**.

```javascript
function esterna() {
  let x = 10;

  function interna() {
    // 'interna' può accedere a 'x' perché è SCRITTA DENTRO 'esterna'
    console.log(x); // 10
  }

  return interna;
}

let fn = esterna();
fn(); // 10 - 'interna' ricorda dove è stata DEFINITA
```

⚠️ **Eccezioni deprecate**: `eval()` e `with` possono modificare lo scope a runtime, ma sono **fortemente sconsigliati**.

```javascript
// ❌ EVITA (modifica scope a runtime)
eval("var x = 10"); // Crea 'x' dinamicamente (pericoloso!)

// ✅ PREFERISCI (scope statico e prevedibile)
let x = 10; // Dichiarazione esplicita lessicale
```

## ✅ Best Practices

**Sfrutta lo scope lessicale per le closures**: È la base dei pattern avanzati.

```javascript
function creaMultiplicatore(fattore) {
  // 'fattore' fa parte dello scope lessicale
  return function (numero) {
    return numero * fattore; // Accede sempre al SUO 'fattore'
  };
}

let doppio = creaMultiplicatore(2);
let triplo = creaMultiplicatore(3);

console.log(doppio(5)); // 10
console.log(triplo(5)); // 15
```

**Comprendi la differenza tra definizione e invocazione**: La posizione nel codice conta.

```javascript
let config = { tema: "chiaro" };

function mostraConfig() {
  console.log(config); // Cerca 'config' dove è DEFINITA
}

function eseguiInAltroContesto() {
  let config = { tema: "scuro" };
  mostraConfig(); // { tema: "chiaro" } (non "scuro")
}

eseguiInAltroContesto();
```

**Evita `eval()` e `with`**: Rendono il codice imprevedibile e lento.

## 🔗 Collegamenti

- [[scope-bubbles]] - Visualizzazione e processo di look-up
- [[scope-properties]] - Distinzione scope vs proprietà oggetti
- [[scope-chain]] - Catena degli scope
- [[nested-scope]] - Scope annidati in pratica

## 📚 Risorse Esterne

- [MDN: Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) - Scope lessicale nelle closures
- [YDKJS: Scope](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch1.md) - Approfondimento scope lessicale

## 📌 Note Aggiuntive

- Lo **scope lessicale** è anche chiamato **static scope** (statico, determinato alla compilazione)
- Il 99.9% dei linguaggi moderni usa lexical scope
- **Dynamic scope** è rarissimo (Bash, alcuni dialetti Lisp)
- Lo scope lessicale è **immutabile** dopo la fase di parsing
- Le closures dipendono completamente dallo scope lessicale
