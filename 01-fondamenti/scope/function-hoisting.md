# [[../../appunti-completi#function-hoisting|Indice dell'Hoisting delle Funzioni]]

Questo documento serve da punto di accesso alla disamina del comportamento dell'hoisting associato temporalmente alle funzioni in JavaScript.

L'hoisting delle funzioni presenta dinamiche precise e in parte singolari, che divergono sensibilmente da quelle atte a governare le ordinarie variabili. L'impatto sul posizionamento semantico del codice determina importanti scelte architetturali in fase di sviluppo.

## Moduli di Approfondimento

Gli argomenti legati all'elevazione delle dichiarazioni sono stati estrapolati in file autonomi, affrontando progressivamente singole sfaccettature dell'ordine di risoluzione:

1. **[[function-hoisting-concept|Concetto Base di Hoisting delle Funzioni]]**
   Tratta la differenza critica tra dichiarazioni di funzione e funzioni espressioni. Spiega il meccanismo esecutivo sottostante che il motore JavaScript avvia preventivamente in pre-compilazione.

2. **[[functions-vs-variables-hoisting|Regole di Precedenza: Funzioni contro Variabili]]**
   Illustra il modello logico attuato dal gestore JavaScript in occasioni di conflitti tra definizioni di funzione e istruzioni di dichiarazione per mere variabili, con speciale riferimento alla sovrascrittura d'identificatori duplicati.

3. **[[block-scoped-functions|Comportamento nei Blocchi e Strict Mode]]**
   Evidenzia i difetti storici e il forte grado di imprevedibilità che accomunano le funzioni radicate e dichiarate in blocchi (cicli if, while), focalizzando le discrepanze cronologiche tra legacy e implementazioni con blocco ristretto.

4. **[[function-hoisting-gotchas|Casi Limite, Eccezioni e Pratiche Suggerite]]**
   Pone a confronto pratico le varie disposizioni sintattiche, discutendo la natura derivata di `TypeError` e dei corrispondenti `ReferenceError` legati alla restrizione TDZ. Illustra i consigli da perseguire preventivamente durante la progettazione.

## Concetti Trasversali

Altre tematiche che fungono da complemento indispensabile nella formazione logica della dichiarazione lessicale all'interno dei motori JavaScript si associano regolarmente allo schema operativo delle classiche variabili:

- Rivedere integralmente il comportamento e gli standard applicati per dichiarazioni non afferenti strettamente alle funzioni, approfondendo variabili dichiarate tramite identificativo.
- Lo studio generale sui confini lessicali, sulle bolle operative e sull'incapsulamento protetto da definizioni ES6 in avanti (let e costanti limitate nel block scope).
