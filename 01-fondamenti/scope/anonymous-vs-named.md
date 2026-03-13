# [[../../appunti-completi#funzioni-anonime-vs-funzioni-nominate|Funzioni Anonime vs Nominate]]

Le **espressioni di funzione** in JavaScript possono essere dichiarate senza un identificatore (**anonime**) o fornite di un nome esplicito (**nominate**). 

Sebbene la sintassi anonima sia diffusa per la sua concisione, l'approccio raccomandato consiste nel nominare sistematicamente le espressioni per facilitare il debugging, l'auto-riferimento e la leggibilità.

Le dichiarazioni di espressione possono omettere il nome, ma le dichiarazioni di funzione vere e proprie lo richiedono sempre per essere sintatticamente valide.

```javascript
// ❌ SINTASSI NON VALIDA: Dichiarazione privata di nome
// function() { console.log('Errore'); } // SyntaxError

// ✅ Dichiarazione di funzione (il nome è obbligatorio)
function dichiaraNome() {
  /* ... */
}

// ✅ Espressione di funzione anonima (sintassi valida ma approccio sconsigliato)
var espressioneAnonima = function () {
  /* ... */
};

// ✅ Espressione di funzione nominata (Best Practice)
var espressioneNominata = function nomeInterno() {
  /* ... */
};
```

## 📂 Sotto-argomenti

Per esplorare in dettaglio i pro e i contro di queste due metodologie di definizione, si faccia riferimento alle seguenti sezioni:

- [[anonymous-functions-drawbacks|Svantaggi delle Funzioni Anonime]]
- [[named-functions-benefits|Vantaggi delle Funzioni Nominate]]

## 🔗 Concetti Correlati

- [[function-as-scope|Funzioni come Scope]]
- [[iife-patterns|Pattern IIFE]]
- [[hiding-in-scope|Hiding in Scope]]
- [[../../appunti-completi#funzioni-anonime-vs-funzioni-nominate|Funzioni Anonime Completo]]

## 📚 Risorse

- "You Don't Know JS" - Scope & Closures
- MDN: Function Expressions

## 📌 Tag

#javascript #functions #anonymous #named-functions
