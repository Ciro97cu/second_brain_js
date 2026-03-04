# [[../../appunti-completi#closure|Closure (Chiusura)]]

## 🎯 Enlightenment: Vedere la Matrix

Per molti sviluppatori, comprendere la **Closure** sembra un traguardo difficile, una sorta di "nirvana" che richiede sforzi immensi. Tuttavia, il segreto fondamentale è che **la Closure è onnipresente in JavaScript**; bisogna solo imparare a riconoscerla.

**Non si tratta di uno strumento opzionale** che richiede una nuova sintassi speciale o l'apprendimento di pattern complessi. Le Closures non sono nemmeno un'arma da "padroneggiare" con fatica. **Esse si verificano naturalmente e automaticamente** come risultato della scrittura di codice che si affida allo **Scope Lessicale**.

Le Closures vengono create e utilizzate continuamente nel codice, spesso senza che lo sviluppatore se ne renda conto intenzionalmente. L'obiettivo non è quindi imparare a crearle da zero, ma **acquisire il contesto mentale corretto per riconoscere** le Closures che stanno già avvenendo nel proprio codice e sfruttarle a proprio vantaggio.

**Comprendere le Closures è paragonabile al momento in cui Neo vede la Matrix per la prima volta**: erano sempre lì, ma ora sono finalmente visibili.

## 💡 Definizione Tecnica

**Closure**: Una funzione è in grado di **ricordare e accedere al proprio Lexical Scope** (lo scope definito al momento della scrittura del codice) **anche quando quella funzione viene eseguita al di fuori del suo Lexical Scope originario**.

In altre parole:

- Una funzione **mantiene un riferimento vivo** alle variabili del suo scope esterno
- Questo riferimento persiste **anche dopo che la funzione esterna ha terminato l'esecuzione**
- La funzione può essere **eseguita ovunque**, ma ricorderà sempre il suo scope originale

## 💻 Osservare la Closure in Azione

### Scope Annidato: Non È (Ancora) Closure

```javascript
function foo() {
  var a = 2;

  function bar() {
    console.log(a); // 2
  }

  bar();
}

foo();
```

Da un punto di vista puramente accademico, si afferma che la funzione `bar()` possiede una **Closure sullo scope di `foo()`**. Tuttavia, in questo esempio, la Closure **non è direttamente osservabile**: quello che si vede è semplicemente l'applicazione delle **regole di accesso lessicale standard**. La funzione viene eseguita nello stesso scope in cui è stata definita.

### Closure Vera: Funzione Eseguita Fuori dal Suo Scope

Per osservare veramente la Closure in azione, è necessario che la **funzione interna venga eseguita in un contesto diverso** da quello in cui è stata dichiarata:

```javascript
function foo() {
  var a = 2;

  function bar() {
    console.log(a);
  }

  return bar; // Restituisce la funzione (non la esegue!)
}

var baz = foo(); // baz contiene ora la funzione bar

baz(); // 2 - ⚡ CLOSURE!
```

**Cosa succede qui?**

1. `foo()` viene eseguita e restituisce la funzione `bar` (senza eseguirla)
2. Assegniamo `bar` alla variabile `baz`
3. Eseguiamo `baz()` (che è `bar`)
4. **Magia**: `bar()` accede ancora a `a`, anche se `foo()` ha già terminato!

### Perché `a` Non Viene Garbage-Collected?

Il comportamento standard dell'Engine prevede che, una volta eseguita una funzione, la sua memoria venga liberata dal **Garbage Collector**. Ci si aspetterebbe che lo scope interno di `foo` sparisca dopo che `foo()` ha terminato.

**Tuttavia, la Closure impedisce che questo accada**. Lo scope interno rimane **"vivo"** perché `bar()` (ora referenziata da `baz`) lo sta ancora utilizzando.

La funzione `baz` viene invocata molto tempo dopo e **ben al di fuori del suo Lexical Scope originario** (che era dentro `foo`), eppure riesce ancora ad accedere alla variabile `a`. Questo **riferimento persistente allo scope originario** è ciò che viene chiamato **Closure**.

## 🚀 Trasportare Funzioni Fuori dal Loro Scope

La Closure funziona **indipendentemente da come la funzione viene trasportata** al di fuori del suo scope. Non importa se viene restituita come valore di ritorno o passata come argomento:

### Passare come Argomento

```javascript
function foo() {
  var a = 2;

  function baz() {
    console.log(a); // 2
  }

  bar(baz); // Passa baz come argomento
}

function bar(fn) {
  fn(); // ⚡ CLOSURE! - Esegue baz, che ricorda 'a'
}

foo();
```

**Cosa succede**:

1. `foo()` definisce `a` e `baz()`
2. `foo()` passa `baz` alla funzione `bar` (che è fuori dallo scope di `foo`)
3. `bar` esegue `fn()` (che è `baz`)
4. `baz()` accede ancora a `a`, anche se eseguita dentro `bar`

### Callback e Timer

