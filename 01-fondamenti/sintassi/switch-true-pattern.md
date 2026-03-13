# [[../../appunti-completi#switch-true-pattern|Switch - Il Pattern True]]

Il pattern logico descritto dalla sintassi `switch (true)` identifica a tutti gli effetti una preziosissima tecnica applicativa d'alto rango funzionale. L'espressione che si richiede di validare risulta configurata deliberatamente sotto il rigido valore booleano assoluto e incondizionato, per l'appunto `true`. Questa singolare impostazione rovescia le aspettative elementari: avvalora adesso dinamiche espressioni algebriche o elaborazioni relazionali estese allocate individualmente nell'alveo d'appartenenza dei disgiunti `case`.

## Emulare la Concatenazione if...else

Allorché uno Switch basilare constata la preesistenza o meno unicamente fondata sulle uguaglianze precise, insorgendo necessità di un paragone di maggiorazione o minorazione si è vincolati solitamente ad usufruire d'una folta ramificazione con la direttiva nativa `if`. Il pattern discusso in queste istanze ne mitiga agevolmente il dispendio:

```javascript
let punteggio = 85;

switch (true) {
  case punteggio >= 90:
    console.log("Voto eccellente");
    break;
  case punteggio >= 80:
    console.log("Voto molto buono"); // Sarà l'elaborazione eseguita in rilievo
    break;
  case punteggio >= 60:
    console.log("Voto appena sufficiente");
    break;
  default:
    console.log("L'esito preannuncia un'insufficienza");
}
```

## Criterio di Tolleranza nell'Esecuzione

Quando si instanzia tale modalità, il lettore di compilazione valuterà per ciascun tag etichetta se e quando riscontrare l'esito come `true`. Va tenuta altamente in considerazione però che il fondamento di risoluzione s'incardina sulla parificazione rigorosa d'uguaglianza strettissima `===`. Non è quindi ammesso il supporto in via autonoma dei valori truthy.

```javascript
let nome = "Mario";

switch (true) {
  case nome:
    // "nome" è considerato "truthy", eppure fallisce perché non risulta rigorosamente === true in senso letterale e compiuto.
    console.log("Accertamento del nome"); // Evitato
    break;
  case !!nome:
    // Una doppia negazione ne induce formalmente e inequivocabilmente l'essenza sotto Boolean
    console.log(
      "Superamento del controllo innescato con l'inquadratura booleana",
    ); // Attivato tempestivamente
    break;
}
```

L'impegno assiduo di codesta strategia apporta indubbi e ragguardevoli sgravi sulle procedure interpretative d'un programma affossato dai grovigli d'un innaturato eccesso sistematico di blocchi algoritmici.
