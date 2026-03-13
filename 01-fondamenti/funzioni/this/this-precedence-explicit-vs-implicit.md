# [[../../../appunti-completi#explicit-vs-implicit-binding|Explicit vs Implicit Binding]]

Nell'algoritmo di risoluzione del binding di `this`, l'_explicit binding_ (effettuato tramite `call`, `apply` o `bind`) gode di una precedenza maggiore rispetto all'_implicit binding_ (la chiamata di una funzione come metodo di un oggetto).

## Esempio di Precedenza

Quando una funzione viene invocata contemporaneamente sia come proprietà di un oggetto che attraverso un binding esplicito, la regola esplicita sovrascrive ed invalida quella implicita:

```javascript
function foo() {
  console.log(this.valore);
}

var obj1 = { valore: "obj1", foo: foo };
var obj2 = { valore: "obj2" };

obj1.foo(); // "obj1" (implicit binding)
obj1.foo.call(obj2); // "obj2" (explicit binding vince)
```

In questo scenario, sebbene `foo` sia chiamato come metodo di `obj1` (`obj1.foo`), l'utilizzo di `.call(obj2)` applica immediatamente un _explicit binding_ al call-site e di conseguenza `this` non punterà ad `obj1`, ma ad `obj2`.

Questa precedenza assicura che il contesto d'esecuzione di una funzione possa essere sempre forzato in modo deterministico, a prescindere dall'oggetto in cui il metodo è stato eventualmente definito o vi è referenziato.

Anche nei casi in cui implicit binding è prevalente sul _default binding_:

```javascript
function bar() {
  console.log(this.a);
}

var a = "global";
var obj3 = { a: "oggetto", bar: bar };

obj3.bar(); // "oggetto" (implicit vince)
bar(); // "global" (default - nessuna regola più forte o metodo associato)
```

Si capisce come le precedenze strutturino le associazioni e il lookup in maniera consistente e predefinita.
