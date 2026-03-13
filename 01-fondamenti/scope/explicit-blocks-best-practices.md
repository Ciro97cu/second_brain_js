# [[../../appunti-completi#blocchi-come-scope-blocks-as-scopes|Blocchi Espliciti e Best Practices nel Block Scope]]

## 📦 Blocchi Espliciti per Chiarezza

Usare `let` per legare una variabile a un blocco pre-esistente (come un `if` o un `for`) può essere **implicito**. Per maggiore chiarezza nel codice e visibilità dello scope, si possono creare **blocchi espliciti** standalone:

```javascript
// Approccio IMPLICITO (blocco pre-esistente)
if (foo) {
  let bar = foo * 2; // 'bar' legato al blocco if
  // ...
}

// Approccio ESPLICITO (blocco dedicato)
if (foo) {
  {
    // Blocco esplicito per 'bar'
    let bar = foo * 2;
    console.log(bar);
  }

  // 'bar' NON esiste qui
  // console.log(bar); // ReferenceError
}
```

Vantaggi di incapsulare l'operazione in un `{}` arbitrario:

- ✅ Trasmette più chiaro ed intuitivo dove le variabili sono confinate
- ✅ Rende più facile spostare il blocco isolato durante le fasi di refactoring
- ✅ Non altera la semantica dell'istruzione `{}` (ad es. `if`) che lo contiene all'esterno

### 📌 Pattern per Variabili Temporanee

```javascript
function processData(data) {
  // Blocco esplicito per calcoli intermedi
  {
    let temp = data * 2;
    let adjusted = temp + 10;
    data = adjusted;
  }

  // 'temp' e 'adjusted' non inquinano questo scope della funzione genitore (processData)
  // console.log(temp); // ❌ ReferenceError

  return data;
}
```

## ✅ Best Practices nell'Uso di Block Scope

Quando si scrive una base di codice solida e sicura nei confronti dell'inquinamento di informazioni, si tende ad adottare regole stringenti che limitano la visibilità alle componenti interessate.

1. **Usa `const` per default** - Se la direttiva imposta non verrà alterata tramite riassegnazione, si consiglia sempre di usare la parola chiave `const` per enfatizzare tale intento ai colleghi programmatori.
2. **Usa `let` solo quando strettamente necessario riassegnare** - Più esplicito nell'intento, garantisce il confine e permette la riassegnazione su contatori o puntatori mutevoli nel design.
3. **Evita `var`** - La sua valutazione si basa sullo scope funzionale, con tanti comportamenti contro-intuitivi che provocano shadow silenti ed il "falso block scope".
4. **Confina le variabili ai blocchi più piccoli possibili** - Principi di sicurezza come il **Principio del Minimo Privilegio**.
5. **Crea blocchi espliciti** - Costruire blocchi sintattici liberi per variabili isolate, temporanee ed importanti è un patter sicuro.
6. **Dichiara variabili prima del loro uso** - Anticipa i fallimenti legati alla **Temporal Dead Zone (TDZ)** dichiarata durante la transizione al block scope di ES6.

## 🔗 Concetti Correlati

- [[lexical-scope-base|Scope Lessicale]]
- [[nested-scope|Scope Annidato]]
- [[block-scope-memory|Block Scope e Memory]]
- [[../variabili/hoisting|Hoisting delle Variabili]]
- [[function-hoisting|Hoisting delle Funzioni]]
