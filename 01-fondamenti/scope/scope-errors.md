# [[../../appunti-completi#errori|Errori di Scope: ReferenceError vs TypeError]]

Gli errori legati allo scope si dividono in due categorie principali: **ReferenceError** (variabile non trovata) e **TypeError** (operazione illegale su variabile esistente).

## 🎯 Concetto Chiave

La distinzione tra **ricerche LHS** (assegnamento) e **RHS** (recupero valore) è fondamentale: hanno comportamenti diversi quando una variabile **non viene trovata** nella scope chain.

### ReferenceError: Variabile Non Trovata

Quando l'Engine **non trova una variabile** in nessuno scope della catena (fino al globale), solleva un **ReferenceError**.

**Ricerca RHS fallita** (recupero valore):

```javascript
function foo(a) {
  console.log(a + b); // ❌ ReferenceError: b is not defined
}

foo(2);
// Engine cerca 'b' per leggerne il valore (RHS)
// Scope di foo → ❌ Non trovato
// Scope globale → ❌ Non trovato
// → ReferenceError
```

**Ricerca LHS fallita** (assegnamento):
Il comportamento dipende dalla **modalità** (Strict o Non-Strict).

## 💻 Strict Mode vs Non-Strict

### Modalità Non-Strict (Default)

In modalità **non-strict**, una ricerca LHS fallita provoca la **creazione automatica** di una variabile globale.

```javascript
// NON-STRICT: crea variabile globale accidentale
function assegna(a) {
  b = a * 2; // ❌ 'b' non dichiarata → creata nello scope globale!
}

assegna(5);
console.log(b); // 10 (variabile globale accidentale)
console.log(window.b); // 10 (in browser)
```

⚠️ **Pericolo**: Inquinamento dello scope globale, bug difficili da tracciare.

### Strict Mode

In **strict mode**, una ricerca LHS fallita genera un **ReferenceError**, proprio come RHS.

```javascript
"use strict";

function assegna(a) {
  b = a * 2; // ❌ ReferenceError: b is not defined
  // Strict mode IMPEDISCE la creazione automatica
}

assegna(5); // Errore!
```

✅ **Best Practice**: Usa sempre `"use strict"` per prevenire variabili globali accidentali.

## ⚖️ ReferenceError vs TypeError

### ReferenceError

**Causa**: Fallimento nella **risoluzione dello scope** (variabile non trovata).

```javascript
console.log(variabileInesistente); // ❌ ReferenceError: variabileInesistente is not defined

function test() {
  return altroNome * 2; // ❌ ReferenceError: altroNome is not defined
}
```

### TypeError

**Causa**: Scope risolto correttamente (variabile trovata), ma **operazione illegale** sul valore.

```javascript
let numero = 42;
numero(); // ❌ TypeError: numero is not a function
// 'numero' esiste, ma non è una funzione

let obj = null;
console.log(obj.proprieta); // ❌ TypeError: Cannot read property 'proprieta' of null
// 'obj' esiste, ma è null

const PI = 3.14;
PI = 3.14159; // ❌ TypeError: Assignment to constant variable
// 'PI' esiste, ma è const
```

## ⚠️ Distinzione Fondamentale

| Errore             | Significato                       | Causa                           |
| ------------------ | --------------------------------- | ------------------------------- |
| **ReferenceError** | "Non ho trovato la variabile"     | Problema di **scope**           |
| **TypeError**      | "Trovata, ma operazione illegale" | Problema di **tipo/operazione** |

```javascript
let persona = { nome: "Mario" };

// ReferenceError: variabile non dichiarata
console.log(altriDati); // ❌ ReferenceError

// TypeError: variabile esiste, operazione illegale
console.log(persona.saluta()); // ❌ TypeError: persona.saluta is not a function
```

## ✅ Best Practices

**Usa strict mode**: Previene creazione automatica di variabili globali.

```javascript
"use strict";
// All'inizio del file o della funzione
```

**Dichiara sempre le variabili**: Usa `let`, `const` o `var` esplicitamente.

```javascript
// ❌ Evita
function calcola() {
  risultato = 10; // Globale accidentale (non-strict)
}

// ✅ Corretto
function calcola() {
  let risultato = 10; // Dichiarazione esplicita
}
```

**Gestisci gli errori appropriatamente**: ReferenceError vs TypeError richiedono strategie diverse.

```javascript
try {
  console.log(variabileInesistente);
} catch (error) {
  if (error instanceof ReferenceError) {
    console.log("Variabile non dichiarata");
  } else if (error instanceof TypeError) {
    console.log("Operazione illegale");
  }
}
```

## 🔗 Collegamenti

- [[scope-chain]] - Meccanismo di ricerca delle variabili
- [[scope]] - Concetti base dello scope
- [[../variabili/variabili]] - Dichiarazione variabili (LHS)

## 📚 Risorse Esterne

- [MDN: ReferenceError](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ReferenceError) - Documentazione ReferenceError
- [MDN: TypeError](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypeError) - Documentazione TypeError
- [MDN: Strict Mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode) - Strict mode in dettaglio

## 📌 Note Aggiuntive

- **ReferenceError** si verifica **prima** dell'esecuzione (durante la risoluzione dello scope)
- **TypeError** si verifica **durante** l'esecuzione (quando si tenta l'operazione)
- Lo **strict mode** è raccomandato per tutti i progetti moderni (ES6+ lo abilita automaticamente nei moduli)
- Accedere a proprietà **non esistenti** di un oggetto esistente restituisce `undefined`, **NON ReferenceError**
