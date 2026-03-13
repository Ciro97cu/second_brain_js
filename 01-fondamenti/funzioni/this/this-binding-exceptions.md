# [[../../../appunti-completi#311-lidentificatore-this|Eccezioni di Binding al Dettaglio]]

Oltre ai problemi comuni di perdita di binding, ci sono situazioni in cui il comportamento di `this` può essere **sorprendente per design**.

## Ignorare null e undefined

Se passi `null` o `undefined` come binding di `this` a funzioni come `call`, `apply` o `bind`, questi valori vengono **ignorati** e viene applicata la **regola di default binding** al loro posto:

```javascript
function foo() {
  console.log(this.a);
}

var a = 2; // global property

foo.call(null); // 2 (default binding!)
foo.apply(undefined); // 2 (default binding!)
```

### Il Pericolo

È comune usare `null` quando non ti interessa il binding di `this` ma hai bisogno di un placeholder per lo strato di parametri extra, come nello spreading array:

```javascript
function sum(a, b) { return a + b; }
sum.apply(null, [2, 3]); // 5
```

Tuttavia, se la funzione **usa effettivamente `this`** nel suo corpo, il default binding può mutare involontariamente il global object, creando bug difficili da scovare:

```javascript
function dangerous() {
  this.leaked = "oops!"; // Muta window/global!
}

dangerous.call(null);
console.log(window.leaked); // "oops!" (in browser)
```

Questo pattern è particolarmente pericoloso quando si utilizzano **funzioni di terze parti** in cui non si ha il controllo interno di eventuali utilizzi del riferimento a `this`. Per risolvere in sicurezza questo problema, si utilizza comunemente il pattern [[this-dmz-object|DMZ Object Pattern]].

---

**Tags**: `#javascript` `#this` `#binding-exceptions` `#call` `#apply`
