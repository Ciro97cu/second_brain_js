# [[../../../appunti-completi#311-lidentificatore-this|DMZ Object Pattern per this]]

Quando si usano `call`, `apply` o `bind` passando `null` o `undefined` come valore per `this`, per design questi vengono ignorati e si applica il **default binding**. Questo per ignoranza o superficialità può inquinare l'oggetto globale.

Per ovviare, specialmente con codici 3rd-party ignoti, si usa un **DMZ (Demilitarized Zone) Object**.

## Creare un DMZ Object

Un DMZ serve come contenitore morto ed è un oggetto completamente vuoto, senza prototipo, creato con `Object.create(null)`.

```javascript
// Crea oggetto DMZ (più vuoto e minimale di {})
// ø rappresenta in matematica un insieme vuoto (Option-o su Mac)
var ø = Object.create(null);

function foo(a, b) {
  console.log("a:" + a + ", b:" + b);
}

// Usa ø invece di null come placeholder
foo.apply(ø, [2, 3]); // a:2, b:3 ✅

var bar = foo.bind(ø, 2); // Binding con placeholder per un currying futuro
bar(3); // a:2, b:3 ✅
```

## Perché non usare semplicemente un oggetto predefinito `{}`?

- `{}` porta con sé tutta la catena delle istanze delegate a `Object.prototype` nascoste ai consumatori di properties (creando side object values di `toString` ecc).
- `Object.create(null)` è **totalmente vuoto** (nessuna prototype chain nativa).
- Qualsiasi uso accidentale di `this` resta isolato senza effetti collaterali verso l'oggetto globale.

## Alternative Future (ES6+)

Con l'arrivo dello **spread operator**, il bisogno di `apply` per passare array come parametri separati viene meno:

```javascript
function foo(a, b, c) {
  return a + b + c;
}
var args = [1, 2, 3];

// ES6: Spread evita di dichiarare un this predefinito
foo(...args); // No this placeholder necessario!
```

**⚠️ Nota**: Non esiste equivalente ES6 generico per lo scoping del _currying_ con un equivalente sintetico nativo che faccia il binding parziale, quindi per questo scenario serve ancora il placeholder DMZ per i bind incompleti.

---

**Tags**: `#javascript` `#this` `#dmz-object` `#null-safety` `#placeholders`
