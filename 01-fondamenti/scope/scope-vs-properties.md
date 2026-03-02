# [[../../appunti-completi#scope-lessicale-vs-accesso-a-proprietà|Scope vs Proprietà Oggetti]]

La **ricerca dello scope** e l'**accesso alle proprietà** sono meccanismi diversi con regole e comportamenti distinti.

## 🎯 Concetto Chiave

Quando scrivi `oggetto.proprietà.valore`, lo **scope lessicale** si applica solo per trovare `oggetto`. Poi subentra l'**accesso alle proprietà** per `proprietà` e `valore`.

### Differenza Fondamentale

```javascript
let obj = {
  livello1: {
    valore: 42,
  },
};

function test() {
  // SCOPE LESSICALE: cerca 'obj'
  // 1. Scope di test → ❌
  // 2. Scope globale → ✅ Trovato!

  // PROPRIETÀ OGGETTO: accede a 'livello1' e 'valore'
  console.log(obj.livello1.valore); // 42
}

test();
```

**Regola chiave**: Scope per il **primo identificatore**, proprietà per il **resto della catena**.

## ⚠️ Comportamento degli Errori

Gli errori sono **completamente diversi** tra scope e proprietà.

### ReferenceError vs undefined

```javascript
let obj = { x: 10 };

// SCOPE LESSICALE: variabile non trovata → ReferenceError
// console.log(variabileNonEsiste); // ❌ ReferenceError

// PROPRIETÀ OGGETTO: proprietà non trovata → undefined
console.log(obj.proprietaNonEsiste); // undefined (NON errore!)
```

| Situazione      | Scope Lessicale    | Proprietà Oggetto |
| --------------- | ------------------ | ----------------- |
| Non trovato     | **ReferenceError** | **undefined**     |
| Tipo di ricerca | Scope chain        | Prototype chain   |
| Si ferma a      | Scope globale      | `null` prototype  |

## 💻 Esempi Pratici

### Confronto Completo

```javascript
let x = 10;
let obj = {
  x: 20,
  y: 30,
};

function mostra() {
  // 'x' → SCOPE LESSICALE (trova 10)
  console.log(x); // 10

  // 'obj.x' → SCOPE per 'obj' + PROPRIETÀ per 'x'
  console.log(obj.x); // 20

  // 'obj.y' → SCOPE per 'obj' + PROPRIETÀ per 'y'
  console.log(obj.y); // 30

  // 'obj.z' → SCOPE per 'obj' ✅ + PROPRIETÀ per 'z' ❌
  console.log(obj.z); // undefined (NON ReferenceError!)

  // 'z' → SCOPE LESSICALE (non trova in nessuno scope)
  // console.log(z); // ❌ ReferenceError: z is not defined
}

mostra();
```

### Catena Complessa

```javascript
let config = {
  server: {
    host: "localhost",
    port: 3000,
  },
};

function connetti() {
  // SCOPE LESSICALE: cerca 'config'
  // 1. Scope di connetti → ❌
  // 2. Scope globale → ✅ Trovato!

  // PROPRIETÀ: 'server', 'host'
  let host = config.server.host; // ✅ "localhost"

  function stampaInfo() {
    // SCOPE LESSICALE: cerca 'host'
    // 1. Scope di stampaInfo → ❌
    // 2. Scope di connetti → ✅ Trovato!
    console.log(host); // "localhost"

    // SCOPE: 'config' | PROPRIETÀ: 'server', 'port'
    console.log(config.server.port); // 3000
  }

  stampaInfo();
}

connetti();
```

## 🔍 Scope vs Prototype Chain

```javascript
// SCOPE: cerca negli scope annidati
// PROTOTYPE: cerca nella catena dei prototipi

let obj = Object.create({ ereditato: "valore" });
obj.proprio = "mio";

function test() {
  // 'obj' → SCOPE LESSICALE
  console.log(obj.proprio); // "mio" (proprietà propria)

  // 'obj.ereditato' → SCOPE per 'obj', PROTOTYPE per 'ereditato'
  console.log(obj.ereditato); // "valore" (proprietà ereditata)

  // 'variabileNonEsiste' → SCOPE LESSICALE (fallisce)
  // console.log(variabileNonEsiste); // ❌ ReferenceError
}

test();
```

## ✅ Best Practices

**Distingui sempre scope da proprietà**: Comportamenti diversi.

```javascript
// ✅ Chiaro: scope per 'utente', proprietà per 'nome'
let utente = { nome: "Mario" };
console.log(utente.nome);

// ✅ Gestisci appropriatamente gli errori
try {
  console.log(variabileNonEsiste); // ReferenceError
} catch (error) {
  console.log("Variabile non in scope");
}

// ✅ Controlla proprietà mancanti
if (utente.cognome !== undefined) {
  console.log(utente.cognome);
}
```

**Usa optional chaining per proprietà**: Evita errori.

```javascript
// ❌ Potenziale TypeError
// console.log(obj.inner.value); // Se 'inner' è undefined

// ✅ Optional chaining
console.log(obj?.inner?.value); // undefined se manca
```

**Ricorda la distinzione negli errori**: Debug più facile.

```javascript
// ReferenceError → Problema di scope (variabile non dichiarata)
// TypeError → Problema di proprietà (oggetto null/undefined)
// undefined → Proprietà mancante (ma oggetto esiste)
```

## 🔗 Collegamenti

- [[lexical-scope-base]] - Scope lessicale base
- [[scope-lookup]] - Processo di look-up
- [[scope-window]] - Oggetto window
- [[../oggetti/prototype]] - Prototype chain

## 📌 Note Aggiuntive

- Lo **scope lessicale** si applica solo al **primo identificatore**
- L'accesso alle **proprietà** usa la **prototype chain**, non la scope chain
- **ReferenceError** = scope | **undefined** = proprietà mancante
- Non confondere: `obj.prop` (proprietà) vs `variable` (scope)
