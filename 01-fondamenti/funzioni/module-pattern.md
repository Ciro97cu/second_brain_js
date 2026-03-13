# [[../../appunti-completi#310-il-pattern-modulo-modules|Module Pattern (Moduli)]]

Oltre alle callback, esistono altri pattern di codice che sfruttano la potenza della Closure. Il più potente e significativo è senza dubbio il Modulo.

## Pattern Base: Non Ancora un Modulo

Inizialmente, si potrebbe considerare una funzione che incapsula dati e funzioni interne:

```javascript
function foo() {
  var something = "cool";
  var another = [1, 2, 3];

  function doSomething() {
    console.log(something);
  }

  function doAnother() {
    console.log(another.join(" ! "));
  }
}
```

Allo stato attuale, non vi è alcuna Closure osservabile. I dati e le funzioni sono semplicemente racchiusi nello scope di "foo".

## Revealing Module Pattern

Per trasformare questo codice in un Modulo, è necessario applicare il pattern del Revealing Module:

```javascript
function CoolModule() {
  var something = "cool";
  var another = [1, 2, 3];

  function doSomething() {
    console.log(something);
  }

  function doAnother() {
    console.log(another.join(" ! "));
  }

  return {
    doSomething: doSomething,
    doAnother: doAnother,
  };
}

var foo = CoolModule();

foo.doSomething(); // cool
foo.doAnother(); // 1 ! 2 ! 3
```

## Requisiti del Module Pattern

Analizzando il codice, emergono due requisiti fondamentali affinché il Module Pattern si verifichi:

1. **Deve esistere una funzione esterna** (nell'esempio CoolModule) che deve essere **invocata almeno una volta**. Ogni invocazione crea una nuova istanza del modulo.

2. **La funzione esterna deve restituire almeno una funzione interna**. Questo permette alla funzione restituita di mantenere una Closure sullo scope privato interno, garantendo l'accesso e la modifica dello stato privato.

**Importante**: Un oggetto che possiede metodi ma nessuna closure su dati privati non è un vero modulo in senso osservabile; è solo un oggetto con funzioni.

## Varianti del Modulo

### Singleton con IIFE

Una variante comune è la creazione di un Singleton, ottenuta trasformando la funzione del modulo in una IIFE:

```javascript
var foo = (function CoolModule() {
  var something = "cool";
  var another = [1, 2, 3];

  function doSomething() {
    console.log(something);
  }

  function doAnother() {
    console.log(another.join(" ! "));
  }

  return {
    doSomething: doSomething,
    doAnother: doAnother,
  };
})();

foo.doSomething(); // cool
foo.doAnother(); // 1 ! 2 ! 3
```

In questo caso, il modulo viene eseguito immediatamente e il valore di ritorno (l'API pubblica) viene assegnato direttamente alla variabile "foo".

### Moduli con Parametri

I moduli, essendo funzioni, possono anche accettare parametri per la configurazione:

```javascript
function CoolModule(id) {
  function identify() {
    console.log(id);
  }

  return {
    identify: identify,
  };
}

var foo1 = CoolModule("foo 1");
var foo2 = CoolModule("foo 2");

foo1.identify(); // "foo 1"
foo2.identify(); // "foo 2"
```

### API Pubblica Mutabile

Una variante potente prevede di mantenere un riferimento interno all'oggetto dell'API pubblica. Ciò consente al modulo di modificare la propria struttura (aggiungere/rimuovere metodi o cambiarne il valore) dall'interno durante l'esecuzione:

```javascript
var foo = (function CoolModule(id) {
  function change() {
    // modificare l'API pubblica
    publicAPI.identify = identify2;
  }

  function identify1() {
    console.log(id);
  }

  function identify2() {
    console.log(id.toUpperCase());
  }

  var publicAPI = {
    change: change,
    identify: identify1,
  };

  return publicAPI;
})("foo module");

foo.identify(); // foo module
foo.change();
foo.identify(); // FOO MODULE
```

## ✅ Punti Chiave

1. **Due requisiti essenziali** - Funzione esterna invocata + ritorno di funzione interna
2. **Closure per privacy** - Dati privati mantenuti vivi dalla closure
3. **Singleton con IIFE** - Esecuzione immediata per istanza unica
4. **Configurazione con parametri** - Moduli flessibili e riusabili
5. **API mutabile** - Riferimento interno permette modifiche runtime

## 🔗 Collegamenti

- [[closure-concept|Concetto di Closure]] - Base del module pattern
- [[iife|IIFE]] - Per creare singleton
- [[module-dependency-managers|Dependency Managers]] - Gestori moduli moderni
- [[../scope/module-management|ES6 Modules]] - Moduli nativi JavaScript
- [[../../appunti-completi#310-il-pattern-modulo-modules|Module Pattern Completo]]

## 📚 Risorse

- "You Don't Know JS" - Scope & Closures
- JavaScript Design Patterns

## 📌 Tag

#javascript #module-pattern #closure #revealing-module #iife #singleton #private-data

- **Manutenibilità** → Modifiche interne senza impatto esterno

## Riepilogo

Il **Module Pattern** sfrutta le closure per creare **stato privato** e un'**interfaccia pubblica**. È un pattern fondamentale pre-ES6 per organizzare il codice, ora sostituito dai **moduli ES6** (`import`/`export`) che offrono la stessa separation of concerns con sintassi nativa.

## Collegamenti

- [[closure]] - Le closure permettono il Module Pattern
- [[iife]] - IIFE per creare singleton modules
- [[funzioni]] - Funzioni come factory
- [[../scope/scope]] - Scope privato e pubblico
