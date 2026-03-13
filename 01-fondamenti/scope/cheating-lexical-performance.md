# [[../../appunti-completi#barare-con-lo-scope-lessicale-cheating-lexical|Scope Lessicale: Impatto sulle Performance]]

## ⚡ Impatto sulle Ottimizzazioni

L'utilizzo di costrutti che modificano lo scope lessicale a runtime (come `eval()` e `with`) ha un effetto devastante sulle performance del codice JavaScript. Tali meccanismi vanificano la maggior parte delle ottimizzazioni che l'engine JavaScript applica durante la fase di compilazione.

## 📉 Motivi della Degradazione

Gli engine JavaScript moderni (come V8) eseguono un'analisi statica del codice per determinare in anticipo dove risiedono le variabili e le funzioni, velocizzando la fase di esecuzione. 

Tuttavia, con l'uso di codice dinamico:

```javascript
// L'engine risulta incapace di ottimizzare questo codice
function foo(obj) {
  with (obj) {
    a = b; // Esiste 'a' in obj? O è globale? E 'b'?
  }
}

function bar(code) {
  eval(code); // Quali variabili o funzioni introduce questo codice?
}
```

In presenza di questi costrutti, l'engine deve assumere che lo scope possa essere stato invalidato, e pertanto:
- È costretto a disabilitare la ricerca statica (scope lookup statico), risolvendo le variabili esclusivamente a runtime.
- Non è in grado di utilizzare l'inline caching.
- È impedita l'applicazione della minification aggressiva (le variabili non possono essere ridenominate in modo sicuro se possono essere riferite dinamicamente).

## 🌊 Effetto a Cascata

L'impatto negativo non si limita unicamente alla funzione che contiene `eval()` o `with`. Se anche **una sola funzione** utilizza uno di questi meccanismi, l'**intero scope gerarchico superiore** cessa di essere ottimizzato.

```javascript
function padre() {
  var x = 10;

  function figlio() {
    eval("var y = 20;"); // ⚠️ Questa istruzione blocca l'ottimizzazione
  }

  // Nessuna ottimizzazione basata su scope è permessa nell'intera funzione padre
}
```

Il costo in termini di performance può rendere l'esecuzione del codice ordini di grandezza più lenta rispetto allo stesso codice privo di alterazioni dinamiche dello scope. Si consiglia vivamente di evitare tali costrutti in qualsiasi scenario produttivo.

## 📚 Risorse

- V8 Engine documentation sulle ottimizzazioni
- "You Don't Know JS" - Scope & Closures

## 📌 Tag

#javascript #scope #performance #optimization #eval #with #v8-engine #compiler