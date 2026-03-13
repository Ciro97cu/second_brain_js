# [[../../appunti-completi#311-lidentificatore-this|L'identificatore this: Indice e Riassunto]]

L'identificatore `this` in JavaScript è uno strumento speciale integrato nativamente nelle funzioni che offre il controllo sul contesto di operatività a runtime, svincolato dal concetto di ordine di scoping o annidamento procedurale fisso.

## La Natura di this

Il valore che popolerà la keyword corrisponde all'identità che ha dato il via all'esecuzione, e prenderà la direzioni dipendentemente da un esame della chiamata (_call-site_). Non incapsulerà alcun rinvio automatico verso la function che lo invoca e nemmeno alle classi superiori finché non lo si indirizzi secondo la corretta gerarchia di binding.

L'adozione dello strumento risiede nell'implementazione di pattern e architetture altamente orientati al superamento di parametri a stringa continua o esplicita in riga per gestire il flusso dei dati. L'obiettivo architettonico di interporlo, pur conservandone attivamente la comprensione delle regole, è scrivere API fluide, flessibili e compatte.

## Collegamenti e Architettura

I dettagli su funzionamento, interpretazione, regole di ingaggio ed errori noti sono presenti nei seguenti moduli dedicati:

- [[this-binding-intro]] - Spiegazioni fondative, natura, scopi e astrazioni dell'implementazione di `this`
- [[this-binding-rules]] - Analisi approfondita di Default, Implicit, Explicit e New binding con order di valutazione
- [[this-binding-problems]] - Difetti comuni di de-referenziazione: callbacks e arrow functions
- [[closure]] - Differenze architetturali con i binding lessicali e di environment
- [[../oggetti/oggetti]] - Comportamenti negli oggetti
