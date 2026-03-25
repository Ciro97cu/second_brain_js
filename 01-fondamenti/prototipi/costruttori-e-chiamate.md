# [[../../appunti-completi#89-costruttori-o-chiamate-costruttrici|Costruttori e Chiamate Costruttrici]]

In JavaScript non esistono funzioni che nascono formalmente come "costruttori" (stile classi OOP). L'illusione di avere dei costruttori è alimentata dall'uso della keyword `new` e dalla convenzione di usare l'iniziale maiuscola per i nomi delle funzioni (es. `function Foo() {}`).

In realtà, non esistono costruttori: esistono solo **chiamate costruttrici** (constructor calls).

L'operatore `new` inserito davanti a una normalissima chiamata di funzione "dirotta" l'esecuzione interna costringendola a fabbricare e restituire un nuovo oggetto (come "effetto collaterale"), oltre a eseguire il normale flusso di istruzioni dichiarato.

```javascript
function NothingSpecial() {
  console.log("Non farci caso!");
}

const a = new NothingSpecial(); // "Non farci caso!"
console.log(a); // {} -> L'oggetto è stato creato!
```

## 🎯 Il Trucco della Proprietà `.constructor`

Ogni volta che si dichiara una funzione, all'interno del suo oggetto `.prototype` viene generata in automatico una proprietà speciale, pubblica e non enumerabile: `.constructor`.
Questa proprietà punta direttamente alla funzione stessa in cui risiede.

```javascript
function Foo() {}

console.log(Foo.prototype.constructor === Foo); // true

const a = new Foo();
console.log(a.constructor === Foo); // true
```

Tale aspetto confonde: potrebbe sembrare che l'oggetto istanziato `a` indichi al suo interno "sono stato costruito da Foo".
Ma **l'oggetto `a` in realtà non possiede una proprietà `.constructor`**: la sta semplicemente _delegando_ a `Foo.prototype` lungo la catena. Inoltre, il termine assunto qui semanticamente non vuol dire che sia tracciata la reale azione costruttrice alle spalle.

## ⚠️ Gotcha / Errori Comuni

- ❌ Pensare che una funzione "Maiuscola" (es. `function User() {}`) riceva poteri o funzionalità speciali a runtime dal motore JS. Si tratta solo di una convenzione stilistica per comunicare tra sviluppatori che andrà usata con `new`.
- ❌ Ritenere che un oggetto contenga fisicamente la proprietà `.constructor` al momento dell'istanziazione. L'accesso avviene sempre tramite Delega (Prototype Chain), chiedendolo al `prototype` della funzione.

## 🔗 Collegamenti

**Prerequisiti**:

- [[illusione-classi|L'Illusione delle Classi e le Funzioni Costruttrici]]
- [[ereditarieta-prototipale-delega|Ereditarietà Prototipale e Delega]]

**Tags**: `#javascript` `#prototype` `#costruttori` `#oop`
