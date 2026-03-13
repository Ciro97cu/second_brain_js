# [[../../../appunti-completi#311-lidentificatore-this|Implicit Binding: Perdita del Contesto]]

Il problema più noto e insidioso legato all'implicit binding è noto come **Implicitly Lost** (perdita implicita). Quando viene estratto o passato un riferimento a una funzione che ci si aspetta agisca come un metodo (con il suo binding "intatto"), tale legame viene facilmente "spezzato", facendo ricadere la chiamata sulla [[this-binding-default|Default Binding (Regola 1)]]. Di conseguenza, `this` diventerà l'oggetto globale o `undefined` se si utilizza strict mode.

Questo accade perché in JavaScript, le funzioni non sono "possedute" dall'oggetto stesso, e il contesto `this` dipende esclusivamente dal modo in cui la funzione viene invocata al momento del **call-site**.

## Perdita per Assegnazione di Riferimento

L'evento più basilare di perdita avviene quando si assegna il metodo a una variabile semplice.

```javascript
function foo() {
  console.log(this.a);
}

const obj = {
  a: 2,
  foo: foo,
};

const bar = obj.foo; // Viene passato solo un riferimento alla funzione!

var a = "oops, global";

bar(); // "oops, global" (Default binding applicato)
```

In questo caso, `bar = obj.foo` crea una copia del *riferimento* alla funzione originale. Essendo invocata tramite `bar()`, questa risulta essere una chiamata normale, scollegata da qualsiasi riferimento all'oggetto `obj`.

## L'Assegnazione per Callback e Temporizzatori

Come caso particolare della perdita per assegnamento, il passaggio come argomento (inclusi i callback) rappresenta un'allocazione implicita e sortisce invariabilmente lo stesso effetto.

```javascript
function foo() {
  console.log(this.a);
}

function doFoo(fn) {
  fn(); // <-- Call-site: chiamata diretta, default binding.
}

const obj = {
  a: 2,
  foo: foo,
};

var a = "oops, global";
doFoo(obj.foo); // "oops, global"
```

Questa stessa problematica emerge ogni volta che si adoperano i temporizzatori integrati del browser, come `setTimeout`, il quale esegue, sotto al cofano, analoghe chiamate dirette al riferimento fornito in ingresso.

```javascript
var obj = {
  a: 2,
  foo: function () {
    console.log(this.a);
  },
};

var a = "oops, global";

setTimeout(obj.foo, 100); // "oops, global"
// All'interno di setTimeout si verificherà: fn()
```

## Strumenti ed Estrazioni Moderni: Array e Destrutturazione

La perdita di correlazione occorre, allo stesso modo, quando una funzione è depositata su una struttura d'appoggio eterogenea, o estratta in modo esplicito grazie alla destrutturazione.

**Metodi di iterazione su Array**
Nel caso di `.forEach()` o simili e array puri (senza bind), il binding non viene salvaguardato.
```javascript
const obj = {
  a: 2,
  foo: function () {
    console.log(this.a);
  },
};

const methods = [obj.foo]; // ← Perdita di binding!
var a = "global";

methods[0](); // "global" - come: const fn = obj.foo; fn();
```

**Assegnazione da destrutturazione (Destructuring)**
Istanziando le property per via destrutturata su variabili autonome, avviene una normale assegnazione.
```javascript
const obj = {
  a: 2,
  foo: function () {
    console.log(this.a);
  },
};

const { foo } = obj; // Assegnazione della proprietà come semplice riferimento!
var a = "global";

foo(); // "global"
```

## Rimediare

Per affrontare queste anomalie si può far riferimento a:
- **Arrow Functions**: per consolidare `this` rispetto al blocco in modo lessicale.
- **`.bind()`**: producendo copie forzate del proprio function wrapper (Explicit binding).

Vedere [[this-binding-problems]] per approfondimenti specifici alle problematiche dei callback.

---
**Tags**: `#javascript` `#this` `#implicit-lost` `#binding` `#callback`
