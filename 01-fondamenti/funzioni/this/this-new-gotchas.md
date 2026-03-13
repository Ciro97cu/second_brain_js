# [[../../../appunti-completi#311-lidentificatore-this|New Binding: Gotchas e Problemi Comuni]]

L'esplicito utilizzo di `new` introduce varie limitazioni e possibili trappole durante l'esecuzione e il parsing del codice, generando risultati inattesi se non se ne comprendono le dinamiche.

## Dimenticare la Parola Chiave `new`

Se un costruttore viene chiamato accidentalmente senza `new`, la funzione subisce i meccanismi del **default binding**. `this` finisce per fare riferimento all'oggetto globale (come `window` nei browser in modalità non-strict), inquinando lo scope.

```javascript
function Person(name) {
  this.name = name;
}

var p = Person("Mario"); // Dimenticato il new

console.log(p); // undefined (il costruttore non ritorna nulla di default)
console.log(window.name); // "Mario" (inquinamento indesiderato del global scope)
```

Le soluzioni comuni comportano:

1. L'utilizzo del costrutto ES6 `class`, che impone categoricamente l'uso di `new`.
2. Verificare cautelativamente all'interno del costruttore che `this instanceof Constructor` sia vero.
3. Affidarsi agli strumenti di analisi statica (linter) per segnalare queste casistiche.

## Compatibilità con Arrow Functions

Le **Arrow Functions** non possiedono una propria struttura interna compatibile con i costruttori. Di conseguenza, non supportano l'uso della parola chiave `new`.

```javascript
const Foo = () => {
  this.a = 1;
};

// var obj = new Foo(); // ERRORE: TypeError: Foo is not a constructor
```

## L'Operatore `new` Sovrascrive il Bind

Esiste una precisa gerarchia per le regole di binding: l'operatore `new` gode della precedenza massima, riuscendo addirittura a scavalcare l'invocazione di costruttori derivati da un _hard binding_.

```javascript
function Foo(name) {
  this.name = name;
}

var obj1 = {};
var Bar = Foo.bind(obj1);

Bar("obj1");
console.log(obj1.name); // "obj1" (modifica dell'oggetto hard-Bound)

var obj2 = new Bar("obj2");
console.log(obj1.name); // "obj1" (non ha subito ulteriori mutazioni)
console.log(obj2.name); // "obj2" (new ha regolarmente creato un nuovo oggetto, bypassando il bind preesistente)
```

## Utilizzo di `instanceof`

Per accertarsi che un dato oggetto figuri come esito corretto della catena di un costruttore, è possibile usare l'operatore `instanceof`.

```javascript
function Person(name) {
  this.name = name;
}

var mario = new Person("Mario");

console.log(mario instanceof Person); // true
console.log(mario instanceof Object); // true (tutti gli oggetti derivano tacitamente da Object)
```

L'operatore risale l'intera catena prototipale per constatare le parentele tra gli oggetti.
