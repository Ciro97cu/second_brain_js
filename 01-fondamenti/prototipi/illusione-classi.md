# [[../../appunti-completi#85-lillusione-delle-classi-in-javascript|L'Illusione delle Classi e le Funzioni Costruttrici]]

A differenza dei linguaggi _class-oriented_, in JavaScript non esistono strati astratti (le "classi") da cui copiare e fabbricare fisicamente gli oggetti. JavaScript possiede solo oggetti nativi che si collegano direttamente fra loro.

Per scimmiottare l'aspetto e il comportamento delle classi convenzionali, per anni si è abusato di una caratteristica nascosta delle funzioni.

Ogni funzione dichiarata ottiene nativamente una proprietà non enumerabile di nome `prototype`, che punta a un oggetto solitario in memoria.

```javascript
function Foo() {
  // ...
}

console.log(Foo.prototype); // { } - Oggetto verso cui punta nativamente la funzione
```

## L'effetto della keyword `new`

Quando si crea un oggetto anteponendo la parola chiave `new` davanti alla chiamata di funzione (`new Foo()`), si forza il motore a generare un nuovo oggetto. Quel nuovo oggetto viene magicamente **collegato**, tramite il proprio cordone ombelicale `[[Prototype]]`, allo stesso ed identico oggetto puntato da `Foo.prototype`.

```javascript
/* Lines 123-456 omitted ... */
const a = new Foo(); // Chiamata della funzione Costruttrice

console.log(Object.getPrototypeOf(a) === Foo.prototype); // true
```

Tale operazione non esegue alcuna copia genetica, tipica invece della formale ereditarietà classica. Con la direttiva `new`, ci si ritrova unicamente con "un oggetto collegato a un altro". Si è forzata una semplice connessione di Delega facendola passare subdolamente per un'Ereditarietà di stampo classista.

## 🔗 Collegamenti

**Prerequisiti**:

- [[catena-prototipi|La Catena dei Prototipi]]

**Approfondimenti**:

- [[ereditarieta-prototipale-delega|Ereditarietà Prototipale e Delega]]
