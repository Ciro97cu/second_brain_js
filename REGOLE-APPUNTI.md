# Regole per la Scrittura degli Appunti Completi

Gli appunti devono essere scritti in italiano chiaro, con l’obiettivo di spiegare ogni concetto in modo semplice, pratico e completo, senza lasciare fuori dettagli tecnici importanti. La priorità è la comprensibilità, ma senza mai banalizzare o tagliare parti fondamentali.

**Workflow:**  
Prima si scrivono gli appunti in `appunti-completi.md`, solo dopo la revisione si creano le note atomiche.

**Stile:**  
Tutto deve essere scritto in terza persona. Non si usano mai “noi”, “tu”, “voi” o “puoi”. Se il testo inglese usa la seconda persona, va sempre trasformato in forma impersonale (“si può”, “è possibile”, “si deve”, “si consideri”).

**Forma:**  
Si preferiscono paragrafi discorsivi e spiegazioni continue. Gli elenchi puntati si usano solo quando servono davvero per chiarezza tecnica (ad esempio per distinguere casi, opzioni, regole o comportamenti diversi). In tutti gli altri casi, meglio una narrazione fluida e lineare.

**Linguaggio:**  
Il linguaggio deve essere il più semplice e diretto possibile, come se si spiegasse a voce a un collega. Si evitano parole difficili, accademiche o inutilmente ricercate, a meno che non siano indispensabili per la precisione tecnica. Se un termine tecnico inglese è lo standard nell’ecosistema JavaScript (come “scope”, “closure”, “callback”, “engine”, ecc.), si lascia in inglese.

**Sintesi:**  
L’obiettivo è sempre quello di rielaborare e sintetizzare il testo originale, senza traduzioni letterali e senza prolissità. Si deve arrivare al nocciolo del concetto, spiegandolo in modo efficace e pratico. Se un concetto è già molto breve e chiaro, si può tradurre direttamente, ma questa deve restare un’eccezione.

**Esempi e codice:**  
Gli esempi di codice sono forniti dall’utente, ma vanno sempre inclusi quando aiutano a chiarire la teoria. Se necessario, si possono ampliare per maggiore chiarezza, ma in genere non dovrebbe servire. I commenti nei codici vanno scritti con commenti multilinea (`/* ... */`) per spiegazioni estese.

**Posizionamento e struttura:**  
Gli appunti vanno inseriti nella sezione giusta, rispettando la struttura e la numerazione del file `appunti-completi.md`. È importante mantenere la coerenza con i capitoli e le sottosezioni già presenti.

**Evitare duplicazioni:**  
Se un concetto è già stato spiegato altrove, non va riscritto. Si inserisce invece un breve rimando con link alla sezione appropriata. Il link va inserito con la sintassi Markdown `[testo descrittivo](#anchor-della-sezione)`, preceduto da una breve frase di contesto, ad esempio:

> **Nota**: Per i dettagli su [concetto], si veda [la sezione dedicata](#nome-sezione).

oppure:

> **Approfondimento**: Il meccanismo di [concetto] è spiegato in dettaglio in [sezione X.Y](#nome-sezione).

**Eccezione alla sintesi:**  
Se un concetto è già brevissimo e un’ulteriore sintesi rischierebbe di renderlo meno chiaro, è consentito riportare una traduzione diretta, purché sia sempre in terza persona. Questa deve restare una vera eccezione e non la regola.
