# [[../../appunti-completi#il-sistema-di-tipi-in-javascript|Sistema dei Tipi JavaScript: Tipi e Sottotipi]]

Il sistema dei tipi di JavaScript è formato da **6 tipi primitivi** (immutabili, assegnati per valore) e da **1 tipo complesso** principale (`object`).

Tale design architetturale presenta alcuni falsi miti diffusi, oltre ad alcune variazioni storiche (legate al comportamento contro-intuitivo dell'operatore `typeof`) ormai integrate a livello strutturale per garantire la retrocompatibilità del linguaggio.

Di seguito si trovano i concetti fondanti sulle caratteristiche interne del tipo oggetto e alle implementazioni con le primitive, separati in argomenti atomici:

## Indice dei Concetti

- [[mito-tutto-oggetto]] - Perché i valori primitivi non costituiscono oggetti e le implicazioni legate al boxing automatico.
- [[sottotipi-built-in]] - Le particolarità esclusive delle funzioni (in quanto Callable Objects) e degli array (Structured Objects), oltre agli altri sottotipi (Date, Error, ecc.).
- [[scelta-strutture-dati]] - Quando impiegare gli appropriati sottotipi per strutturare i dati e i criteri su come effettuare type-checking in sicurezza.
- [[passaggio-valore-vs-riferimento]] - I principi operativi di mutabilità, allocazione mnemonica in fase di inizializzazione e i differenti passaggi come argomenti in procedure locali.

## Risorse Correlate e Approfondimenti
- [[typeof]] - Panoramica integrale sull'operatore di verifica sintattica del tipo.
- [[boxing]] - Analisi della reazione in background del motore JS davanti ad accessi ad una proprietà situata su tipi primitivi.
- [[valori-tipi]] - Classificazione sommaria estesa di tutti i valori identificabili nel linguaggio di programmazione.