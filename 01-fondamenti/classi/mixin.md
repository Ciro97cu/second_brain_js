# Mixin ed Ereditarietà Parassita

Poiché in JavaScript gli oggetti non vengono copiati nativamente ma semplicemente "collegati", il linguaggio è privo del meccanismo che concretamente riversa il DNA di una classe genitore in un figlio.

Per scavalcare questa mancanza e simulare l'ereditarietà classica, negli anni gli sviluppatori hanno ampiamente fatto ricorso a pattern e funzioni di utilità che "mescolano" forzatamente due oggetti: i **Mixin**.

## Mixin Esplicito

La tecnica di base consiste nello scrivere una funzione che accetta un oggetto sorgente e un oggetto destinazione, per poi ciclare e ricopiare manualmente ogni proprietà e funzione dall'uno all'altro.

```javascript
/*
 * Esempio base di utility per il mixin.
 * Copia i valori da un oggetto all'altro
 * senza sovrascrivere quelli già esistenti.
 */
function mixin(sourceObj, targetObj) {
  for (var key in sourceObj) {
    if (!(key in targetObj)) {
      targetObj[key] = sourceObj[key];
    }
  }
  return targetObj;
}
```

Questa manipolazione permette di assemblare oggetti complessi, simulando la copiatura di una classe genitore nell'oggetto figlio.
Quando si ricopiano funzioni da un oggetto all'altro, in realtà il linguaggio si limita a sdoppiare il _riferimento_ alla funzione originale in memoria, senza duplicarne concretamente il codice.

## Pseudopolimorfismo Esplicito

Durante la composizione con i mixin, accade spesso che l'oggetto figlio e l'oggetto genitore abbiano una funzione con lo stesso nome (es. `drive()`). Se l'oggetto figlio vuole richiamare la versione originale del genitore all'interno della propria, si imbatte in un ostacolo: JavaScript (prima di ES6) non ha la parola chiave `super` per pescare automaticamente la versione precedente.

Non avendo questo "polimorfismo relativo", si è costretti a indicare a mano dove si trova il metodo originale e imporgli il contesto di esecuzione attuale:

```javascript
// Si forza manualmente la chiamata dell'oggetto Vehicle
// ma imponendo che venga applicata "qui" (this)
Vehicle.drive.call(this);
```

Questa pratica prende il nome di **pseudopolimorfismo esplicito**. Rende il codice poco flessibile, confuso e terribilmente rigido, poiché ogni volta che si cambiano i nomi o la gerarchia, è necessario ritoccare tutte le occorrenze in modo manuale. In generale, si consiglia vivamente di evitarlo.

## Ereditarietà Parassita

Un ulteriore approccio legato al concetto di "mescolare" oggetti è l'**Ereditarietà Parassita** (resa popolare da Douglas Crockford).

Piuttosto che affidarsi a una funzione di manipolazione esterna, la pratica parassita inscena una copia all'interno di una funzione "Costruttore".

1. Si crea internamente una normale istanza di un oggetto genitore.
2. La si modifica e la si personalizza, ad esempio aggiungendo proprietà.
3. Si salvano riferimenti intoccabili ai metodi originali che si desidera in seguito sovrascrivere.
4. Si rimpiazzano o sovrascrivono i metodi desiderati sull'oggetto.
5. Invece di lasciare che il costruttore generi un normale oggetto vuoto, si costringe la funzione a restituire il nostro oggetto appena "truccato".

Entrambe queste tecniche (mixin esplicito ed ereditarietà parassita) evidenziano fino a che punto gli sviluppatori siano costretti ad arrampicarsi sugli specchi pur di mascherare l'assenza nativa delle classi nel linguaggio.

## Mixin Impliciti

Un'ulteriore variante consiste nel _mixin implicito_. La base di questo approccio è il forzare momentaneamente una funzione appartenente a un altro oggetto, per farle eseguire le sue mansioni interne all'interno del proprio.

```javascript
/* Lines 123-456 omitted ... actually no */
var Something = {
  cool: function () {
    this.greeting = "Hello World";
  },
};

var Another = {
  cool: function () {
    // Mescolamento implicito forzando il costrutto this
    Something.cool.call(this);
  },
};
```

In questo caso, `Another` prende semplicemente in prestito per un istante il codice di calcolo di `Something`. Anche qui, si ripresentano i massimi problemi e i grandi avvisi derivati dallo _pseudopolimorfismo esplicito_: si tratta di un'invocazione testuale, fragile e impossibile da reindirizzare in modo automatico se un altro fattore esterno modifica il file, per la qual cosa se ne caldeggia l'eliminazione ed esclusione ove ce ne sia il modo o il tempo.

## Riepilogo Riflessivo

Come riepilogo per il paradigma "Classi in JavaScript" va ricordato questo incipit: le classi si basano intrinsecamente sull'azione della "Copia" materiale dei dati e del codice.
JavaScript non crea mai meccanicamente copie. Cercare allora di appiccicare una finta "copia in stile classe" a JavaScript — appoggiandosi ai Mixin o ai pesanti trick dell'Ereditarietà Parassita e dello stringente pseudopolimorfismo esplicito — genererà nella stragrande e assoluta maggioranza dei casi più problemi occulti e futuri fallimenti, le cosiddette _mine vaganti_, rispetto che applicare i corretti e fluidi schemi di costruzione nati o intrinseci dell'anima di JavaScript.
