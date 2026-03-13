# [[../../../appunti-completi#call-site-dove-viene-chiamata-la-funzione|Call-Site e Call-Stack]]

Il **Call-Site** è la posizione nel codice in cui una funzione viene invocata, e determina il binding di `this`.

## 🎯 Concetti Chiave

- **Call-Site**: Il punto esatto in cui la funzione viene **chiamata** (non dove viene dichiarata).
- **Call-Stack**: Lo pila di chiamate delle funzioni che porta all'esecuzione corrente.
- **Identificare il Call-Site**: Per trovarlo, bisogna guardare il call-stack e trovare l'invocazione "immediatamente precedente" alla funzione in esecuzione.

## 💻 Esempio di Call-Stack

```javascript
function baz() {
  // call-stack: `baz`
  // call-site: globale (in fondo allo script)
  console.log("baz");
  bar(); // <-- call-site per `bar`
}

function bar() {
  // call-stack: `baz` -> `bar`
  // call-site: dentro `baz`
  console.log("bar");
  foo(); // <-- call-site per `foo`
}

function foo() {
  // call-stack: `baz` -> `bar` -> `foo`
  // call-site: dentro `bar`
  console.log("foo");
}

baz(); // <-- call-site per `baz`
```

## 🛠️ Come ispezionare il Call-Site

1. Usare il **debugger** dei Developer Tools del browser.
2. Inserire `debugger;` all'interno della funzione.
3. Il debugger mostrerà l'intero "Call Stack".
4. Il **secondo elemento dall'alto** nello stack è il reale call-site.

## 🔗 Collegamenti

**Prerequisiti**:

- [[this-concept]] - Concetto base di this

**Approfondimenti**:

- [[this-binding-default]] - Regole di binding in base al call-site

---

**Tags**: `#javascript` `#this` `#call-site` `#call-stack` `#debugger`
