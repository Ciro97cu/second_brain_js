# [[../../appunti-completi#scope-annidato-nested-scope|Errori di Scope e Variabili Globali Accidentali]]

La corretta gestione della scope chain nel linguaggio JavaScript implica necessariamente prevenire errori comuni legati alla ricerca di identificatori inesistenti o non disponibili, nonché all'inquinamento casuale ma massiccio delle variabili non strettamente dichiarate.

## ReferenceError nella Scope Chain

L'errore sincrono **ReferenceError** viene innescato omettendo identificatori, o quando si tenta specificamente di accedere ad un parametro o a una variabile assolutamente non disponibile né nello scope corrente in esecuzione né in alcuno degli scope più esterni.

```javascript
function test() {
  // console.log(inesistente);  // ❌ ReferenceError: inesistente is not defined
}

if (true) {
  let x = 10;
}
// console.log(x);  // ❌ ReferenceError: x is not defined (fuori dal block scope originario)
```

## Pericolo: Variabili Globali Accidentali

Un comportamento particolarmente insidioso e **pericoloso** dell'Engine JavaScript (laddove questo operi in modalità "non-stretta" o casuale) si verifica quando nel blocco di codice viene assegnato inopinatamente un valore a una variabile **non dichiarata** esplicitamente.

```javascript
function esempio() {
  x = 10; // ❌ Nessuna dichiarazione formale (var/let/const)
  // L'Engine risale la scope chain fino ad arrivare saldamente in cima
  // Non trovando 'x' esplicitata localmente da nessuna parte,
  // ne crea costantemente e AUTOMATICAMENTE una copia globale.
}

esempio();
console.log(x); // 10 (variabile globale creata accidentalmente nel sistema!)
```

### Rischi e Possibili Derivazioni delle Variabili Accidentali

1. **Inquinamento incontrollato**: Viene alterato drasticamente lo scope globale per cause ignote.
2. **Bug complessi e logoranti**: Strutture incrociate del codice finiscono con l'andare a sovrascrivere o interferire col medesimo puntatore. Trasformare dati in modo concorrenziale e confuso.
3. **Conflitti intrusivi**: Spesso nascondono parametri primari di importanza tecnica per le librerie importate, finendo con l'andare ad annullarne le procedure di utilità in favore di riferimenti superflui e imprevisti.

### Soluzione Pratica: Strict Mode

**Soluzione Definitiva**: L'utilizzo formale dell'annotazione per una modalità più severa imposta rigorosamente la pre-assegnazione delle dichiarazioni. Lo **strict mode** (`"use strict"`) interviene convertendo inesorabilmente gli assegnamenti accidentali verso identificatori "invisibili" in potenti e tempestivi **errori espliciti**.

```javascript
"use strict";

function test() {
  z = 10; // ❌ ReferenceError: z is not defined, interrotto dall'analisi statica/dinamica!
}
```
