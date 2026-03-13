# [[../../../appunti-completi#311-lidentificatore-this|Arrow Functions e this]]

Le arrow functions introdotte nello standard ES6 si differenziano profondamente dalle funzioni tradizionali per la gestione del binding di `this`. Non seguono le regole di assegnazione dinamica, ma adottano un approccio basato sul contesto lessicale.

Questa caratteristica risolve storiche criticità del linguaggio (come la perdita del contesto nei callback) ma introduce comportamenti specifici che è necessario comprendere in maniera puntuale per evitare errori architetturali o gotchas derivati.

## Argomenti

- **[[this-arrow-lexical-behavior|Comportamento Lessicale]]**: Come le arrow functions si legano al `this` esterno e i vantaggi rispetto al codice tradizionale (Closure binding).
- **[[this-arrow-pitfalls|Gotchas e Limitazioni]]**: Situazioni pratiche in cui le arrow functions non funzionano (metodi di oggetti letterali, costruttori e new operator, bind ignorati e function scope) e perché falliscono.
- **[[this-arrow-best-practices|Best Practices e Paradigmi]]**: Linee guida pratiche su dove usare o evitare le arrow functions e la scelta di architettura tra l'uso dello scoping lessicale `self=this` o il binding dinamico procedurale.

## Collegamenti Relazionati

- [[this-concept]] - Concetti fondamentali sul binding e le sue quattro regole.
- [[this-binding-precedence]] - Come le quattro regole prendono il controllo del binding.
- [[this-call-apply-bind]] - Metodi di chiamata esplicita che ignorano le arrow function.
- [[../es6/arrow-functions]] - Altri dettagli e caratteristiche su sintassi delle arrow functions in ES6.
- [[../avanzate/lexical-scope]] - Scope lessicale interno per Closure e Context.
