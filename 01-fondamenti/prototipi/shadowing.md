# [[../../appunti-completi#83-shadowing-oscuramento-nellassegnazione|Shadowing e Assegnazione]]

Lo **Shadowing** (o oscuramento) si verifica quando si assegna (`[[Put]]`) una proprietà a un oggetto (`myObject.foo = "bar"`), ma `foo` è già presente più in alto nella sua catena dei prototipi.

La proprietà `foo` viene creata direttamente in `myObject`, oscurando la versione originale.

Se `foo` si trova _solo_ sul prototipo superiore, ci sono 3 scenari in cui si suddivide l'assegnazione:

1. **Scrivibile**: Se la proprietà nel prototipo ha `writable: true`, l'assegnazione aggiunge regolarmente `foo` al nostro `myObject`, creando a tutti gli effetti lo `shadowing`.
2. **Read-only**: Se nel prototipo superiore ha `writable: false`, `foo` in `myObject` **non viene aggiunto**, l'operazione fallisce o in Modalità Rigida (Strict Mode), lancia un Errore. Lo shadowing non avviene affatto.
3. **Setter**: Se nel prototipo c'è un Setter associato al nome (es. `set foo() { ... }`), scatta l'esecuzione di tale setter. La proprietà aggiuntiva su `myObject` **non viene** posta come shadowing, perché la chiamata viene intercettata originariamente.

## Shadowing Implicito

Lo shadowing può crearsi accidentalmente, come con l'operatore di incremento `++`, che equivale a `[[Get]]` + `[[Put]]`.

```javascript
const obj2 = { a: 2 };
const obj1 = Object.create(obj2);

console.log(obj1.a); // 2
console.log(obj2.a); // 2

// obj1.a = obj1.a + 1
obj1.a++;

// Lo shadowing implicito è scattato:
console.log(obj1.a); // 3 (Proprietà nuova!)
console.log(obj2.a); // 2
```

## 🔗 Collegamenti

**Prerequisiti**:

- [[../../appunti-completi#81-prototype-e-la-catena|La Catena dei Prototipi `[[Prototype]]`]]
