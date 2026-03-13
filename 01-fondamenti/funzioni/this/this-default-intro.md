# [[../../../appunti-completi#311-lidentificatore-this|Default Binding (Introduzione)]]

La **default binding** è la prima regola del binding di `this` e rappresenta il caso più comune: l'invocazione standalone di una funzione senza alcun contesto specifico.

## Concetti Chiave

- **Regola catch-all**: Si applica quando nessuna delle altre regole (implicit, explicit, new) risulta applicabile.
- **Plain function call**: Chiamata diretta senza decorazioni (es. `foo()`).
- **Global object**: In non-strict mode, `this` punta al global object.
- **Precedenza**: Tra le quattro regole per determinare il valore di `this`, la default binding possiede la priorità più bassa.

## Quando Si Applica

La default binding entra in gioco in concomitanza con una chiamata diretta di una funzione standalone (plain, undecorated function reference).

```javascript
function foo() {
  console.log(this.a);
}

var a = 2;

foo(); // 2 (this = global object in non-strict mode)
```

## Concetti Fondamentali

### Variabili Globali come Proprietà del Global Object

Definire una variabile tramite `var` nello scope globale, comporta la creazione di una proprietà sul global object. Non si tratta di due copie distinte, bensì della stessa entità.

```javascript
var a = 42;

console.log(window.a); // 42 (browser)
console.log(this.a);   // 42 (global scope)
console.log(a);        // 42
// Sono tutti riferimenti alla stessa proprietà.
```

### Il Concetto di Plain Function Call

L'invocazione di `foo()` tramite un riferimento semplice, senza l'uso di decorazioni contestuali, esclude le altre formule di binding. In particolare:

- Non è presente un `.call()` o un `.apply()` (che attiverebbero l'explicit binding).
- L'invocazione non è del tipo `obj.foo()` (che imporrebbe l'implicit binding).
- La chiamata non reca la keyword `new` anteposta, ad es. `new foo()` (il che causerebbe il new binding).

La mancanza di tutti i suddetti pattern decreta l'applicazione immancabile della default binding.

### Risoluzione di this verso il Global Object

Assodato che le altre regole non intervengano, `this` punterà all'oggetto globale, corrispondente a:

- `window` in ambiente browser.
- `global` in ambiente Node.js.

```javascript
function foo() {
  console.log(this === window); // true (ambiente browser)
}

foo();
```

---
**Tags**: `#javascript` `#this` `#default-binding` `#global-object`
