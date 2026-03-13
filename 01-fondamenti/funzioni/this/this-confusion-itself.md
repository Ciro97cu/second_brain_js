# [[../../appunti-completi#confusione-1-this-come-riferimento-alla-funzione-stessa|Confusione: this come Riferimento alla Funzione Stessa]]

Una delle confusioni più comuni è assumere che `this` si riferisca alla funzione stessa. Dal punto di vista grammaticale può sembrare ragionevole, ma **è completamente sbagliato**.

## 🎯 Concetti Chiave

- `this` NON punta mai alla funzione stessa
- Le funzioni sono oggetti, ma `this` non le referenzia automaticamente
- Per riferirsi a una funzione dall'interno, usa il nome della funzione (lexical identifier)
- Oppure forza `this` con `call()`, `apply()` o `bind()`

## 💻 Il Problema: Tentativo di Tracciare Chiamate

### Codice che Fallisce

```javascript
function foo(num) {
  console.log("foo: " + num);
  this.count++; // ❌ Pensiamo che this = foo
}

foo.count = 0; // Aggiungiamo proprietà count alla funzione

for (var i = 0; i < 10; i++) {
  if (i > 5) {
    foo(i);
  }
}
// foo: 6
// foo: 7
// foo: 8
// foo: 9

console.log(foo.count); // 0 -- Perché ancora 0?!
```

**Cosa è successo**: La funzione è stata chiamata 4 volte, ma `foo.count` è ancora 0.

### Spiegazione

1. `foo.count = 0` crea effettivamente una proprietà `count` sull'oggetto funzione `foo`
2. **MA** quando eseguiamo `foo(i)` (chiamata diretta), `this` dentro la funzione punta al **global object**, non a `foo`
3. Quindi `this.count++` crea accidentalmente una variabile globale `count` con valore `NaN` (perché `undefined++` = `NaN`)
4. La proprietà `foo.count` rimane intoccata a 0

Il problema è il **default binding**: in una chiamata diretta `foo()`, `this` = global object (o `undefined` in strict mode).

## ⚠️ Soluzioni Sbagliate (ma Comuni)

### Soluzione 1: Oggetto Esterno

Molti sviluppatori aggirano il problema creando un oggetto separato:

```javascript
var data = { count: 0 };

function foo(num) {
  console.log("foo: " + num);
  data.count++; // Usa lexical scope
}

for (var i = 0; i < 10; i++) {
  if (i > 5) {
    foo(i);
  }
}

console.log(data.count); // 4 ✅ Funziona
```

**Problema**: Risolve il sintomo ma ignora la vera comprensione di `this`. Si rifugia nel lexical scope invece di imparare come funziona `this`.

### Soluzione 2: Nome della Funzione

Usare l'identificatore lessicale della funzione:

```javascript
function foo(num) {
  console.log("foo: " + num);
  foo.count++; // Usa il nome della funzione direttamente
}

foo.count = 0;

for (var i = 0; i < 10; i++) {
  if (i > 5) {
    foo(i);
  }
}

console.log(foo.count); // 4 ✅ Funziona
```

**Problema**: Anche questo evita la comprensione di `this`. Si basa interamente sul lexical scope.

## ✅ Soluzione Corretta: Forzare this con call()

```javascript
function foo(num) {
  console.log("foo: " + num);
  this.count++; // Ora this = foo grazie a call()
}

foo.count = 0;

for (var i = 0; i < 10; i++) {
  if (i > 5) {
    /*
     * Usando call(), assicuriamo che this punti
     * all'oggetto funzione (foo) stesso
     */
    foo.call(foo, i);
  }
}

console.log(foo.count); // 4 ✅ Funziona!
```

**Perché è corretta**: Invece di evitare `this`, lo abbracciamo. Usando `.call(foo)`, forziamo esplicitamente `this` a puntare all'oggetto funzione `foo`.

## 💡 Perché Questo Confonde

### Ragioni della Confusione

1. **Grammaticalmente sembra sensato**: "this" in inglese suggerisce "se stesso"
2. **Le funzioni SONO oggetti**: In JavaScript le funzioni sono oggetti con proprietà
3. **Sembra conveniente**: Poter memorizzare stato nella funzione stessa appare utile
4. **Uso di recursione**: Per la ricorsione si riferisce alla funzione stessa, quindi perché non con `this`?

### La Verità

- Per **recursione**, usa il nome della funzione: `function foo() { foo(); }`
- Per **proprietà della funzione**, usa il nome: `foo.count++`
- `this` serve per **binding dinamico a oggetti esterni**, non alla funzione stessa

### Anonymous Functions

Con funzioni anonime il problema è ancora più visibile:

```javascript
setTimeout(function () {
  // Come mi riferisco a questa funzione?
  // Non ho un nome!
  // this NON mi aiuta
}, 10);
```

**Soluzione**: Usa named functions quando hai bisogno di self-reference.

## 📊 Confronto Approcci

| Approccio                          | Funziona? | Usa this?      | Comprensione   |
| ---------------------------------- | --------- | -------------- | -------------- |
| `this.count++` in chiamata diretta | ❌ No     | Sì (sbagliato) | Confuso        |
| Oggetto esterno `data.count++`     | ✅ Sì     | No             | Evita problema |
| Nome funzione `foo.count++`        | ✅ Sì     | No             | Evita problema |
| `foo.call(foo, i)`                 | ✅ Sì     | Sì (corretto)  | Comprende this |

## 🔗 Collegamenti

**Prerequisiti**:

- [[this-concept]] - Comprendere cos'è this
- [[this-binding-default]] - Default binding
- [[funzioni]] - Funzioni come oggetti

**Concetti Correlati**:

- [[this-call-apply-bind]] - Come forzare this con call()
- [[this-confusion-scope]] - L'altra confusione comune (this e scope)

**Approfondimenti**:

- [[../scope/lexical-scope-base]] - Differenza tra this e lexical scope
- [[../avanzate/recursion]] - Ricorsione senza this

## 📚 Riferimenti

- **You Don't Know JS**: this & Object Prototypes - Chapter 1 "Confusions"
- **MDN**: [Function.prototype.call()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)
- **MDN**: [this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)

## 📌 Note Personali

[Annotazioni sulla confusione "this = funzione stessa"]

---

**Tags**: `#javascript` `#this` `#confusioni` `#binding` `#call` `#default-binding`
