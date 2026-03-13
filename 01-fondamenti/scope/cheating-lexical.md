# [[../../appunti-completi#barare-con-lo-scope-lessicale-cheating-lexical|Barare con lo Scope Lessicale (Indice)]]

## 🎯 Concetto

Lo scope lessicale di norma è **immutabile** ed è strettamente determinato al momento della scrittura del codice (**author-time**). JavaScript, per ragioni storiche, possiede meccanismi per "barare" e modificare questo scope dinamicamente in fase di esecuzione (**runtime**).

Queste pratiche sono oggi **fortemente sconsigliate** o vietate per problemi legati sia alla sicurezza che all'efficienza del codice, in quanto violano la prevedibilità e l'ottimizzazione statica dell'engine.

## 📑 Sotto-argomenti

Le modifiche a runtime dello scope e le relative conseguenze presentano i seguenti focus:

1. **[[eval-lexical|L'utilizzo di eval()]]**: Dettagli su come e perché la valutazione del codice da stringhe compromette l'integrità del programma.
2. **[[with-lexical|Il costrutto with]]**: Problematiche legate all'espansione temporanea dello scope su oggetti e la generazione di variabili globali accidentali.
3. **[[cheating-lexical-performance|Impatto sulle Performance]]**: L'interruzione inesorabile delle ottimizzazioni dell'engine e il conseguente rallentamento dell'esecuzione del codice.
4. **[[cheating-lexical-alternatives|Alternative Moderne]]**: Pattern robusti e performanti (come destructuring e bracket notation) per rimpiazzare l'uso di tali costrutti dinamici.

Si ricorda che l'implementazione dello strict mode rende inapplicabili alcuni di questi meccanismi, confermando la direzione volta ad allontanare queste prassi obsolete nello sviluppo JavaScript moderno.

## 📌 Tag

#javascript #scope #lexical-scope #eval #with #performance #strict-mode #index
