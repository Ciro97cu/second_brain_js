# [[../../appunti-completi#switch-basics|Switch - Concetti Base]]

Quando si ha la necessità di confrontare una singola espressione con una serie di valori specifici, l'istruzione `switch` offre un'alternativa più strutturata a una lunga catena di `if...else if`. 
La logica prevede la valutazione di un'espressione e l'esecuzione del blocco di codice corrispondente al valore testuale trovato.

## Sintassi Base

```javascript
switch (espressione) {
  case valore1:
    // codice eseguito se espressione === valore1
    break;
  case valore2:
    // codice eseguito se espressione === valore2
    break;
  default:
    // codice eseguito se nessun case corrisponde
}
```

La struttura si basa su:
- **`case`**: Un'etichetta che rappresenta un possibile valore per l'espressione valutabile.
- **`break`**: Un'istruzione che interrompe l'esecuzione vera e propria dello switch.
- **`default`**: Un caso opzionale eseguito in coda se nessun `case` utile corrisponde.

## Esempio Pratico

```javascript
let giorno = "Lunedì";

switch (giorno) {
  case "Lunedì":
    console.log("Inizio settimana");
    break;
  case "Mercoledì":
    console.log("Metà settimana");
    break;
  case "Venerdì":
    console.log("Quasi weekend!");
    break;
  default:
    console.log("Giorno normale");
}
```

## Quando usare switch o if...else

Si utilizza tipicamente `switch` quando:
- Si confronta una singola espressione con molti valori specifici e fissi.
- I confronti si basano strettamente sull'uguaglianza rigorosa (`===`).
- Si gestiscono 3 o più casi al fine prevalente di ottenere codice più leggibile.

Si utilizza al contrario `if...else` quando:
- Si verificano condizioni estese e complesse (come range, disuguaglianze logiche).
- Si impiegano operatori logici e relazionali multipli intrecciati.
- I casi da valutare sono numericamente modesti (solitamente fra 1 e 2 variazioni rilevanti).
