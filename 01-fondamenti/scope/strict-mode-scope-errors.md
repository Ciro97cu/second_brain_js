# [[../../appunti-completi#errori|Strict Mode e Scope Errors]]

Il comportamento del motore JavaScript di fronte a un fallimento nella ricerca di una variabile (in particolare durante un assegnamento, noto come **LHS** o Left-Hand Side lookup) varia drasticamente in base alla modalità di esecuzione.

## Modalità Non-Strict (Default)

In modalità non-strict, una ricerca LHS fallita non provoca un errore. Al contrario, causa la **creazione automatica** di una variabile nell'oggetto globale (es. `window` nei browser).

```javascript
// NON-STRICT: crea variabile globale accidentale
function assegna(a) {
  // 'b' non è mai stata dichiarata nello scope attuale o in quelli esterni
  b = a * 2;
}

assegna(5);
console.log(b); // 10 (variabile globale creata accidentalmente)
console.log(window.b); // 10 (in ambienti browser)
```

Questo comportamento porta frequentemente a inquinamento dello scope globale e a bug difficili da tracciare all'interno delle applicazioni.

## Strict Mode

Apponendo la direttiva `"use strict"` all'inizio di un modulo o funzione, si entra in **strict mode**. In questa modalità, l'Engine JavaScript previene la creazione automatica delle variabili; una ricerca LHS fallita genera un **ReferenceError**, allineando il comportamento a quello di una ricerca RHS (Right-Hand Side, recupero del valore).

```javascript
"use strict";

function assegna(a) {
  b = a * 2; // ❌ ReferenceError: b is not defined
  // In strict mode è IMPEDITA la creazione automatica
}

assegna(5); // Errore bloccante!
```

## Best Practices

Si raccomanda di utilizzare sempre lo **strict mode** per tutti i progetti moderni, in modo da prevenire inneschi accidentali legati allo scope. I moduli ES6 (ES Modules) abilitano automaticamente questa funzionalità senza bisogno della dichiarazione esplicita iniziale.

```javascript
// Dichiarare sempre le variabili
function calcola() {
  let risultato = 10; // ✅ Dichiarazione esplicita invece di auto-globale accidentale
}
```
