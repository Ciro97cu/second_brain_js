# [[../../appunti-completi#310-il-pattern-modulo-modules|Module Pattern Variants]]

Il Module Pattern può essere implementato in varie forme per adattarsi a diverse esigenze progettuali. Tra queste, i moduli con parametri e i moduli con API mutabile offrono grande flessibilità.

## Moduli con Parametri

Poiché i moduli sono definiti tramite funzioni, possono accettare parametri durante l'inizializzazione. Questo permette di configurare il comportamento del modulo o di dotarlo di dati iniziali.

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

## API Pubblica Mutabile

Spesso è utile poter modificare la struttura dell'API pubblica del modulo dall'interno, ad esempio aggiungendo, rimuovendo o sostituendo metodi durante l'esecuzione. Per fare ciò, si mantiene un riferimento all'oggetto API nello scope interno.

```javascript
var foo = (function CoolModule(id) {
  function change() {
    // modifica dell'API pubblica
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

foo.identify(); // "foo module"
foo.change();
foo.identify(); // "FOO MODULE"
```
