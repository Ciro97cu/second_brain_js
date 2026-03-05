# [[../../appunti-completi#311-lidentificatore-this|L'identificatore this]]

La keyword `this` è uno dei meccanismi più fraintesi in JavaScript. Si tratta di un identificatore speciale definito automaticamente nello scope di ogni funzione, ma ciò a cui si riferisce rappresenta fonte di confusione anche per sviluppatori esperti.

## 🎯 Concetti Chiave

- **Call-site determina this**: L'oggetto a cui `this` punta dipende **esclusivamente da come la funzione viene chiamata** (call-site), non da dove è stata definita
- **Binding dinamico**: Il valore di `this` è determinato al momento dell'invocazione, non al momento della scrittura
- **Equivoco comune**: `this` **NON** si riferisce alla funzione stessa
- **Quattro regole**: Default, Implicit, Explicit, New binding (in ordine di precedenza crescente)

## 💡 Perché this?

Il meccanismo `this` fornisce un modo elegante per **passare implicitamente** un riferimento a un oggetto, permettendo il riutilizzo delle funzioni su multipli contesti:
/\*

- Con this: contesto implicito (più elegante)
  \*/
  function identify() {
  return this.name.toUpperCase();
  }

function speak() {
var greeting = "Hello, I'm " + identify.call(this);
console.log(greeting);
}

var me = { name: "Kyle" };
var you = { name: "Reader" };

identify.call(me); // KYLE
identify.call(you); // READER
speak.call(me); // Hello, I'm KYLE
speak.call(you); // Hello, I'm READER

/\*

- Senza this: passaggio esplicito (più verboso)
  \*/
  function identifyContext(context) {
  return context.name.toUpperCase();
  }

function speakContext(context) {
var greeting = "Hello, I'm " + identifyContext(context);
console.log(greeting);
}

identifyContext(you); // READER
speakContext(me); // Hello, I'm KYLE

````

Più complesso diventa il pattern di utilizzo, più chiaramente si vede che passare il contesto come parametro esplicito risulta più disordinato rispetto all'uso di `this`.

## Confusioni Comuni

**Principio fondamentale**: quando una funzione contiene un riferimento a `this`, quel riferimento punta a un oggetto. Tuttavia, **l'oggetto dipende esclusivamente da come la funzione viene chiamata** (call-site), non da dove è stata definita.

**Equivoco più comune**: pensare che `this` si riferisca alla funzione stessa. Non è così. Il valore di `this` è un binding dinamico determinato al momento dell'invocazione secondo regole specifiche.

## Le Quattro Regole del Binding

Per capire a cosa si riferisce `this`, si esamina il punto esatto in cui la funzione viene chiamata. Il contesto determina il valore di `this` secondo una di queste quattro regole:

```javascript
function foo() {
  console.log(this.bar);
}

var bar = "global";
var obj1 = { bar: "obj1", foo: foo };
var obj2 = { bar: "obj2" };

// Le quattro regole in azione:
foo(); // "global" - default binding
obj1.foo(); // "obj1" - implicit binding
foo.call(obj2); // "obj2" - explicit binding
new foo(); // undefined - new binding
````

### 1. Default Binding

Chiamata **diretta** senza contesto specifico → `this` = oggetto **globale** (`window` nel browser).

```javascript
function mostraNome() {
  console.log(this.nome);
}

var nome = "Globale";
mostraNome(); // "Globale" (this = window/global)
```

⚠️ **Strict Mode**: `this` rimane `undefined` invece del globale, causando un TypeError se si tenta di accedere alle sue proprietà.

### 2. Implicit Binding

Chiamata come **metodo di un oggetto** → `this` = l'**oggetto** stesso.

```javascript
var persona = {
  nome: "Mario",
  saluta: function () {
    console.log("Ciao, sono " + this.nome);
  },
};

persona.saluta(); // "Ciao, sono Mario" (this = persona)
```

**⚠️ Perdita del Binding**: Estraendo il metodo si perde il riferimento all'oggetto:

```javascript
var saluto = persona.saluta;
saluto(); // "Ciao, sono Globale" (this = window, default binding!)
```

Questo è un problema frequente con i **callback**. Con oggetti annidati, `this` si riferisce all'oggetto più vicino nella catena di chiamata.

### 3. Explicit Binding

Impostare **esplicitamente** `this` con `.call()`, `.apply()`, o `.bind()`.

```javascript
function descrivi() {
  console.log(this.tipo + ": " + this.nome);
}

var animale1 = { tipo: "Cane", nome: "Fido" };
var animale2 = { tipo: "Gatto", nome: "Micio" };

descrivi.call(animale1); // "Cane: Fido"
descrivi.call(animale2); // "Gatto: Micio"
```

**call vs apply**: `call` accetta argomenti separati, `apply` accetta un array:

```javascript
function somma(a, b) {
  console.log(this.nome + " calcola: " + (a + b));
}

var utente = { nome: "Mario" };

somma.call(utente, 5, 3); // "Mario calcola: 8" (argomenti separati)
somma.apply(utente, [5, 3]); // "Mario calcola: 8" (argomenti in array)
```

**bind**: crea una nuova funzione con `this` permanentemente fissato (hard binding):

```javascript
var salutaMario = persona.saluta.bind(persona);
salutaMario(); // "Ciao, sono Mario" (this è sempre persona)

setTimeout(persona.saluta, 1000); // "Ciao, sono Globale" (perde this)
setTimeout(persona.saluta.bind(persona), 1000); // "Ciao, sono Mario" (this fissato)
```

### 4. New Binding

Con `new` → `this` = **nuovo oggetto vuoto** creato automaticamente.

```javascript
function Persona(nome, eta) {
  this.nome = nome;
  this.eta = eta;
  this.descrivi = function () {
    console.log(this.nome + " ha " + this.eta + " anni");
  };
}

var p1 = new Persona("Mario", 30);
var p2 = new Persona("Luigi", 25);

p1.descrivi(); // "Mario ha 30 anni"
p2.descrivi(); // "Luigi ha 25 anni"
console.log(p1.nome); // "Mario" (this era il nuovo oggetto)
```

Quando si usa `new`:

1. Viene creato un nuovo oggetto vuoto
2. `this` viene associato al nuovo oggetto
3. La funzione costruttore popola `this`
4. Il nuovo oggetto viene ritornato automaticamente (a meno che la funzione non ritorni esplicitamente un altro oggetto)

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

- [[this-binding-problems]] - Problemi comuni con this (callback, arrow functions, soluzioni)
- [[funzioni]] - Le funzioni e il loro contesto di esecuzione
- [[closure]] - This e closure insieme per dati privati
- [[../oggetti/oggetti]] - This nei metodi degli oggetti
- [[../sintassi/strict-mode]] - Comportamento di this in strict mode
