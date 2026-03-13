# [[../../appunti-completi#39-scope-closure-e-illuminazione-enlightenment|Closure: Concetto Fondamentale]]

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

## ✅ Punti Chiave

1. **Le Closure sono ovunque** - Non devi "crearle", esistono già nel tuo codice
2. **Basate su Lexical Scope** - Se capisci lo scope lessicale, capisci le closure
3. **Funzioni "ricordano" il loro scope** - Anche quando eseguite altrove
4. **Previene Garbage Collection** - Lo scope rimane vivo finché la funzione esiste

## 🔗 Collegamenti

- [[../scope/lexical-scope-base|Scope Lessicale]] - La base delle closure
- [[../scope/nested-scope|Scope Annidato]] - Come le funzioni accedono agli scope esterni
- [[closure-transport-mechanisms|Meccanismi di Trasporto]] - Come trasportare funzioni fuori dallo scope
- [[closure-patterns|Pattern Pratici]] - Usi pratici delle closure
- [[../../appunti-completi#closure|Closure Completo]]

## 📚 Risorse

- "You Don't Know JS" - Scope & Closures, Chapter 5
- MDN: Closures

## 📌 Tag

#javascript #closure #scope #lexical-scope #garbage-collection
