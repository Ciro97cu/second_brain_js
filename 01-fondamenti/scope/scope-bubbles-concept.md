# [[../../appunti-completi#le-bolle-di-scope-annidate|Bolle di Scope (Concetto)]]

Le **bolle di scope** rappresentano visivamente gli scope annidati in JavaScript: ogni blocco o funzione crea una particolare "bolla" che a sua volta risulta contenuta nella sua genitrice esterna, fino a giungere all'ambiente globale.

L'ambiente di scope complessivo può essere visualizzato come **bolle annidate** posizionate una all'interno dell'altra, senza sovrapposizioni parziali o intersecazioni. Al vertice di tutte vi è la grande bolla che incapsula e ospita tutte le restanti minori.

A livello concettuale, ogni funzione e blocco crea una nuova bolla locale. Queste bolle definiscono la struttura **lessicale**, fissata rigidamente alla stesura del codice sorgente.

La regola assoluta che dirige le bolle di scope è il contenimento totale: una bolla più piccola, corrispondente per esempio a uno scope in un blocco di codice contenuto in una certa funzione, deve trovarsi **interamente** nella bolla creata dalla funzione che le fa da contenitore, mai una frazione esterna o a cavallo di altre.

## 🔗 Collegamenti
- [[scope-bubbles]]
- [[lexical-scope-base]]
