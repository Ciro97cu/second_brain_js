# Barare con lo Scope Lessicale (Cheating Lexical Scope) [[../../appunti-completi#barare-con-lo-scope-lessicale-cheating-lexical|📚]]

## 🎯 Concetto

Lo scope lessicale è normalmente **immutabile** e determinato dalla posizione del codice nel file sorgente (**author-time**). JavaScript offre due meccanismi deprecati che permettono di "barare" modificando lo scope a **runtime**: `eval()` e `with`.

**Perché "barare"**: Questi meccanismi violano il principio fondamentale che lo scope è determinato staticamente, permettendo modifiche dinamiche durante l'esecuzione.

**Avviso**: Entrambi sono **fortemente sconsigliati** e `with` è completamente vietato in strict mode.

## 💻 eval() - Esecuzione Dinamica di Codice

### Sintassi Base

`eval()` esegue codice arbitrario **a runtime**, modificando dinamicamente lo scope lessicale:

```javascript
function foo(str, a) {
  eval(str); // modifica lo scope a runtime!
  console.log(a, b);
}

var b = 2;
foo("var b = 3;", 1); // 1, 3 - eval ha creato b nello scope di foo!
```

`eval()` esegue la stringa come se fosse codice scritto in quella posizione, creando o modificando variabili nello scope corrente.

### eval() in Strict Mode

In **strict mode**, `eval()` ha il proprio scope lessicale **isolato**:

```javascript
function foo(str) {
  "use strict";
  eval(str);
  console.log(a); // ReferenceError: a is not defined
}

foo("var a = 2");
```

La dichiarazione dentro `eval()` non "inquina" lo scope circostante - rimane confinata.

### Funzioni Simili a eval()

Altre funzioni accettano stringhe di codice ed eseguono runtime evaluation:

```javascript
// setTimeout / setInterval con stringhe (DEPRECATO)
setTimeout("console.log('Hello')", 1000); // ❌ SCONSIGLIATO

// new Function() (leggermente più sicuro, ma comunque deprecato)
var add = new Function("a", "b", "return a + b"); // ❌ SCONSIGLIATO
console.log(add(2, 3)); // 5
```

**Best Practice**: Usare sempre callback function anziché stringhe di codice.

### Pericoli di eval()

1. **Sicurezza**: Injection attacks se si esegue input utente
2. **Debugging**: Codice dinamico difficile da tracciare
3. **Performance**: Engine non può ottimizzare (vedi sotto)
4. **Manutenibilità**: Comportamento imprevedibile

```javascript
// PERICOLOSO - Input utente
var userInput = getUserInput(); // Potrebbe contenere codice malevolo
eval(userInput); // ❌ MAI FARE QUESTO!
```

## 🔀 with - Scope Temporaneo da Oggetto

### Sintassi Base

`with` è un costrutto **deprecato** che crea uno scope temporaneo da un oggetto:

```javascript
var obj = {
  a: 1,
  b: 2,
  c: 3,
};

// Senza with - ripetitivo
obj.a = 2;
obj.b = 3;
obj.c = 4;

// Con with - apparentemente più pulito
with (obj) {
  a = 3;
  b = 4;
  c = 5;
}

console.log(obj); // { a: 3, b: 4, c: 5 }
```

Sembra pratico per l'accesso ripetuto alle proprietà, ma nasconde pericoli enormi.

### Il Pericolo: Variabili Globali Accidentali

```javascript
function foo(obj) {
  with (obj) {
    a = 2; // Cosa succede qui?
  }
}

var o1 = { a: 3 };
var o2 = { b: 3 };

foo(o1);
console.log(o1.a); // 2 - proprietà modificata ✅

foo(o2);
console.log(o2.a); // undefined - o2 non ha 'a'
console.log(a); // 2 - ⚠️ VARIABILE GLOBALE ACCIDENTALE!
```

**Problema Critico**: Se l'oggetto non ha la proprietà richiesta, `with` crea una **variabile globale** invece di generare un errore!

### Come with Modifica lo Scope

```javascript
var obj = { a: 1 };

with (obj) {
  // Lo scope lookup parte da "obj"
  // 1. Cerca "a" in obj → ✅ TROVATO: obj.a
  console.log(a); // 1

  // 2. "b" non è in obj → cerca nello scope esterno
  // console.log(b); // ReferenceError (se non esiste globalmente)
  b = 2; // ⚠️ Crea variabile GLOBALE!
}

console.log(b); // 2 (globale accidentale)
```

