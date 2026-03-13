# [[../../appunti-completi#blocchi-come-scope-blocks-as-scopes|let e const: Block Scope Moderno (Indice)]]

Questa sezione affronta in profondità l'implementazione del **Block Scope** in JavaScript (ES6+), esplorando l'evoluzione da `var` all'utilizzo moderno di `let` e `const`.
Di seguito i concetti esplorati in dettaglio:

- 📖 [[block-scope-concept|Concetto Base e Problemi con var]] - Il falso block scope con `var`, l'inizio del block scope con `try...catch` in ES3, e il principio del Minimo Privilegio.
- ✨ [[let-declaration|let: Block Scope Moderno]] - Come la parola chiave `let` confina le variabili ai blocchi, il divieto di ridichiarazione e lo shadowing tra scope diversi.
- 🔒 [[const-declaration|const: Block Scope Immutabile]] - Immutabilità della dichiarazione rispetto alla mutazione del valore referenziato e i blocchi limitati a una singola assegnazione.
- 🔄 [[block-scope-loops|let e const nei Cicli (Loops)]] - Il rebinding automatico di `let` per iterazione nei cicli, e la validità per ciclo limitata a iterator logic per il block scope `const`.
- ⚠️ [[tdz-temporal-dead-zone|Temporal Dead Zone (TDZ)]] - Cos'è la TDZ, la sua differenza rispetto all'hoisting esplicito in stile `var` e come garantisce precisione del refactoring logico prima del suo impiego assieme all'operatore condizionale `typeof`.
- 📦 [[explicit-blocks-best-practices|Blocchi Espliciti e Best Practices nel Block Scope]] - Formattare la base di codice per incapsulamento esplificito del valore e come impostare default logici per la dichiarazione del codice per mezzo della direttiva `const`.

## 📌 Tag

#javascript #scope #block-scope #let #const #var #es6 #tdz #hoisting #temporal-dead-zone #refactoring
