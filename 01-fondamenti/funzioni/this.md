# [[../../appunti-completi#311-lidentificatore-this|L'identificatore this]]

La parola chiave `this` in JavaScript è spesso fraintesa. Se una funzione contiene un riferimento a `this`, quel riferimento punta a un **oggetto**, ma l'**oggetto dipende da come la funzione è stata chiamata** (call-site).

**Equivoco comune**: `this` **NON** si riferisce alla funzione stessa.

```javascript
function foo() {
  console.log(this.bar);
}

var bar = "global";
var obj1 = { bar: "obj1", foo: foo };
var obj2 = { bar: "obj2" };

foo(); // "global" - default binding
obj1.foo(); // "obj1" - implicit binding
foo.call(obj2); // "obj2" - explicit binding
new foo(); // undefined - new binding
```

## Le Quattro Regole del Binding

### 1. Default Binding

Chiamata **diretta** → `this` = oggetto **globale** (`window` nel browser).

```javascript
function identify() {
  console.log(this.name);
}

var name = "Global Context";
identify(); // "Global Context"
```

⚠️ **Strict Mode** → `this` rimane `undefined` invece del globale.

### 2. Implicit Binding

Chiamata come **metodo di un oggetto** → `this` = l'**oggetto** stesso.

```javascript
var person = {
  name: "Alice",
  greet: function () {
    console.log("Ciao, sono " + this.name);
  },
};

person.greet(); // "Ciao, sono Alice"
```

⚠️ **Perdita del Binding** → Estraendo il metodo si perde il binding:

```javascript
var greetFunc = person.greet;
greetFunc(); // this = globale (default binding)
```

Questo accade spesso con i **callback**.

### 3. Explicit Binding

Impostare **esplicitamente** `this` con `.call()`, `.apply()`, o `.bind()`.

```javascript
function greet() {
  console.log("Ciao, sono " + this.name);
}

var person1 = { name: "Alice" };
var person2 = { name: "Bob" };

greet.call(person1); // "Ciao, sono Alice"
greet.apply(person2); // "Ciao, sono Bob"

// .bind() crea hard binding permanente
var boundGreet = greet.bind(person1);
boundGreet(); // "Ciao, sono Alice"
```

### 4. New Binding

Con `new` → `this` = **nuovo oggetto vuoto** creato.

```javascript
function Person(name) {
  this.name = name;
}

var alice = new Person("Alice");
console.log(alice.name); // "Alice"
```

Quando si usa `new`:

1. Viene creato un nuovo oggetto vuoto
2. `this` = nuovo oggetto
3. La funzione popola `this`
4. Il nuovo oggetto viene ritornato automaticamente

## Ordine di Precedenza

1. **New binding** (massima)
2. **Explicit binding**
3. **Implicit binding**
4. **Default binding** (minima)

## Riepilogo

Per capire `this`, esamina il **call-site** (dove la funzione è chiamata):

- `foo()` → Default: globale (o `undefined` in strict mode)
- `obj.foo()` → Implicit: `obj`
- `foo.call(obj)` → Explicit: `obj` specificato
- `new foo()` → New: nuovo oggetto creato

## Collegamenti

- [[funzioni]] - Le funzioni e il loro contesto di esecuzione
- [[closure]] - This e closure insieme per dati privati
- [[../oggetti/oggetti]] - This nei metodi degli oggetti
- [[../sintassi/strict-mode]] - Comportamento di this in strict mode
