# Proprietà vs Metodi (Property Versus Method)

In molti linguaggi di programmazione Object-Oriented (come Java o C++), una funzione legata strettamente a un oggetto o a una classe gode di uno status semantico speciale ed è chiamata un **"metodo"**.

Tuttavia, in JavaScript le dinamiche dell'architettura si differenziano. Nonostante gli sviluppatori di frequente impieghino il termine "method access" quando accedono a funzioni presenti su di un oggetto — incoraggiati anche dalle specifiche JS che talvolta accennano al sostantivo — **tecnicamente e strutturalmente le funzioni non "appartengono" in forma esclusiva agli oggetti.**

## Concetti Chiave

- **Le funzioni non appartengono agli oggetti**: Gli oggetti dispongono solamente di _riferimenti_ (references) che puntano a dei valori funzione.
- **Intercambiabilità semantica**: Le diciture "funzione" e "metodo" in lingua JavaScript possono essere intese per lo più come interscambiabili.
- **Tutto è un 'Property Access'**: Dal punto di vista del motore, chiedere una funzione a un oggetto è esattamente la stessa procedura che si invoca per prendere una banale stringa associata in memoria: un **Property Access**.
- **Indipendenza dei Riferimenti**: Due variabili, incluse le chiavi di oggetto che in quel momento contengono una funzione, non attribuiscono particolarità intrinseca: sono semplici indicatori al valore.

## Solamente Multipli Riferimenti

Quando un valore di tipo oggetto espone una funzione, noi stiamo seguendo la rotta tramite uno dei suoi puntatori. Che la si estragga e posizioni altrove, non va a stravolgerne l'origine non proprietaria. Di seguito l'enunciato pratico:

```javascript
/*
 * Creazione di una normale funzione
 */
function foo() {
  console.log("esecuzione logica!");
}

/*
 * Due variabili diverse ottengono
 * l'identico e paritario puntamento alla funzione
 */
var someFoo = foo;

var myObject = {
  someFoo: foo,
};

/*
 * La riprova risiede nel fatto che producono lo stesso return
 */
foo; // restituisce la funzione "function foo(){..}"
someFoo; // restituisce la funzione "function foo(){..}"
myObject.someFoo; // restituisce la funzione "function foo(){..}"
```

Nello scenario sopra tracciato, `someFoo` e `myObject.someFoo` non sono due tipologie distinte di costrutti, ma soltanto **riferimenti separati in cerca della stessa identica fonte**. Non c'è alcun magico "trasferimento di proprietà" tra l'oggetto e la funzione. Nessuno chiamerebbe assennatamente `someFoo` un "metodo". Lo stesso razionale, sul piano rigoroso, può e deve reggere per `myObject.someFoo`.

## Il Caso Frequente: La Parola Chiave this

Una tipica obiezione sollevata osserva che, se una referenza come quella soprastante possiede un riferimento di tipo `this` al suo interno, per via della regola basilare nota come [Implicit Binding](../funzioni/this/this-binding-implicit.md), la chiamata `myObject.someFoo()` farebbe puntare tale `this` proprio a `myObject`.

Sicuramente in quel preciso istante d'esecuzione il contesto viene assorbito — ma è soltanto un artefatto del _call-site_ (il luogo in cui e il modo in cui essa viene azionata dal codice in tempo d'esecuzione), un attributo che viene accollato in maniera puramente **dinamica a runtime**, non un legame formale a design-time o definition-time della logica stessa.

L'associazione tra funzione e la sua "sede ospitante" per via del `this` rimane sempre di natura prettamente _indiretta_.

## Object-Literal e Funzioni Inline

Anche definendo sùbito e organicamente una funzione come espressione nel corpo del letterale (object-literal), l'appartenenza non si concretizza sotto alcuna metrica maggiore:

```javascript
var container = {
  /*
   * Espressione di funzione inline nel blocco
   */
  printer: function () {
    console.log("print interno");
  },
};

/*
 * Estrapolando in una comune variabile,
 * continuiamo ad avere in mano il reference originario
 */
var extractedPrinter = container.printer;

extractedPrinter; // restituisce la funzione
container.printer; // restituisce la stessa funzione
```

Ancora uno scollamento tra oggetto "contenitore" e valore tenuto. Restano meri appigli plurimi per lo stesso oggetto radice `[Function]`.

## Una Nuance Sottile: La Keyword `super` (ES6)

A tutta questa diffusa uniformità "funzione = metodo" si accompagna una precisazione peculiare giunta più tardi nello sviluppo di JS.
Un'eventuale scisma d'intenti e identità subentra assieme all'aggiunta della sintassi in favore delle `class` da ES6, ed affonda con l'introduzione della parola chiave contestuale sussidiaria: **`super`**.

Diversamente al meccanismo di tardìa determinazione (late binding) che domina il comportamento di `this`, l'interazione che le definizioni intavolano col parametro `super` avviene in modalità staticamente associata al compimento dell'inizializzazione del layer-schema. In tale ottica assumerlo come un indicatore e definirla più simile alle vesti classiche d'un "metodo" saldamente correlato e legato allo scoglio di appartenenza ottiene invero un inquadramento logico più appropriato. Detto ciò, le casistiche continuano prevalentemente a rappresentare dettagli minimi tra corpose somiglianze terminologiche.

## Punti Chiave

1. **Non sono specializzati**: La "proprietà" contenente una funzione non adotta poteri strutturali aggiuntivi ed essa è in tutto e per tutto un normale richiamo (property access).
2. **Vocaboli sinonimi**: Considerare l'adozione tra "funzione" e "metodo" quale opzione puramente discrezionale dipendente dal contesto di conversazione.
3. È un collegamento debole e reversibile. Passare una referenza d’una funzione estratta è norma radicata e dimostra assenza di rigidità.

## Collegamenti

- [[../funzioni/this|Il rintracciamento dell'ancora dinamica "this"]] - Dinamiche relative al this e call-site
- [[property-access]] - Regole sull'accesso a un oggetto
- [[object-literal-vs-constructed]] - Praticità sulle dichiarazioni immediate
- [[../funzioni/funzioni]] - Come le funzioni si comportano nel loro essere un subtype base di tipo oggettificato

#oggetti #funzioni #metodi #this-binding #super-binding #sintassi
