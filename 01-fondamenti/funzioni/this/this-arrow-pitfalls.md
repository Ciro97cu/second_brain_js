# [[../../../appunti-completi#311-lidentificatore-this|Arrow Functions: Gotchas e Limitazioni]]

Poiché le arrow functions adottano un binding lessicale per `this`, presentano caratteristiche specifiche che le rendono inadatte in svariati contesti rispetto alle funzioni tradizionali.

## Non Modificabile con Call, Apply e Bind

Il valore di `this` in una arrow function è fissato al momento della definizione e risulta inalterabile sia con l'uso di `call`, `apply`, che di `bind`.

```javascript
var obj1 = { value: 1 };
var obj2 = { value: 2 };

var arrow = () => console.log(this.value);
var regular = function () { console.log(this.value); };

regular.call(obj1); // 1
regular.call(obj2); // 2

// Le arrow function ignorano il contesto passato esplicitamente dall'oggetto
arrow.call(obj1); // undefined (preleva il reference al 'this' globale)
arrow.call(obj2); // undefined
```

## Strumenti Inadeguati come Metodi di Oggetti

Utilizzare un'arrow function come metodo in un oggetto letterale impedisce alla funzione di accedere alle proprietà dell'oggetto stesso. Questo accade perché il valore non referenzia l'oggetto ospitante ma viene automaticamente agganciato al contesto globale o della funzione più esterna in esecuzione.

```javascript
// Implementazione errata
var objErrato = {
  value: 42,
  getValue: () => {
    return this.value; // 'this' non si riferisce a 'objErrato'
  },
};

// Implementazione corretta
var objCorretto = {
  value: 42,
  getValue() { // equivalente del classico function()
    return this.value; 
  },
};
```

## Impossibilità di Utilizzo Costruttori (new)

Le arrow functions non espongono la proprietà `prototype` e sono sprovviste del metodo interno `[[Construct]]`. Risulta perciò impossibile generare oggetti derivati usando l'operatore di istanza `new`, ottenendo invece un errore.

```javascript
var Foo = () => {
  this.value = 1;
};

var obj = new Foo(); // Restituisce Type Error
```

## L'Assenza dell'Oggetto Arguments

Le arrow function non espongono o memorizzano l'oggetto implicito e globale `arguments` interno alle invocazioni. Per accedere ad argomenti indefiniti, è doveroso ed essenziale basarsi sull'impiego dei Rest Parameters dello standard ES6.

```javascript
var arrowData = (...args) => {
  console.log(args); // Rende un Array [1, 2, 3]
};

arrowData(1, 2, 3);
```