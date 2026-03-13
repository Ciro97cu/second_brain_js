# [[../../appunti-completi#errori|Errori di Scope]]

L'analisi degli errori di Scope nello sviluppo in JavaScript si concentra principalmente su due concetti complementari che dividono il comportamento in esecuzione rispetto alle restrizioni del motore e delle dichiarazioni:

- [[referenceerror-vs-typeerror]]: Come distinguere e risolvere i classici `ReferenceError` dalla gestione di un `TypeError`.
- [[strict-mode-scope-errors]]: Il comportamento di un errore di scope quando si opera in Strict Mode contro gli ambienti tradizionalmente permissivi.

Questi sub-argomenti trattano dal recupero di una variabile (RHS) all'inquinamento dello scope globale causato da un assegnamento (LHS).

## Collegamenti Relativi

- [[scope-chain]] - Meccanismo di ricerca delle variabili
- [[scope]] - Concetti base dello scope
- [[../variabili/variabili]] - Dichiarazione variabili (LHS)

## Risorse Esterne

- [MDN: ReferenceError](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ReferenceError)
- [MDN: TypeError](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypeError)
- [MDN: Strict Mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)
