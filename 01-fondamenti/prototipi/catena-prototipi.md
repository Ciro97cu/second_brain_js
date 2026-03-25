# [[../../appunti-completi#81-prototype-e-la-catena|La Catena dei Prototipi (`[[Prototype]]`)]]

In JavaScript, quasi tutti gli oggetti possiedono una proprietà di sistema, interna e nascosta chiamata `[[Prototype]]`. Essa costituisce fondamentalmente un ponte di collegamento vivo verso un altro oggetto.

## 🎯 Concetti Chiave

- **Ricerca a Ritroso**: Quando il motore JS esegue una specifica operazione di ispezione o lettura (come operazione `[[Get]]`) e non rileva immediatamente la proprietà nativamente nel nucleo locale, non rilascia errore, ma perlustra ciecamente seguendo il collegamento prototipale riversandolo all'oggetto interconnesso superiore.
- **Ciclo senza Fine**: Se l'elemento manca anche lì, continua inesorabile a risalire la gerarchia da padre in padre. Questo esatto e laborioso percorso vitale prende il nome perentorio di **Catena dei Prototipi**.
- **The End (`Object.prototype`)**: La caccia non dura all'infinito: si esaurisce solo in caso di ritrovamento andato a buon fine, o inevitabilmente incagliandosi toccando il fondo (in questo caso tecnicamente "la cima") globale che corrisponde formalmente all'entità maestra nota come `Object.prototype` (il cuore o fondamento del linguaggio che fornisce le basi universali standard per chi non le dispone in pancia nativamente).

## 💻 Esempi di Codice

### Esempio Base della Catena

```javascript
/* Il link del prototype tramite Object.create */

const anotherObject = { a: 2 };

// myObject viene collegato ad anotherObject
const myObject = Object.create(anotherObject);

// "a" non esiste qui: JS esplora e lo intercetta magicamente in "anotherObject"
console.log(myObject.a); // 2
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **La trappola del Null (`undefined`)**: Non riuscire a localizzare la metrica una volta raggiunta e oltrepassata la punta abissale di `Object.prototype`, fa rilasciare silenziosamente ed esclusivamente il classico valore standard associato a un'assenza insondabile, ovvero `undefined`.

## ✅ Best Practices

- ✓ **Attenzione ai Loop Orizzontali (`for..in`)**: Cicli che iterano tra le stringhe e le chiavi o interrogazioni d'esistenza booleane (`in`), navigano passivamente intercettando risposte da tutte le componenti radicate per tutta l'intera spina dorsale della gerarchia interconnessa, appesantendo e mescolando in output i dati fusi assieme dalle singole schede. Per scansare questo gap occorre filtrare con una verifica di non appoggio incrociata (`.hasOwnProperty()`).

## 🔗 Collegamenti

**Approfondimenti**:

- [[shadowing|Shadowing e Assegnazione]]
- [[ereditarieta-prototipale-delega|Ereditarietà Prototipale e Delega]]

## 📚 Riferimenti

- [MDN - Inheritance and Prototype Chain](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)

## 📌 Note Personali

---

**Tags**: `#javascript` `#prototype` `#chain` `#objects`
