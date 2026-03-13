# [[../../../appunti-completi#confusione-2-this-come-riferimento-allo-scope-lessicale|Soluzioni per Condividere Dati tra Funzioni]]

Poiché `this` e lo scope lessicale sono meccanismi separati che non possono essere fusi insieme, esistono pattern specifici e corretti da adottare a seconda del caso d'uso, evitando tentativi fallimentari di creare "ponti" inesistenti.

## ✅ Soluzione 1: Lexical Scope (Closure)

Utilizzare le closure è il modo corretto per permettere a una funzione di accedere alle variabili di un'altra funzione.

```javascript
function foo() {
  var a = 2;

  bar(); // Chiamata lessicale semplice

  function bar() {
    console.log(a); // Closure su scope di foo ✅
  }
}

foo(); // 2
```

**Quando usare**: Quando si ha bisogno di accedere a variabili di uno scope esterno e la struttura del codice permette di nidificare le funzioni in modo da creare la closure.

## ✅ Soluzione 2: this Binding (Oggetti)

Se l'intento è condividere stato tramite un oggetto comune e non tramite lo scope delle variabili locali, si deve strutturare il codice per operare su proprietà di un oggetto.

```javascript
var obj = {
  a: 2,

  foo: function () {
    this.bar(); // Chiamata metodo via this ✅
  },

  bar: function () {
    console.log(this.a); // Accesso proprietà via this ✅
  },
};

obj.foo(); // 2
```

**Quando usare**: Quando si lavora con proprietà di oggetti ed entrambe le funzioni sono metodi dello stesso oggetto (o vengono chiamate con un contesto opportunamente vincolato tramite `call`, `apply` o `bind`).

## ✅ Soluzione 3: Passare Parametri

L'approccio più funzionale e con meno side-effects per far dialogare funzioni indipendenti è passare esplicitamente i dati.

```javascript
function foo() {
  var a = 2;
  bar(a); // Passa esplicitamente il valore
}

function bar(value) {
  console.log(value); // Usa parametro ✅
}

foo(); // 2
```

**Quando usare**: Quando le funzioni sono indipendenti o appartenenti a scope e oggetti diversi e devono condividere dati senza creare accoppiamento implicito.
