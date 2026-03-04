# [[../../appunti-completi#310-il-pattern-modulo-modules|ES6 Modules: Moduli Futuri]]

## Supporto Nativo per i Moduli

ES6 introduce un supporto sintattico di prima classe per il concetto di moduli. Quando caricato tramite il sistema di moduli, ES6 tratta ogni file come un modulo separato. Ogni modulo può sia importare altri moduli o membri specifici di un'API, sia esportare i propri membri dell'API pubblica.

## API Statiche vs Runtime

A differenza dei moduli basati su funzioni, che non sono un pattern staticamente riconosciuto dal compilatore (e la cui semantica viene considerata solo a runtime), le **API dei moduli ES6 sono statiche**. Questo significa che l'API non cambia a runtime.

### Vantaggi dell'Analisi Statica

Poiché il compilatore è a conoscenza di ciò, può verificare durante la compilazione (e il caricamento del file) che un riferimento a un membro di un modulo importato esista effettivamente. Se il riferimento non esiste, il compilatore solleva un **errore "early"** al momento della compilazione, invece di attendere la risoluzione dinamica a runtime.

## Caratteristiche dei Moduli ES6

I moduli ES6 **non hanno un formato "inline"**; devono essere definiti in **file separati** (uno per modulo). I browser e gli engine dispongono di un "module loader" predefinito che carica in modo sincrono un file di modulo quando viene importato.

## Esempio Pratico Multi-File

Si consideri il seguente esempio suddiviso in file:

### bar.js

```javascript
function hello(who) {
  return "Let me introduce: " + who;
}

export hello;
```

### foo.js

```javascript
// import solo `hello()` dal modulo "bar"
import hello from "bar";

var hungry = "hippo";

function awesome() {
  console.log(hello(hungry).toUpperCase());
}

export awesome;
```

### baz.js

```javascript
// import dell'intero modulo "foo" e "bar"
module foo from "foo";
module bar from "bar";

console.log(bar.hello("rhino")); // Let me introduce: rhino
foo.awesome(); // LET ME INTRODUCE: HIPPO
```

## Keywords dei Moduli ES6

### `import`

Importa uno o più membri dall'API di un modulo nello Scope corrente, legandoli a una variabile (es. hello).

```javascript
import hello from "bar";
```

### `module`

**Nota**: Nella specifica finale ES6 standardizzata come `import * as name`

Importa l'intera API del modulo.

```javascript
// Sintassi originale (esempio teorico)
module foo from "foo";

// Sintassi standard ES6
import * as foo from "foo";
```

### `export`

Esporta un identificatore (variabile, funzione) nell'API pubblica del modulo corrente.

```javascript
export function hello(who) {
  return "Hello, " + who;
}
```

## Scope Closure nei Moduli ES6

Il contenuto all'interno del file del modulo viene trattato come se fosse racchiuso in una **Scope Closure**, esattamente come accade con i moduli basati su funzioni visti in precedenza.

Tutto ciò che non viene esplicitamente esportato rimane privato al modulo.

## ✅ Punti Chiave

1. **API Statiche** - Verificate a compile-time, non a runtime
2. **Early Errors** - Errori rilevati prima dell'esecuzione
3. **File Separati** - Un modulo = un file (no inline)
4. **Module Loader Nativo** - Browser/engine caricano automaticamente
5. **Scope Closure** - Stessa privacy dei moduli basati su funzioni
6. **import/export** - Keywords native del linguaggio

## 🔗 Collegamenti

- [[module-pattern|Module Pattern]] - Pattern basato su funzioni
- [[module-dependency-managers|Dependency Managers]] - Gestori precedenti a ES6
- [[../scope/module-management|Module Management]] - Panoramica sistemi moduli
- [[closure-concept|Closure]] - Base della privacy nei moduli
- [[../../appunti-completi#310-il-pattern-modulo-modules|Module Pattern Completo]]

## 📚 Risorse

- MDN: JavaScript Modules
- "You Don't Know JS" - ES6 & Beyond
- ECMAScript 2015 Specification

## 📌 Tag

#javascript #es6-modules #import #export #static-analysis #module-loader #esm
