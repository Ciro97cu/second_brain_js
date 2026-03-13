# [[../../../appunti-completi#algoritmo-decisionale-di-this|Algoritmo Decisionale di this]]

Quando **più di una regola** potrebbe applicarsi allo stesso call-site, è necessario conoscere l'**ordine di precedenza** per determinare quale viene applicata.

## Gerarchia Completa

Le regole seguono un ordine di precedenza specifico, dal più al meno forte:

1. `new` binding (massima priorità)
2. _Explicit binding_ (`call`, `apply`, `bind`)
3. _Implicit binding_ (`obj.method()`)
4. _Default binding_ (minima priorità)

La priorità garantisce che `new` vinca sempre, mentre il _default binding_ perde invariabilmente.

## Algoritmo

Per determinare il logico target del `this`, si consiglia di rispondere a queste domande in sequenza top-down:

### 1. La funzione è chiamata con `new`?

```javascript
var obj = new foo();
```

In caso affermativo, `this` assume il valore del nuovo oggetto generato.

### 2. La funzione è chiamata con binding esplicito?

```javascript
foo.call(obj);
// oppure
var bar = foo.bind(obj);
bar();
```

Se applicato, `this` è l'oggetto specificato esplicitamente.

### 3. La funzione è chiamata come metodo (`obj.foo()`)?

```javascript
obj.foo();
```

Se la risposta è positiva, `this` corrisponde all'oggetto contenitore (binding implicito).

### 4. Altrimenti (Default)

```javascript
foo();
```

Senza un contesto vincolante, `this` è associato al global object (o equivale a `undefined` in _strict mode_).

## Diagramma di Flusso

```text
┌──────────────────────┐
│ new foo()?           │
└──────┬───────────────┘
       │ Sì → this = nuovo oggetto creato
       │ No ↓
┌──────────────────────┐
│ call/apply/bind?     │
└──────┬───────────────┘
       │ Sì → this = oggetto specificato
       │ No ↓
┌──────────────────────┐
│ obj.foo()?           │
└──────┬───────────────┘
       │ Sì → this = obj (contenitore)
       │ No ↓
┌──────────────────────┐
│ Default              │
└──────┬───────────────┘
       │ → this = global (o undefined in strict)
```
