# [[../../appunti-completi#descrittori-delle-proprietà-property-descriptors|Property Descriptors]]

Da ES5, ogni proprietà di un oggetto in JavaScript è associata a un insieme di attributi chiamato _Property Descriptor_ (Descrittore di Proprietà). Oltre al suo semplice `value`, il descrittore ne governa il comportamento per quanto riguarda modificabilità, visibilità e cancellazione.

## 🎯 Concetti Chiave

- **Writable**: Determina se il `value` di una proprietà può essere riassegnato in futuro.
- **Configurable**: Determina se la proprietà può essere cancellata tramite `delete` e se i suoi descrittori (come `enumerable` e `configurable` stesso) possono essere modificati successivamente. Un passaggio a `false` è **irreversibile**.
- **Enumerable**: Determina se la proprietà viene inclusa durante le iterazioni sulle proprietà di un oggetto (es. nei cicli `for..in` o tramite `Object.keys()`).

## 💻 Esempi di Codice

### Ispezione di un Descrittore Standard

Per i banali oggetti letterali, le proprietà nascono con tutti i flag liberi (\`true\`):

```javascript
let myObject = { a: 2 };

console.log(Object.getOwnPropertyDescriptor(myObject, "a"));
// { value: 2, writable: true, enumerable: true, configurable: true }
```

### Configurazione Manuale

Usando `Object.defineProperty()`, si può definire (o alterare) esplicitamente un descrittore:

```javascript
let obj = {};

Object.defineProperty(obj, "costante", {
  value: 42,
  writable: false, // Non può più cambiare valore
  configurable: false, // Non diventerà mai più configurable o cancellabile
  enumerable: true, // Sarà listata nei cicli for..in
});

obj.costante = 50; // Silently fails (o lancia TypeError in "use strict")
delete obj.costante; // Silently fails, la proprietà permane
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **La Trappola di Configurable**: Impostare `configurable: false` è un'operazione che "sbarra la porta". Qualsiasi tentativo successivo di usare `defineProperty` per reimpostarlo a `true` scagionerà un `TypeError`.
- ❌ **Confondere delete con memoria**: L'operatore `delete` si applica unicamente alle proprietà degli oggetti ed è inibito da `configurable: false`. Non invoca attivamente la gestione della memoria in stile C++, rompe solamente il riferimento e confida nel garbage collector in differita.

## ✅ Best Practices

- ✓ **Eccezione su configurable e writable**: Di norma un parametro `configurable: false` blocca qualsiasi modifica di descrittore, con una sola deroga: il parametro `writable` può sempre e comunque fare lo scalino al ribasso (passare da `true` a `false`), a prescindere dal limite di configurable.
- ✓ **Sfruttare enumerable passivi**: Per memorizzare metadati in un oggetto e contemporaneamente tenerli fuori dalla serializzazione JSON o dai map/reduce, basta definire esplicitamente `enumerable: false`.

## 🔗 Collegamenti

**Prerequisiti**:

- [[oggetti]]

**Correlati**:

- [[duplicazione-oggetti]]
