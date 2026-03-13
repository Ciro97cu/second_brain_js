# [[../../appunti-completi#scope-lessicale-lexical-scope|Scope Lessicale (Lexical Scope) - Sommario]]

Lo **scope lessicale** (o *static scope*) è il meccanismo mediante il quale JavaScript determina l'accesso alle variabili attraverso lo spazio e i blocchi del codice sorgente. Tale processo avviene durante la fase di lexing, conferendo alle variabili risoluzione in maniera puramente statica.

Il presente file indice raccoglie i diversi argomenti sul tema:

## Processo Autoriale e Dinamico
1. [[lexical-vs-dynamic-scope]] - Analisi e confronto del comportamento statico introdotto dal JavaScript rispetto a linguaggi eseguiti con pattern chiamati in maniera dinamica.
2. [[lexical-scope-author-time]] - Regole su come lo scope e l'astrazione si definiscano in base a dove il codice viene materialmente scritto, a prescindere da dove esso verrebbe invocato. 

## 🔗 Ulteriori Approfondimenti
- [[scope-bubbles]] - Esposizione formale dei confini spaziotemporali dello scope tra blocchi e funzioni.
- [[scope-chain]] - Processo di concatenazione lessicabile tra diversi strati dello scope e relativi look-up per il recupero delle variabili.
- [[nested-scope]] - Meccanica dell'integrazione di scope subordinati all'interno di processi e funzioni più grandi attraverso il nesting.
- [MDN: Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) - Documentazione ufficiale e definizione.
- [YDKJS: Scope](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch1.md) - Riferimento normativo del comportamento dello scope e sue chiusure lessicali.
