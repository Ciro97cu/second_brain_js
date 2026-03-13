# [[../../appunti-completi#35-boxing-e-metodi-dei-primitivi|Boxing, Wrapper Objects e Metodi]]

In JavaScript, i tipi primitivi (`string`, `number`, `boolean`) non sono oggetti, ma dispongono di metodi built-in grazie al concetto del "boxing" implicito o dell'impiego dei relativi wrapper object esposti nativamente dall'ambiente d'esecuzione.

Gli appunti precedenti sono stati separati per trattare sistematicamente la logica dei primitivi, delle variabili wrapper e le varie conversioni esplicite dei tipi primitivi base in un formato più agevole ed ordinato.

## Sotto-argomenti

- **[[boxing-concept]]**: Come e perché JavaScript permette di utilizzare proprietà e metodi tipici dei prototipi ad istanza su semplici valori letterali, applicando implicitamente l'astrazione del boxing sul tipo di dato temporaneo fornito in analisi.
- **[[native-wrappers-vs-primitives]]**: La forma letterale di valutazione rispetto alla forma costruita. Per quali motivi la creazione esplicita dei cosiddetti _built-in wrappers_ viene raccomandata contro la comune forma primitiva.
- **[[object-wrappers-caveats]]**: I rischi nascosti per l'uguaglianza stretta logica introdotta dagli sviluppatori e la peculiarità legata alla veridicità dei medesimi che compongono false flag nella valutazione coercitiva booleana.
- **[[explicit-type-conversion]]**: Una catalogazione degli strumenti preposti a guidare esplicitamente un tipo verso il formalismo alternativo desiderato (e.g. da `string` a `number` e viceversa) tramite parsing dedicato, costruttori o espressioni globali.

## Collegamenti

- [[valori-tipi]] - Tipi primitivi e riferimenti
- [[typeof]] - Rilevare tipi di esecuzione rispetto le loro allocazioni interne
- [[coercizione]] - I domini dei dati impliciti e misti
