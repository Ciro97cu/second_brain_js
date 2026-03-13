# [[../../appunti-completi#switch-fallthrough|Switch - Break e Fall Through]]

L'istanza operativa di `break` svolge l'attività essenziale nella struttura del blocco di codice per arginare quel fenomeno computazionale noto ampiamente come **fall through** (che in gergo viene tradotto in _caduta al di sotto_, in cascata continua), un difetto procedurale capace di estendere la visibilità fino all'esecuzione non intenzionale delle espressioni interne previste per i flussi di casi situati consecutivamente più a valle, indipendentemente dal rispetto effettivo del match testuale e semantico.

## Fall Through Accidentale

Nel sopraggiungimento fatale di totale amnesia circa l'apposizione del termine `break`, l'elaborazione continua ed inciampa irrimediabilmente nei passaggi preordinati susseguenti.

```javascript
let numero = 1;

switch (numero) {
  case 1:
    console.log("Uno");
  // Attenzione: manca break. L'esecuzione non si conclude.
  case 2:
    console.log("Due");
  case 3:
    console.log("Tre");
    break;
}
// Generazione Output consequenziale d'errore: "Uno", "Due", "Tre"
```

## Raggruppare i Case Intenzionalmente

Questa insidiosa dinamica di _fall through_, allorquando accuratamente concepita e incanalata al servizio corretto, offre un formidabile stratagemma sintattico. Consente il provvidenziale raggruppamento unitario di multipli `case` accumunati da precisi criteri funzionali e diretti verso il compimento del medesimo iter d'uscita. Omettendo intenzionalmente un `break` inneschiamo una concatenazione.

```javascript
let mese = "Gennaio";

switch (mese) {
  case "Dicembre":
  case "Gennaio":
  case "Febbraio":
    console.log("Inverno");
    break;
  case "Marzo":
  case "Aprile":
  case "Maggio":
    console.log("Primavera");
    break;
  default:
    console.log("Mese non riconosciuto");
}
```

L'esecuzione del motore perlustra in cerca del primo innesco testuale ed inizia lo scivolamento verso le azioni da portare a compimento, fermandosi esclusivamente in sede d'intervento dell'istruzione di rottura `break`. Si rimarca sovente una buona prassi quella di allegare un adeguato commento esplicativo allo scopo in modo che la potenziale lacuna originaria non venga accidentalmente colmata.
