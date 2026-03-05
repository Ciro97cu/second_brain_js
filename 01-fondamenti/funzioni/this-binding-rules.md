# [[../../appunti-completi#311-lidentificatore-this|Le Quattro Regole del Binding di this]]

Esistono quattro regole che determinano quale sia il binding di `this` durante una chiamata di funzione. L'ordine di applicazione è importante: alcune regole hanno precedenza sulle altre.

## 🎯 Concetti Chiave

- **Quattro regole**: Default, Implicit, Explicit, New binding
- **Precedenza**: New > Explicit > Implicit > Default
- **Call-site**: Il punto nel codice dove la funzione viene chiamata determina quale regola si applica
- **Vincitore unico**: Solo UNA regola si applica per ogni chiamata

## 💻 Le Quattro Regole

### 1️⃣ Default Binding

**Quando**: Chiamata diretta di funzione standalone (nessun contesto)

```javascript
function foo() {
  console.log(this.a);
}

var a = 2;
foo(); // 2 (in non-strict mode, this = global object)
```

**Strict mode**: `this` è `undefined` invece che global object.

```javascript
function foo() {
  "use strict";
  console.log(this.a); // TypeError: this is undefined
}

var a = 2;
foo();
```

---

### 2️⃣ Implicit Binding

**Quando**: La funzione viene chiamata come metodo di un oggetto

```javascript
function foo() {
  console.log(this.a);
}

var obj = {
  a: 2,
  foo: foo,
};

obj.foo(); // 2 (this = obj)
```

**Con catene di oggetti**: Conta solo l'ultimo livello

```javascript
function foo() {
  console.log(this.a);
}

var obj2 = {
  a: 42,
  foo: foo,
};

var obj1 = {
  a: 2,
  obj2: obj2,
};

obj1.obj2.foo(); // 42 (this = obj2, non obj1)
```

---

### 3️⃣ Explicit Binding

**Quando**: Usi `call()`, `apply()` o `bind()` per specificare esplicitamente `this`

```javascript
function foo() {
  console.log(this.a);
}

var obj = {
  a: 2,
};

foo.call(obj); // 2 (this forzato a essere obj)
```

**Hard binding** con `bind()`:

```javascript
function foo() {
  console.log(this.a);
}

var obj = {
  a: 2,
};

var bar = foo.bind(obj); // Hard binding
bar(); // 2
setTimeout(bar, 100); // 2
bar.call(window); // 2 (bind vince su call!)
```

---

### 4️⃣ New Binding

**Quando**: La funzione viene invocata come costruttore con `new`

```javascript
function foo(a) {
  this.a = a;
}

var bar = new foo(2);
console.log(bar.a); // 2 (this = nuovo oggetto creato)
```

**Cosa fa `new`**:

1. Crea un nuovo oggetto vuoto
2. Linka il nuovo oggetto al prototype della funzione
3. Il nuovo oggetto diventa `this` per la chiamata
4. Se la funzione non ritorna un oggetto, `new` ritorna il nuovo oggetto

## 📊 Ordine di Precedenza

Le regole si applicano in questo ordine (dalla più forte):

```
1. new binding          (massima priorità)
2. Explicit binding     (call, apply, bind)
3. Implicit binding     (obj.method())
4. Default binding      (minima priorità)
```

### Esempio di Precedenza

```javascript
function foo(something) {
  this.a = something;
}

var obj1 = {};

var bar = foo.bind(obj1);
bar(2);
console.log(obj1.a); // 2

var baz = new bar(3);
console.log(obj1.a); // 2 (obj1 non modificato)
console.log(baz.a); // 3 (new vince su bind!)
```

## ⚠️ Gotcha

### Perdita dell'Implicit Binding

```javascript
function foo() {
  console.log(this.a);
}

var obj = {
  a: 2,
  foo: foo,
};

var bar = obj.foo; // Riferimento alla funzione!
var a = "oops, global";

bar(); // "oops, global" (usa default binding!)
```

La funzione perde il contesto quando viene assegnata come riferimento.

### Callback e this

```javascript
function foo() {
  console.log(this.a);
}

function doFoo(fn) {
  fn(); // call-site!
}

var obj = {
  a: 2,
  foo: foo,
};

var a = "oops, global";
doFoo(obj.foo); // "oops, global"
```

Le callback perdono spesso il binding implicito.

## ✅ Best Practices

1. **Default Binding**: Usa strict mode per evitare binding accidentali al global object
2. **Implicit Binding**: Attenzione quando passi metodi come callback (si perde il contesto)
3. **Explicit Binding**: Usa `bind()` per "congelare" il contesto in callback e handler
4. **New Binding**: Usa sempre `new` con funzioni constructor (convenzione: CamelCase)

## 🔗 Collegamenti

**Prerequisiti**:

- [[this-concept]] - Comprendere cos'è this
- [[funzioni]] - Funzioni JavaScript base

**Concetti Correlati**:

- [[this-call-apply-bind]] - Dettagli su explicit binding
- [[this-binding-problems]] - Problemi comuni con this
- [[this-arrow-functions]] - Arrow functions e this

**Approfondimenti**:

- [[../oggetti/costruttori]] - Pattern constructor con new
- [[../prototipi/prototipi]] - This e prototipi

## 📚 Riferimenti

- **You Don't Know JS**: this & Object Prototypes - Chapter 2
- **MDN**: [this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
- **MDN**: [new operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new)

## 📌 Note Personali

[Annotazioni personali sulle regole di binding]

---

**Tags**: `#javascript` `#this` `#binding` `#call-site` `#precedence`
