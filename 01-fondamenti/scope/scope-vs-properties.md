# [[../../appunti-completi#scope-lessicale-vs-accesso-a-proprietà|Scope vs Proprietà Oggetti]]

La ricerca dello scope lessicale e l'accesso alle proprietà di un oggetto operano su catene e logiche differenti, portando a tipi di esecuzioni ed errori distinti. Il corretto disambiguo di questi concetti aiuta il debugging delle applicazioni e garantisce l'adozione delle corrette best practices come l'uso dell'optional chaining.

I concetti chiave dell'argomento sono suddivisi nei seguenti appunti:

- [[scope-properties-lookup-differences]] - Regole base su come JavaScript risolve il primo identificatore (tramite scope) e il resto della catena (tramite proprietà) e differenza negli errori generati.
- [[scope-chain-vs-prototype-chain]] - Analisi parallela su come lo Scope Chain sia disaccoppiato dal Prototype Chain e come operano in sinergia per restituire i valori alle istruzioni esegutive.
