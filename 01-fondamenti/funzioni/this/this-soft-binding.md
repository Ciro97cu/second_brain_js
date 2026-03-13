# [[../../../appunti-completi#311-lidentificatore-this|Soft Binding di this]]

L'**hard binding** (tramite `bind()`) previene efficacemente una funzione dal ricadere nel default binding, forzandola a usare un `this` specifico preassegnato. Tuttavia, questo approccio ha un grosso limite: **riduce drasticamente la flessibilità**, non rendendo quasi più possibile sovrascrivere `this` manualmente tramite futuri implicit o explicit binds con chiamate extra.

Sarebbe utile avere un **default preassegnato più sicuro** rispetto allo standard `global` o `undefined`, ma **lasciando comunque la possibilità** di sovrascriverlo al momento opportuno con un context volontario.

## Implementazione Custom

Si può polifillare un'utility `softBind()` personalizzata che emula questo comportamento e cattura this a runtime:

```javascript
if (!Function.prototype.softBind) {
  Function.prototype.softBind = function (obj) {
    var fn = this;
    var curried = [].slice.call(arguments, 1);
    
    var bound = function () {
      // Controlla this al call-time
      // Se è globale/undefined (è un default binding scappato dal controllo) ecc... usa 'obj' protetto preimpostato
      // Se invece 'this' è stato volontariamente configurato dal chimate manuale in seguito... rispettalo.
      var isDefault = (!this || this === (window || global));
      
      return fn.apply(
        isDefault ? obj : this,
        curried.concat.apply(curried, arguments)
      );
    };
    
    bound.prototype = Object.create(fn.prototype);
    return bound;
  };
}
```

## Vantaggi

Il soft binding offre sicurezza ma massima flessibilità futura:

```javascript
function foo() { console.log(this.name); }

var obj = { name: "obj" };
var obj2 = { name: "obj2" };
var obj3 = { name: "obj3" };

var fooOBJ = foo.softBind(obj);

// Scatenerebbe default binding → usa obj come fallback di cuscinetto salva-vita
fooOBJ(); // name: obj

// Implicit binding → override manuale permesso! Questo differisce dal blind originario 
obj2.foo = fooOBJ;
obj2.foo(); // name: obj2 

// Explicit binding
fooOBJ.call(obj3); // name: obj3

// Anche nelle classiche perdite di callback
setTimeout(obj2.foo, 10); // name: obj (Ricompare il fallback di salvataggio)
```

**Quando usarlo**: utile per non lockare API terze mantenendo il "this" di modulo come ruota di riserva senza limitare lo sviluppatore consumer nell'adozione finale della funzione.

---

**Tags**: `#javascript` `#this` `#soft-binding` `#custom-polifills`
