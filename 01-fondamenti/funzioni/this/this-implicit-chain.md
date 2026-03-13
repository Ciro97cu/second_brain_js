# [[../../../appunti-completi#311-lidentificatore-this|Implicit Binding: Catena di Oggetti]]

Nell'ambito dell'implicit binding in JavaScript, quando si invocano metodi attraverso una catena di proprietà di oggetti, si applica una regola fondamentale: **conta solo l'ultimo livello** della catena. L'oggetto che precede immediatamente la chiamata al metodo diventa il contesto `this`.

## Il Principio dell'Ultimo Livello

Quando un metodo viene richiamato tramite molteplici riferimenti concatenati (es. `obj1.obj2.foo()`), il motore JavaScript considera esclusivamente l'oggetto più "vicino" alla funzione al momento dell'invocazione. Gli oggetti precedenti nella catena vengono ignorati per quanto riguarda il binding del contesto.

```javascript
function foo() {
  console.log(this.a);
}

const obj2 = {
  a: 42,
  foo: foo,
};

const obj1 = {
  a: 2,
  obj2: obj2,
};

obj1.obj2.foo(); // 42 (this refers to obj2, NOT obj1)
```

In questo scenario, il call-site effettivo è `obj2.foo()`. Di conseguenza, `obj2` viene utilizzato come contesto `this`, portando alla stampa del valore `42`.

## Catene Più Complesse

Il comportamento rimane invariato indipendentemente dalla profondità della catena. L'unico elemento rilevante per determinare `this` è l'oggetto che possiede la proprietà funzione al momento dell'esecuzione.

```javascript
function greet() {
  console.log(`Hello, ${this.name}!`);
}

const top = {
  name: "Top",
  middle: {
    name: "Middle",
    bottom: {
      name: "Bottom",
      greet: greet,
    },
  },
};

top.middle.bottom.greet(); // "Hello, Bottom!"
```

Anche in questo caso, il metodo viene invocato sull'oggetto `bottom`, che diventa il contesto per `greet`. Gli oggetti `top` e `middle` fungono solo da percorso per raggiungere il riferimento alla funzione.

Questo comportamento sottolinea come in JavaScript l'assegnazione del contesto dipenda strettamente da come la funzione viene chiamata nel suo call-site finale, piuttosto che da come gli oggetti sono strutturati in memoria.

---

**Tags**: `#javascript` `#this` `#implicit-binding` `#object-chain`
