# [[../../appunti-completi#Truthy Falsy Best Practices|Truthy Falsy: Best Practices]]

L'uso corretto e consapevole delle regole riguardanti i valori truthy e falsy permette di scrivere codice conciso. Tuttavia, applicarle indiscriminatamente può portare a bug difficili da diagnosticare, specialmente con alcuni domini di dati.

## Uso Consigliato per Controllare l'Esistenza

Sfruttare la valutazione truthy/falsy è utile e raccomandato per verificare la presenza di dati complessi, quali stringhe o istanze d'oggetto, abbattendo la verbosità del codice.

```javascript
/*
 * Pattern consigliato: Stringhe e Oggetti validi
 */
function processaUtente(nome, config) {
  // Conciso: copre false, null, undefined, ed espressioni vuote
  if (!nome) {
    nome = "Ospite";
  }

  if (config) {
    // Esegue logica sapendo che config esiste (non è falsy)
  }
}
```

## Attenzione a Zero e False

L'errore più comune relativo alla coercizione booleana occorre quando un valore `0` (numero originario) oppure un booleano `false` costituiscono stati **validi** a livello di business logic della determinata applicazione.

Un banale controllo falsy tramite negazione inibirà del tutto tali valori validi.

```javascript
/*
 * Pattern incorretto con numeri
 */
function calcolaSconto(percentuale) {
  if (!percentuale) {
    // BUG: intercetta null, ma previene anche la possibilità di uno sconto al 0%
    percentuale = 10;
  }
  return percentuale;
}

/*
 * Gestione corretta
 */
function calcolaScontoCorretto(percentuale) {
  // Controllo esplicito che preserva lo zero
  if (percentuale === undefined || percentuale === null) {
    percentuale = 10;
  }
  return percentuale;
}
```

Per il controllo delle variabili a cui possono essere assegnati `null` o `undefined`, dall'avvento di ES2020 l'operatore di **Nullish Coalescing (`??`)** costituisce la soluzione primaria, agendo unicamente sulle vere assenze di dato e trascurando le dinamiche standard truthy/falsy.

```javascript
// ?? preserva 0 e "" (falsy values), applicando default solo per null/undefined
let sconto = inputSconto ?? 10;
```

## Costringere Tipi in Uscita

Quando si redigono funzioni per restituire lo stato di una verifica (le cosiddette funzioni "_Predicate_"), va preferita l'emissione tassativa del tipo boolean. L'operatore logico negato impedisce ritorni ambigui per il consumatore.

```javascript
// Sconsigliato (restituisce numero stringhe, non boolean)
function isDisabled(elemento) {
  return elemento.className.indexOf("disabled");
}

// Raccomandato (restituisce strictly boolean via doppia negazione)
function isFocusable(elemento) {
  return !!elemento.getAttribute("tabindex");
}
```
