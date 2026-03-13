# [[../../appunti-completi#310-il-pattern-modulo-modules|Module Pattern Concept]]

Il Pattern Modulo (Module Pattern) è uno dei pattern di progettazione più significativi in JavaScript per sfruttare la potenza delle closure. Permette di incapsulare dati e comportamenti, fornendo uno scope privato e un'interfaccia pubblica.

## Requisiti Fondamentali

Affinché si possa parlare di vero Module Pattern, devono essere soddisfatti due requisiti essenziali:

1. **Funzione Invocata**: Deve esistere una funzione esterna che viene invocata almeno una volta. Ogni volta che questa funzione viene eseguita, crea una nuova istanza del modulo e un nuovo scope chiuso.
2. **Ritorno di Funzioni Interne**: La funzione esterna deve restituire almeno una funzione interna. Questo passaggio è cruciale perché permette alla funzione restituita di mantenere una closure sullo scope privato interno, garantendo l'accesso e la manipolazione dello stato interno anche dopo che la funzione esterna ha terminato la sua esecuzione.

## Oggetti vs Moduli

Un oggetto che possiede metodi ma nessuna closure su dati privati non è considerato un vero modulo in senso stretto all'interno di questo pattern. È semplicemente un oggetto con delle funzioni assegnate alle sue proprietà.

Inizialmente, una funzione che racchiude dati e altre funzioni senza restituirle non implementa una closure osservabile dall'esterno. I dati rimangono semplicemente isolati all'interno di quello scope. La trasformazione in modulo avviene quando alcune di queste funzionalità vengono esposte all'esterno mantenendo il collegamento con l'ambiente interno.