### with in Strict Mode

```javascript
"use strict";

var obj = { a: 1 };
// with (obj) { // ❌ SyntaxError: Strict mode code may not include a with statement
//   a = 2;
// }
```

**Strict mode vieta completamente `with`**.

### Pericoli di with

1. **Variabili Globali Accidentali**: Il pericolo più critico
2. **Performance Devastante**: Engine non può ottimizzare
3. **Leggibilità**: Impossibile capire quale scope contiene una variabile
4. **Debugging**: Comportamento imprevedibile e difficile da tracciare

## ⚡ Impatto sulle Performance

Sia `eval()` che `with` **distruggono le ottimizzazioni** dell'engine JavaScript.

### Perché sono Lenti

```javascript
// L'engine NON PUÒ ottimizzare questo codice
function foo(obj) {
  with (obj) {
    a = b; // Quale scope? obj? globale? locale?
  }
}

// O questo
function bar(code) {
  eval(code); // Cosa esegue? Quali variabili modifica?
}
```

**Motivo**: L'engine deve assumere che lo scope possa cambiare a runtime, quindi:

- ❌ Non può fare **scope lookup statico** (deve controllare a runtime)
- ❌ Non può fare **inline caching** (nomi variabili imprevedibili)
- ❌ Non può applicare **ottimizzazioni lexical scope-based**
- ❌ Non può applicare **minification** aggressiva

### Effetto a Cascata

**Regola Critica**: Se anche **una sola funzione** usa `eval()` o `with`, l'**intero scope gerarchico superiore** non può essere ottimizzato.

```javascript
function padre() {
  var x = 10;

  function figlio() {
    eval("var y = 20;"); // ⚠️ Anche solo questa riga...
  }

  // ...impedisce ottimizzazioni in TUTTA la funzione padre!
}
```

Il costo in performance può essere **10-100x più lento** rispetto a codice normale.

## ✅ Alternative Moderne

### Invece di eval()

```javascript
// ❌ Vecchio approccio
eval("console.log('Hello')");

// ✅ Approccio moderno
const code = () => console.log("Hello");
code();

// ❌ Per accesso a proprietà dinamiche
var obj = { a: 1, b: 2 };
eval("console.log(obj." + prop + ")");

// ✅ Bracket notation
console.log(obj[prop]);

// ❌ Per calcoli dinamici
var result = eval("2 + 2 * 3");

// ✅ Parser dedicati (es. math.js, expr-eval)
// O Function constructor (più sicuro di eval)
var calc = new Function("return 2 + 2 * 3");
var result = calc(); // 8
```

### Invece di with

```javascript
var obj = { a: 1, b: 2, c: 3 };

// ❌ con with (deprecato)
with (obj) {
  console.log(a, b, c);
}

// ✅ Destructuring (ES6+)
const { a, b, c } = obj;
console.log(a, b, c);

// ✅ Accesso esplicito
obj.a = 2;
obj.b = 3;
obj.c = 4;

// ✅ Se hai molte proprietà
const temp = obj;
temp.a = 2;
temp.b = 3;
temp.c = 4;
```

Il **destructuring** è più esplicito, sicuro e completamente ottimizzabile dall'engine.

## ⚠️ Quando (Forse) Usarli

I casi in cui è **realmente necessario** generare codice dinamicamente sono **estremamente rari**:

- Template engines server-side (ma usa librerie dedicate)
- REPL/Console interattive (ambiente controllato)
- Code generation tools (build time, non runtime)

In tutti questi casi, esplora alternative prima di ricorrere a `eval()` o `with`.

## 🔗 Concetti Correlati

- [[lexical-scope-base|Scope Lessicale]] - Il principio che viene violato
- [[scope-window|Variabili Globali]] - Global leak con with
- [[scope-vs-properties|Scope vs Proprietà]] - Differenza fondamentale
- [[nested-scope|Scope Chain]] - Come with/eval la modificano
- [[../../appunti-completi#barare-con-lo-scope-lessicale-cheating-lexical|Barare con Scope Lessicale Completo]]

## 📚 Risorse

- MDN: eval() is evil
- MDN: with statement (deprecated)
- "You Don't Know JS" - Scope & Closures, Chapter 2

## 📌 Tag

#javascript #scope #eval #with #deprecated #security #performance #lexical-scope #strict-mode #global-leak
