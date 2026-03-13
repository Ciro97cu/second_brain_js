# [[../../appunti-completi#Valori Truthy e Falsy|Valori Truthy e Falsy in JavaScript]]

Il concetto di valorizzazione truthy e falsy in JavaScript regola in che modo i valori non booleani vengono interpretati in tutti i contesti che si aspettano l'uso della logica condizionale.

La **coercizione booleana** è una tecnica integrante del linguaggio, in grado di convertire, implicitamente ed esplicitamente, praticamente ogni istanza d'oggetto in un puro `true` o `false`.

Si ramificano svariate logiche di valutazione e specifici impieghi di queste dinamiche.

Per esplorarne appieno il funzionamento, i valori sono ripartiti nei seguenti argomenti specifici:

- **[[boolean-coercion-rules|Coercizione Booleana Implicita]]**: modalità e contesti applicativi in cui l'engine trasforma i valori in logica booleana.
- **[[falsy-values-list|Lista dei Valori Falsy]]**: tutti e soli i 7 valori specifici che generano `false`.
- **[[truthy-values-list|Lista dei Valori Truthy]]**: cosa compone il resto del linguaggio e valutazioni che restano truthy (come array vuoti).
- **[[explicit-boolean-coercion|Coercizione Booleana Esplicita]]**: mezzi per convertire forzatamente e dichiarativamente un elemento in `boolean`.
- **[[truthy-falsy-best-practices|Best Practices e Fallacie]]**: impieghi suggeriti, utilizzo sicuro evitando coercizioni non desiderate come sullo `0`.
