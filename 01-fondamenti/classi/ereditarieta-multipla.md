# [[../../appunti-completi#78-ereditarieta-multipla-multiple-inheritance|Ereditarietà Multipla]]

## Il Desiderio di Comporre

Considerando l'allegoria classica del genitore e del figlio, si nota che biologicamente ogni discendente nasce da due genitori. Se il codice permettesse a una classe di ereditare da più classi contemporaneamente, il parallelismo genitore/figlio risulterebbe più calzante e consentirebbe un grande livello di composizione.
I linguaggi orientati agli oggetti che lo consentono applicano l'**ereditarietà multipla**, limitandosi a copiare le definizioni di tutti i genitori all'interno della singola classe figlia.

## Il Problema del Diamante

Un'enorme potenza compositiva, tuttavia, porta a complicanze non indifferenti. Se si eredita da genitori diversi che condividono metodi con lo stesso identico nome (es. `drive()`), si genera inevitabilmente l'ambiguità su quale versione la classe figlia debba adottare, forzando spesso specificazioni manuali che rompono l'eleganza del polimorfismo.

La complicazione peggiore si definisce come **Il Problema del Diamante**:

- Una classe `D` eredita dai genitori `B` e `C`.
- I genitori `B` e `C` ereditano, in partenza, da un comune "nonno" `A`.
- Si supponga che `A` introduca un metodo `drive()`. Successivamente, le classi `B` e `C` lo modificano e lo sovrascrivono internamente (polimorfismo) con comportamenti totalmente diversi.
- Al momento della creazione di `D` (che eredita da `B` e `C`), la classe quale versione di `drive()` dovrebbe scegliere?

![Problema del Diamante](../../../assets/diamond-problem.png)

> **Nota Visiva**: Il problema si definisce "del diamante" a causa della peculiare forma romboidale che lo schema gerarchico va a creare, con il nonno `A` in cima, i genitori `B` e `C` allargati al centro, e la classe figlia finale `D` riunita alla base.

## L'Approccio Drastico di JavaScript

Tutte queste dinamiche andrebbero a costare sforzi immani a livello progettuale e a livello di compilazione dei motori di sistema.
La soluzione di JavaScript a questa spinosa questione è perentoria: **il linguaggio vieta nativamente l'ereditarietà multipla**.

La maggior parte degli sviluppatori concorda che la purificazione e la semplificazione architetturale che ne deriva compensi ampiamente l'impossibilità di usare questo strumento. Ciò, inevitabilmente, non spegne il desiderio degli ingegneri che tentano ostinatamente di simularla ricorrendo ad astuzie e ai mixin.

## 🔗 Collegamenti

**Prerequisiti**:

- [[../../appunti-completi#71-teoria-delle-classi|Teoria delle Classi]]

**Approfondimenti**:

- [[mixin|Mixin ed Ereditarietà Parassita]]
