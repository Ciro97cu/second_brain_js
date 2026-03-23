# [[../../appunti-completi#81-prototype-e-la-catena|La Catena dei Prototipi (`[[Prototype]]`)]]

In JavaScript, quasi tutti gli oggetti possiedono una proprietà nascosta chiamata `[[Prototype]]`, che è un semplice collegamento verso un altro oggetto.

Quando l'Engine esegue un'operazione di lettura (`[[Get]]`) e non trova la proprietà direttamente nell'oggetto, segue questo collegamento per cercarla nell'oggetto "genitore".

```javascript
const anotherObject = { a: 2 };

// myObject viene collegato ad anotherObject
const myObject = Object.create(anotherObject);

console.log(myObject.a); // 2
```

Se non la trova, continua a risalire la gerarchia di oggetto in oggetto. Questo percorso è definito **catena dei prototipi**. La consultazione a ritroso avviene anche quando si analizza un oggetto con un ciclo `for..in` o con l'operatore `in`.

## Object.prototype

La catena termina sempre in `Object.prototype`. Questo è l'oggetto globale alla radice del linguaggio, che contiene le utility standard ereditate da tutti gli altri oggetti, come `.hasOwnProperty()`, `.toString()`, o `.valueOf()`.

## 🔗 Collegamenti

**Approfondimenti**:

- [[shadowing]]
