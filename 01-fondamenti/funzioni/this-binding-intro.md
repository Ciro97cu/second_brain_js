# [[../../appunti-completi#311-lidentificatore-this|L'identificatore this: Introduzione]]

Il meccanismo controllato dalla keyword `this` rappresenta una delle funzionalità più caratteristiche e spesso fraintese del linguaggio JavaScript. Non si riferisce al contesto in cui una funzione è stata definita, ma a un binding dinamico stabilito in fase di chiamata.

## Concetti Fondamentali

La natura di `this` sfida spesso le intuizioni di sviluppatori abituati ad altri paradigmi orientati agli oggetti. Le regole sono specifiche del motore di esecuzione:

- **Call-site determina il this**: Il riferimento all'oggetto per `this` dipende esclusivamente da come la funzione viene invocata nell'espressione (call-site).
- **Binding dinamico**: Il momento in cui il codice assegnerà un valore a `this` avviene al volo, a runtime, non in scrittura, differenziando dal concetto di ambito lessicale (lexical scope).
- **Equivoco comune**: C'è l'idea diffusa che `this` faccia indirettamente riferimento alla medesima istanza della funzione. Non è corretto; esso non incapsula e non si riferisce in alcun caso alla medesima *Function Object*.

## Perché Utilizzare il meccanismo this?

Esso fornisce in JavaScript un'astrazione fondamentale per il passaggio di riferimenti, garantendo logiche riutilizzabili contro oggetti diversi senza richiedere l'uso esplicito dell'identificatore o dell'argomento oggetto a ogni singola chiamata di funzione.

```javascript
/* Utilizzo di un approccio implicito con 'this' */
function identify() {
  return this.name.toUpperCase();
}

function speak() {
  var greeting = "Hello, I'm " + identify.call(this);
  console.log(greeting);
}

var me = { name: "Kyle" };
var you = { name: "Reader" };

// L'esecuzione di speak adatta automaticamente "this" al nuovo "owner"
speak.call(me); // Hello, I'm KYLE
speak.call(you); // Hello, I'm READER
```

All'opposto, rinunciando alla gestione di binding automatico che accompagna `this`, la medesima struttura logica causerebbe maggiore proliferazione di parametri passati, forzando un sistema ad alto accoppiamento verso l'input:

```javascript
/* Implementazione verbosa passando stringhe e object (senza this) */
function identifyContext(context) {
  return context.name.toUpperCase();
}

function speakContext(context) {
  var greeting = "Hello, I'm " + identifyContext(context);
  console.log(greeting);
}

// Bisogna far fluire l'intero riferimento attraverso multiple pipeline 
speakContext(me); // Hello, I'm KYLE
```

Più l'architettura cresce, accoppiando metodi diversi, o pattern come il delegato, gestire internamente tali parametri appesantisce il software e aumenta inesorabilmente gli errori di astrazione.

## Il Call-Site Binding

Rintracciare il valore effettivo assegnato a `this` significa analizzare univocamente il punto in cui avviene l'effettiva istruzione a runtime. Il motore JS delega la valutazione esaminando lo strato sintattico o la catena che evoca la funzionalità.

Le dinamiche complete di interpretazione sono classificate sotto una rigorosa gerarchia, suddivisa nelle Quattro Regole del Binding esplorate in [[this-binding-rules]].

## Collegamenti

- [[this-binding-rules]] - Le regole e gerarchia di valutazione per this
- [[this-binding-problems]] - Casistiche anomale e problemi in this
- [[funzioni]] - Contesto di esecuzione delle funzioni
- [[closure]] - Paradigmi di privatezza rispetto al this
- [[this]] - L'indice per orientare l'applicazione della keyword
