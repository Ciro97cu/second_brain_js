# [[../../../appunti-completi#311-lidentificatore-this|Implicit Binding: Event Handlers]]

Oltre alle perdite causate dal comportamento standard di JavaScript e del [[this-binding-default|Default Binding (Regola 1)]], un'altra complicanza frequente del binding implicito avviene nell'ambito del rendering e della manipolazione del DOM. Molte librerie e metodologie, non da meno il runtime nativo stesso, scelgono attivamente di sovrascrivere o forzare il valore espresso da `this`.

Questa manomissione viene definita in gergo **Hard binding non intenzionale**.

## Azioni Forzate nel DOM

Gli event listener associati ad elementi HTML spesso dirottano deliberatamente il contesto di una funzione fornita come risorsa o callback, ridirigendolo affinché corrisponda all'agente scatenante l'evento.

In questi ambiti, l'operazione avviene in maniera trasparente, sovrascrivendo l'implicit binding preventivato dello sviluppatore a favore di quello stabilito internamente dall'API di gestione degli eventi.

```javascript
const controller = {
  name: "Controller",
  handleClick: function () {
    console.log(this.name); // "Controller" o nome dell'elemento innesco?
  },
};

// Utilizzo del riferimento diretto al metodo dell'oggetto
const button = document.querySelector("#myButton");
button.addEventListener("click", controller.handleClick);

// Internamente, l'implementazione scavalca il costrutto nativo facendo simile a:
// button.handleClick.call(button, event); // Forzatura di THIS = button
```

In tale situazione, un tentativo di usufruire delle proprietà della variabile `controller` da via `this` genererà un esito deludente, risultando "indefinito" oppure restituendo le proprietà previste dal nodo HTML in questione, e sottraendo di netto il controllo dal programmatore.

La reazione in questi casi corrisponde invariabilmente a quella di una funzione "scollegata" e successivamente ri-forzata, dal momento in cui, come ogni passaggio per parametro (e destrutturazione), la libreria riceve nient'altro se non la reference spogliata dell'involucro `controller`.

## Risoluzione alle Forzature

A differenza dell'Implicitly Lost del solo operatore `this`, dove quest'ultimo scala su `window` (o globale puro in Strict Mode), l'intervento forzatamente manipolativo rimpiazza totalmente il puntatore assegnando a `this` oggetti che possono variare dall'elemento bersaglio, per librerie quali jQuery o API DOM Standard ([`addEventListener`](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)), o a volte alla Window stessa nei contesti meno maturi.

L'adozione di costrutti per bloccare il binding diviene d'obbligo. Strumenti come [[this-arrow-functions|Arrow Functions]] e `.bind()` si rivelano resistenti in particolar modo a tali pratiche, per non rischiare modificazioni del loro comportamento implicito o esplicito già confermato in fase compilatoria, stabilizzando il contesto e ignorando qualsivoglia "richiamo" mascherato sottostante.

```javascript
/* Utilizzo esplicito con .bind() per bypassare la designazione forzata */
button.addEventListener("click", controller.handleClick.bind(controller));
```

```javascript
/* Arrow Function wrapper che fa affidamento alla Lexical Scope Strategy */
button.addEventListener("click", (e) => controller.handleClick(e));
```

---

**Tags**: `#javascript` `#this` `#event-handlers` `#dom` `#implicit-lost`
