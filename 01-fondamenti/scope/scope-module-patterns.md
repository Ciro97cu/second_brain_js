# [[../../appunti-completi#gestione-dei-moduli-module-management|Pattern e Vantaggi dei Moduli]]

I moduli offrono notevoli vantaggi nel gestire lo scope e nell'evitare collisioni tra dipendenze, superando le limitazioni dei classici namespace globali in JavaScript.

## Namespace vs Moduli

Il pattern classico dei namespace si basa su oggetti globali, non offrendo una vera privacy. Le proprietà "private" spesso vengono solo designate da convenzioni di naming.

### Namespace (Approccio Classico)

Nel pattern Namespace l'incapsulamento non è reale:

```javascript
var App = {
  _privateHelper: function () {
    /* ... */
  }, // Convenzione, ma di fatto accessibile
  publicMethod: function () {
    /* ... */
  },
};

App._privateHelper(); // ⚠️ L'accesso è comunque possibile (niente vera privacy)
```

### Moduli (Approccio Moderno)

Con i moduli l'incapsulamento è garantito, e i dati non esportati diventano inaccessibili.

```javascript
// === utils.js ===
function privateHelper() {
  /* vera privacy, solo accessibile all'interno del modulo */
}
export function publicMethod() {
  privateHelper();
}

// === app.js ===
import { publicMethod } from "./utils.js";
publicMethod(); // ✅ OK
// privateHelper(); // ❌ ReferenceError (vera privacy garantita!)
```

## Strumenti per la Prevenzione Collisioni

Visto che i moduli lavorano con la visibilità nello scope locale in cui vengono importati, è facile trovarsi a gestire librerie differenti che offrono elementi con nomi identici.

E' possibile evitare questi problemi ricorrendo ad alias per separare le referenze.

```javascript
// === math.js ===
export function add(a, b) {
  return a + b;
}

// === app.js ===
// Immaginando due librerie che definiscano una funzione 'add'
import { add as mathAdd } from "./math.js";
import { add as stringAdd } from "./string-utils.js";

mathAdd(2, 3); // 5
stringAdd("hello", "world"); // 'helloworld'
// Nessun conflitto poichè sono stati assegnati alias differenti!
```

## Vantaggi dei Moduli

L'utilizzo dei moduli porta benefici chiave nell'architettura delle applicazioni JS moderne:

1. **Vera Privacy**: L'incapsulamento è reale, non fondato su convenzioni.
2. **Zero Global Pollution**: Non esistono inquinante variabili nel blocco globale (global object).
3. **Dipendenze Esplicite**: Vengono indicati chiaramente gli import necessari ad un modulo.
4. **Prevenzione Collisioni**: Questa operazione è automatica tramite sistemi di scope separati per ogni modulo.
5. **Tree Shaking**: I bundler hanno la possibilità di rimuovere il codice non utilizzato.
6. **Code Splitting**: Possibilità di un caricamento ritardato (lazy loading) dei moduli, che vengono chiamati solo quando occorrono.
7. **Manutenibilità**: Il flusso delle dipendenze è sempre chiaro da leggere e tracciabile.
