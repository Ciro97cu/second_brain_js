# [[../../../appunti-completi#311-lidentificatore-this|Arrow Functions: Comportamento Lessicale]]

Le arrow functions (ES6+) presentano un comportamento completamente diverso rispetto alle funzioni tradizionali riguardo a `this`. Non seguono le quattro regole standard di binding dinamico, ma **ereditano `this` dal contesto lessicale esterno**.

## Concetti Chiave

- **Lexical this**: Le arrow function non possiedono un proprio `this`, ma utilizzano quello del contesto esterno in cui sono state definite.
- **Soluzione ai callback**: Risolvono strutturalmente il problema della perdita di contesto nei callback.
- **Pattern equivalente**: Il costrutto `var self = this`, utilizzato nello standard pre-ES6, svolgeva la medesima funzione tramite cattura lessicale.

## Binding Lessicale vs Funzione Tradizionale

Nelle funzioni tradizionali, il valore di `this` è determinato dinamicamente al momento dell'invocazione. Nelle arrow function, è determinato in modo statico al momento della definizione.

```javascript
function TimerTradizionale() {
  this.seconds = 0;

  // Funzione tradizionale: perde il riferimento all'istanza
  setInterval(function () {
    this.seconds++; // 'this' punta all'oggetto globale (Window)
    console.log(this.seconds); // NaN
  }, 1000);
}

function TimerArrow() {
  this.seconds = 0;

  // Arrow function: cattura 'this' dal contesto della funzione esterna
  setInterval(() => {
    this.seconds++; // 'this' punta all'istanza di TimerArrow
    console.log(this.seconds); // 1, 2, 3...
  }, 1000);
}
```

## Cattura del Contesto Esterno

Il comportamento si evidenzia particolarmente all'interno dei metodi di un oggetto gestiti in modalità asincrona:

```javascript
var obj = {
  id: 42,

  metodoTradizionale: function () {
    console.log(this.id); // 42

    setTimeout(function () {
      console.log(this.id); // undefined ('this' è globale)
    }, 100);
  },

  metodoArrow: function () {
    console.log(this.id); // 42

    setTimeout(() => {
      console.log(this.id); // 42 ('this' è catturato lessicalmente da 'metodoArrow')
    }, 100);
  },
};
```
