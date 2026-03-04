# [[../../appunti-completi#310-il-pattern-modulo-modules|Moduli Moderni: Dependency Managers]]

## Gestori di Dipendenze

Diversi gestori e caricatori di dipendenze (dependency managers/loaders) incapsulano il pattern del modulo in API più amichevoli e strutturate. Senza analizzare una libreria specifica, è utile esaminare un semplice Proof of Concept per comprendere come questi strumenti operino "sotto il cofano".

## Implementazione Proof of Concept

```javascript
var MyModules = (function Manager() {
  var modules = {};

  function define(name, deps, impl) {
    for (var i = 0; i < deps.length; i++) {
      deps[i] = modules[deps[i]];
    }
    modules[name] = impl.apply(impl, deps);
  }

  function get(name) {
    return modules[name];
  }

  return {
    define: define,
    get: get,
  };
})();
```

### Come Funziona

La parte chiave di questo codice è l'istruzione `modules[name] = impl.apply(impl, deps)`. Questa riga:

1. Invoca la funzione "wrapper" che definisce il modulo
2. Passa le dipendenze risolte come parametri
3. Memorizza il valore restituito (l'API pubblica del modulo) in una lista interna gestita per nome

## Utilizzo del Gestore

Ecco come questo gestore potrebbe essere utilizzato per definire dei moduli:

```javascript
MyModules.define("bar", [], function () {
  function hello(who) {
    return "Let me introduce: " + who;
  }

  return {
    hello: hello,
  };
});

MyModules.define("foo", ["bar"], function (bar) {
  var hungry = "hippo";

  function awesome() {
    console.log(bar.hello(hungry).toUpperCase());
  }

  return {
    awesome: awesome,
  };
});

var bar = MyModules.get("bar");
var foo = MyModules.get("foo");

console.log(bar.hello("hippo")); // Let me introduce: hippo
foo.awesome(); // LET ME INTRODUCE: HIPPO
```

### Analisi dell'Esempio

Si osserva che entrambi i moduli, "foo" e "bar", sono definiti tramite una funzione che restituisce un'API pubblica. Il modulo "foo" riceve addirittura l'istanza di "bar" come parametro di dipendenza e può utilizzarla liberamente.

## Nessuna Magia

L'aspetto fondamentale da cogliere è che **non esiste alcuna "magia" particolare** dietro i gestori di moduli. Essi soddisfano semplicemente le due caratteristiche essenziali del pattern:

1. Invocano un wrapper di definizione della funzione
2. Conservano il suo valore di ritorno come API del modulo

In sintesi, i moduli rimangono moduli, anche se avvolti da strumenti che ne facilitano la gestione.

## ✅ Punti Chiave

1. **Dependency injection** - Le dipendenze vengono risolte e iniettate automaticamente
2. **Registro centrale** - Tutti i moduli sono memorizzati in un oggetto `modules`
3. **API semplice** - `define()` per registrare, `get()` per recuperare
4. **Nessuna magia** - Sotto il cofano sono sempre closure e module pattern
5. **Base per librerie** - RequireJS, AMD, etc. seguono questo principio

## 🔗 Collegamenti

- [[module-pattern|Module Pattern]] - Fondamenti del pattern
- [[../scope/module-management|ES6 Modules]] - Sistema moduli nativo
- [[closure-concept|Closure]] - Meccanismo alla base dei moduli
- [[../../appunti-completi#310-il-pattern-modulo-modules|Module Pattern Completo]]

## 📚 Risorse

- RequireJS Documentation
- AMD (Asynchronous Module Definition)
- "You Don't Know JS" - Scope & Closures

## 📌 Tag

#javascript #module-loader #dependency-manager #amd #requirejs #module-pattern #dependency-injection