```javascript
function wait(message) {
  setTimeout(function timer() {
    console.log(message);
  }, 1000);
}

wait("Hello, closure!"); // Dopo 1 secondo: "Hello, closure!"
```

La funzione `timer` ha una **closure su `message`**. Anche dopo che `wait()` ha terminato, `timer` ricorda `message` e può stamparlo 1 secondo dopo.

### Event Handlers

```javascript
function setupButton(buttonId) {
  var clickCount = 0;

  document.getElementById(buttonId).addEventListener("click", function () {
    clickCount++;
    console.log(`Button clicked ${clickCount} times`);
  });
}

setupButton("myButton");
```

Il callback dell'evento ha una **closure su `clickCount`**. Ogni click incrementa e stampa il contatore, anche se `setupButton` ha già terminato.

## 📦 Esempio Base: Factory Function

```javascript
function makeAdder(x) {
  function add(y) {
    return x + y; // 'add' ricorda 'x'
  }
  return add;
}

let plusOne = makeAdder(1); // Closure che ricorda x = 1
let plusTen = makeAdder(10); // Closure che ricorda x = 10

console.log(plusOne(3)); // 4  (1 + 3)
console.log(plusTen(13)); // 23 (10 + 13)
```

**Come funziona**: Ogni chiamata a `makeAdder()` crea un **nuovo scope** con una propria copia di `x`. La funzione `add` restituita "ricorda" il valore di `x` del suo scope, anche dopo che `makeAdder` ha terminato.

## Uso Pratico: Dati Privati

Le closure permettono di creare **variabili private** in JavaScript:

```javascript
function counter() {
  let count = 0; // Variabile privata

  return {
    increment: function () {
      count++;
      return count;
    },
    decrement: function () {
      count--;
      return count;
    },
    getValue: function () {
      return count;
    },
  };
}

let myCounter = counter();
console.log(myCounter.increment()); // 1
console.log(myCounter.increment()); // 2
console.log(myCounter.getValue()); // 2

// ❌ Non posso accedere direttamente a count
console.log(myCounter.count); // undefined
```

## Closure nei Loop (Problema Classico)

Un errore comune è non comprendere come le closure si comportano nei loop:

```javascript
// ❌ Problema: tutte le funzioni condividono lo stesso 'i'
for (var i = 1; i <= 3; i++) {
  setTimeout(function () {
    console.log(i); // 4, 4, 4 (non 1, 2, 3!)
  }, i * 1000);
}

// ✅ Soluzione 1: Usa let (block scope)
for (let i = 1; i <= 3; i++) {
  setTimeout(function () {
    console.log(i); // 1, 2, 3
  }, i * 1000);
}

// ✅ Soluzione 2: Crea closure esplicita
for (var i = 1; i <= 3; i++) {
  (function (j) {
    setTimeout(function () {
      console.log(j); // 1, 2, 3
    }, j * 1000);
  })(i);
}
```

## 🎓 Sintesi del Concetto

**In sintesi**, qualunque sia il mezzo utilizzato per trasportare una funzione fuori dal suo Lexical Scope (return, argomento, callback, event handler), essa **manterrà un riferimento allo scope in cui è stata originariamente dichiarata** (al momento della scrittura, o "author-time") e lo utilizzerà **ovunque venga eseguita**.

Le **closure** permettono:

- Funzioni che **ricordano** il loro scope lessicale
- Creazione di **variabili private** (incapsulamento)
- Implementazione di **factory functions** e **module pattern**
- **Garbage Collector consapevole**: mantiene vivo lo scope necessario

**Regola chiave**: Una funzione ha sempre accesso alle variabili del suo scope esterno, anche dopo che quello scope ha terminato l'esecuzione. Questo non è un bug, è una feature fondamentale di JavaScript.

## ✅ Punti Chiave

1. **Le Closure sono ovunque** - Non devi "crearle", esistono già nel tuo codice
2. **Basate su Lexical Scope** - Se capisci lo scope lessicale, capisci le closure
3. **Funzioni "ricordano" il loro scope** - Anche quando eseguite altrove
4. **Previene Garbage Collection** - Lo scope rimane vivo finché la funzione esiste
5. **Trasportabili in qualsiasi modo** - Return, argomenti, callbacks, event handlers

## 🔗 Collegamenti

- [[funzioni]] - Le funzioni come first-class citizens
- [[../scope/lexical-scope-base|Scope Lessicale]] - La base delle closure
- [[../scope/nested-scope|Scope Annidato]] - Come le funzioni accedono agli scope esterni
- [[iife]] - IIFE per creare scope isolati
- [[module-pattern]] - Module Pattern basato su closure
- [[../../appunti-completi#closure|Closure Completo]]

## 📚 Risorse

- MDN: Closures
- "You Don't Know JS" - Scope & Closures, Chapter 5

## 📌 Tag

#javascript #closure #scope #lexical-scope #garbage-collection #callbacks #event-handlers #private-variables #factory-functions
