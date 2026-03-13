# [[../../../appunti-completi#311-lidentificatore-this|Default Binding (Strict Mode)]]

Il comportamento della default binding muta in modo radicale laddove intervenga la direttiva "use strict".

## Strict Mode e Default Binding

**In strict mode**, il global object **non è eleggibile** per la default binding. Ne consegue che `this` assumerà invariabilmente il valore `undefined`.

```javascript
function foo() {
  "use strict";
  console.log(this); // undefined
  console.log(this.a); // TypeError: Cannot read property 'a' of undefined
}

var a = 2;

foo(); // TypeError
```

### Dettaglio Importante: Dove Conta lo Strict Mode

Esiste una regola sottile ma di massima importanza per la corretta determinazione del comportamento di `this`: il global object è eleggibile per la default binding **se e solo se il contenuto della funzione invocata non si trova in strict mode**.

La presenza o meno dello strict mode nel call-site (il punto in cui la funzione viene invocata) risulta del tutto irrilevante.

```javascript
function foo() {
  // Il contenuto di questa funzione NON è in strict mode.
  console.log(this.a);
}

var a = 2;

(function () {
  "use strict";

  foo(); // Il call-site è strict, ma il corpo di foo non lo è. Il risultato sarà 2.
})();
```

Anche nell'ipotesi in cui il call-site esponga la direttiva "use strict", il valore risolto per `this` consisterà ancora nel global object, dato che la definizione della funzione invocata, ovvero `foo()`, è estranea alla modalitità restrittiva.

Al contrario, la casistica inversa produrrà un esito diametralmente opposto:

```javascript
function foo() {
  "use strict";
  console.log(this); // undefined
}

var a = 2;

// Call-site sprovvisto di strict mode
foo(); // Questo produce comunque undefined, dacché conta unicamente il corpo di foo.
```

## Mixing Strict/Non-Strict

Rappresenta un antiparttern mescolare porzioni di codice strict e non-strict nel contesto di un medesimo programma JavaScript. È fortemente raccomandabile l'adozione di un approccio omogeneo:

- Utilizzo di strict mode sull'intera base di codice.
- Utilizzo di non-strict mode sull'intera base di codice.

Va operata un'eccezione a titolo prudenziale quando l'esecuzione coinvolge librerie fornite da parti terze: codeste ultime potrebbero adottare di default un differente livello di restrittività. È opportuno riporre massima cautela circa i dettagli intrinseci alla compatibilità inter-modulare e alla potenziale contaminazione dello scope.

---

**Tags**: `#javascript` `#this` `#default-binding` `#strict-mode`
