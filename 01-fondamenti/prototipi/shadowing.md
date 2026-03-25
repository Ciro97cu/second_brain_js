# [[../../appunti-completi#83-shadowing-oscuramento-nellassegnazione|Shadowing e Assegnazione]]

Lo **Shadowing** (o oscuramento) si verifica tramite un blocco visivo durante un'operazione di Set (`[[Put]]`). Avviene quando si tenta di assegnare una proprietà a un oggetto, la quale è invece già presente più in alto nella gerarchia (Catena dei Prototipi).

## 🎯 Concetti Chiave

- **3 Scenari Imprevedibili**: A seconda di come la proprietà originale è definita nel prototipo superiore, l'assegnazione della nuova proprietà nell'oggetto "figlio" muta radicalmente risultato.
- **Caso 1 (Scrivibile)**: Se il prototipo ha `writable: true`, il linguaggio crea la nuova proprietà sull'oggetto figlio e ignora perennemente l'originale del genitore in tutte le successive consultazioni. Questo è lo Shadowing classico e corretto.
- **Caso 2 (Solo Lettura)**: Se la proprietà originale ha `writable: false`, JS ferma l'operazione in maniera silente (o lancia errore in Strict Mode). L'oscuramento non avviene e l'oggetto figlio non riceverà alcun nuovo dato.
- **Caso 3 (Setter Intercettivo)**: Se in cima alla catena c'è un Setter con lo stesso nome, questo fa da calamita intercettando e consumando la richiesta. La proprietà extra non viene creata nel figlio.

## 💻 Esempi di Codice

### L'Illusione Implicita (`++`)

L'operatore di incremento crea insidiosi bug in merito perché maschera l'operazione. Equivale ad un `[[Get]]` (per analizzare il numero superiore) per po far scattare un `[[Put]]` (il base tenterà di schiantarci l'assegnazione generando Shadowing istantaneo).

```javascript
const obj2 = { a: 2 };
const obj1 = Object.create(obj2);

console.log(obj1.a); // 2 (Del genitore)
console.log(obj2.a); // 2 (Del genitore)

// obj1.a = obj1.a + 1
obj1.a++;

// Lo shadowing implicito è scattato:
console.log(obj1.a); // 3 (Proprietà nuova e disgiunta!)
console.log(obj2.a); // 2 (L'originale è salvo ma oscurato per obj1)
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Sovrascrivere per Modificare**: Molti programmatori causano Shadowing quando il loro scopo primario era in realtà modificare la fonte superiore. Se si vuole modificare lo standard ereditato, non si deve fare `child.prop = "X"`, altrimenti il costrutto si scollega incapsulando il nuovo dato localmente. Bisogna risalire e mutare in scala l'originale.

## ✅ Best Practices

- ✓ **Definizione Forzata**: Per aggirare i limitanti Casi 2 e 3 descritti sopra, se strettamente necessario oscurare o imporre la regola al figlio per aggirare i divieti della catena, si consiglia vivamente l'uso asettico di `Object.defineProperty(...)`.

## 🔗 Collegamenti

**Prerequisiti**:

- [[../../appunti-completi#81-prototype-e-la-catena|La Catena dei Prototipi `[[Prototype]]`]]

## 📚 Riferimenti

- [MDN - Prototypes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)

## 📌 Note Personali

---

**Tags**: `#javascript` `#prototype` `#shadowing` `#objects`
