# [[../../appunti-completi#85-lillusione-delle-classi-in-javascript|L'Illusione delle Classi e le Funzioni Costruttrici]]

A differenza dei linguaggi _class-oriented_, in JavaScript non esistono strati astratti ("le classi") da cui copiare e fabbricare fisicamente gli oggetti come da stampino. JavaScript possiede solo oggetti nativi crudi e malleabili che si collegano dinamicamente tra loro.

## 🎯 Concetti Chiave

- **Il Trucco Storico della Funzione**: Per scimmiottare l'aspetto e l'organigramma formale delle classi convenzionali, la community per anni ha pesantemente abusato di una caratteristica nascosta intrinseca alla natura delle funzioni.
- **La proprietà `prototype` nativa**: Ogni tipica funzione regolare dichiarata in memoria ottiene alla nascita una dotazione preimpostata speciale (non enumerabile) di nome `.prototype`. Questo pointer aggancia in automatico la funzione appena battuta ad un parallelo e solitario oggetto vergine in un cassetto limitrofo dello stack.

## 💻 Esempi di Codice

### L'effetto manipolato della keyword `new`

In OOP classiche, stampando a schermo un neo-costrutto `new Foo()` si estrae una copia rigida staccata dalla madre. In JS si forza il motore a partorire un nuovo oggetto slegandosi dall'idea di "Copia genetica".

```javascript
function Foo() {
  // ...
}

console.log(Foo.prototype); // { } - Oggetto asettico agganciato nativamente

const a = new Foo(); // Chiamata della funzione scatenante.

// Qual è l'effetto di new?
console.log(Object.getPrototypeOf(a) === Foo.prototype); // true
```

_Effetto_: Anteponendo la parola chiave `new`, tale oggetto appena partorito subisce l'allacciamento, tramite il suo invisibile cordone ombelicale interno `[[Prototype]]`, incatenandolo di forza alla medesima capsula asettica appuntata originariamente da `Foo.prototype`.

## ⚠️ Gotcha / Errori Comuni

- ❌ **Equivocare su Ereditarietà di stampo classista**: Non c'è copia! Con la direttiva magica `new` ci si ritrova impiantati unicamente con "un oggetto nuovo in pugno forzatamente appoggiato a un altro". Trattasi a tutti gli effetti di una semplice e robusta connessione di **Delega**. Fallisce integralmente l'associazione all'Ereditarietà convenzionale.

## ✅ Best Practices

- ✓ **Lessico e Mindset**: Per padroneggiare fluidamente il linguaggio non si deve tentare mentalmente di appiattirne l'ecosistema imitando le forzature delle classi di altre sintassi o di esplicite estensioni formali; si deve guardare a queste relazioni per quello che biologicamente le anima di logica (il Pattern Delega).

## 🔗 Collegamenti

**Prerequisiti**:

- [[catena-prototipi|La Catena dei Prototipi]]

**Approfondimenti**:

- [[ereditarieta-prototipale-delega|Ereditarietà Prototipale e Delega]]
- [[costruttori-e-chiamate|Costruttori e Chiamate Costruttrici]]

## 📚 Riferimenti

- [MDN - Objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)

## 📌 Note Personali

---

**Tags**: `#javascript` `#classi` `#prototype` `#new` `#oop`
