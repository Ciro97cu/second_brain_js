# [[../../../appunti-completi#311-lidentificatore-this|Perdita del Binding di this]]

Uno dei problemi più comuni in JavaScript è la **perdita del binding di `this`** quando si passano funzioni come callback o event handler. Questo accade perché il call-site determina `this`, non il punto di definizione della funzione.

## Il Problema: Callback Perde this

Quando passi un metodo come callback, estrai il riferimento alla funzione dal suo oggetto. Il call-site diventa un'invocazione normale senza contesto, ricadendo nel **default binding** (globale o `undefined`).

```javascript
var obj = {
  value: 42,
  getValue: function () { console.log(this.value); }
};

obj.getValue(); // 42 (implicit binding)

// Passato come callback
setTimeout(obj.getValue, 100); // undefined (o errore in strict mode)
// Equivalente a: var fn = obj.getValue; fn();
```

## Soluzioni

Ci sono tre modi principali per risolvere la perdita di binding.

### 1. Arrow Function Wrapper

Le arrow functions mantengono il contesto del lexical scope (dove sono state definite).

```javascript
// setTimeout
setTimeout(() => obj.getValue(), 100); // 42

// Event handler (mantieni this del contesto esterno)
element.addEventListener("click", () => button.handleClick());
```

### 2. Hard Binding con bind()

Il metodo `bind()` crea una nuova funzione con il `this` forzato all'oggetto specificato.

```javascript
var boundGetValue = obj.getValue.bind(obj);
setTimeout(boundGetValue, 100); // 42

// Event handler con possibilità di rimuovere
var handler = button.handleClick.bind(button);
element.addEventListener("click", handler);
element.removeEventListener("click", handler); // Funziona!
```

### 3. pattern self/that (Legacy)

Prima delle arrow functions, si salvava il riferimento a `this` in una variabile accessibile via closure.

```javascript
var obj = {
  value: 42,
  setup: function () {
    var self = this; // Salva riferimento
    setTimeout(function () {
      console.log(self.value); // 42 (usa closure)
    }, 100);
  }
};
```

---

**Tags**: `#javascript` `#this` `#callbacks` `#binding-loss` `#arrow-functions` `#bind`
