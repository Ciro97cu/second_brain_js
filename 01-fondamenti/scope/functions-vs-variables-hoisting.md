# [[../../appunti-completi#funzioni-vs-variabili-hoisting|Hoisting: Precedenza tra Funzioni e Variabili]]

## Precedenza delle Funzioni

In occasioni dove una funzione e una singola variabile collidono nell'astrazione dell'identificativo di pertinenza (nell'ambito di uno statement di dichiarazione esplicita simultanea), ne deriva stabilmente che la **funzione dichiarativa vanta la massima precedenza**.

```javascript
// Contenuto programmato
console.log(foo); // [Function: foo]

var foo = 2;

function foo() {
  console.log("Hello!");
}

console.log(foo); // 2

// Traduzione logica d'esecuzione
function foo() {
  // La Function declaration diviene sollevata a priorità massima PRIMA che d'altro
  console.log("Hello!");
}

var foo; // La dichiarazione associata sfocia in nullità e viene ignorata esplicitamente dal compilatore

console.log(foo); // Produce logicamente [Function: foo]
foo = 2; // Qualsiasi attribuzione di valore posteriore SOVRASCRIVE e domina referenzialmente la funzione stessa
console.log(foo); // 2
```

Si chiarisce che il compilatore antepone ciecamente la sintassi predefinita del blocco funzione esautorando l'impatto inizializzativo della semplice entità innalzabile "var", lasciando libero arbitrio alle fasi di susseguente riassegnazione imperativa all'interno del flusso base di codice in ordine riga.

## Ordine di Elaborazione Sintattica

Per quanto gravoso si possa presentare il conflitto identificativo, la classificazione interna al motore ES aderisce rigorosamente alla gerarchia operativa sequente:

1. **Function Declarations**: Sublimazione intera, corporea e in blocco dell'istruzione e logica del metodo al ramo portante del livello applicato. Registrata storicamente sempre da principio.
2. **Dichiarazioni Variabili**: Qualora s'imponga traccia pregressa sul record d'identificativi analogo a causa primariamente di precedenti referenziazioni alle funzioni medesime, esso incoraggia e comporta l'annullamento omologativo della presente espressione restrittiva.
3. **Assegnazioni Dirette**: Subordinano ed eseguono sistematiche sostituzioni dei puntatori formali originali assecondando la progressione alfabetico-sintattica rigo dopo rigo prescritta dall'operatore programmativo.

## Sovrascrittura su Identificativi Identici

Si ponga il caso sussistano all'attivo dichiarazioni interamente omonime concernenti il macro-segmento dell'identico dominio esecutivo.

Il principio dell'interpretabilità asserisce in via esclusiva che la collocata istruzione che sosta più in basso domina e rimpiazza senza equivoco possibile l'alter-ego disposta per prima, sovrascrivendola e celandola allo scrutinio per le routine operazionali future.

```javascript
function foo() {
  console.log("1");
}

function foo() {
  console.log("3");
}

// Analisi post-compilativa riepilogativa:
function foo() {
  console.log("3"); // Questo stadio finale azzera storicamente il richiamo preambolare su console "1"
}
```

Esula invece l'effettivo posizionamento della riassegnazione qualora lo statement in concorso risulti configurato unicamente per variare esecuzione su base puramente di natura valutativa nel costrutto "espressione espansa", limitandosi dunque allo scavalco in un ordine sequenziale postumo e differito.
