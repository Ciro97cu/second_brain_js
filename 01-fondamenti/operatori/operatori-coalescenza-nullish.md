# [[../../appunti-completi#5-operatori|Coalescenza Nullish]]

L'operatore di coalescenza nullish (`??`) è un operatore logico che restituisce il valore del suo operando destro quando l'operando sinistro è `null` o `undefined`, e altrimenti restituisce il valore dell'operando sinistro.

## Funzionamento

Questo operatore è stato introdotto per risolvere i problemi legati all'utilizzo dell'operatore logico OR (`||`) per l'assegnazione di valori di default.

```javascript
let risultato = valoreRicevuto ?? valoreDiDefault;
```

## Differenza tra || e ??

La distinzione fondamentale riguarda i valori considerati "falsy":

- L'operatore `||` scarta tutti i valori "falsy", inclusi `0`, `""` (stringa vuota) e `false`.
- L'operatore `??` scarta esclusivamente `null` e `undefined`.

Questa differenza risulta cruciale quando `0`, `""` o `false` rappresentano valori validi per la logica dell'applicazione.

```javascript
let contatore = 0;

// Utilizzando ||, il valore 0 viene sovrascritto poiché valutato falsy
console.log(contatore || 10); // 10

// Utilizzando ??, il valore 0 viene mantenuto in quanto valido
console.log(contatore ?? 10); // 0
```

## Casi d'Uso Pratici

La coalescenza nullish risulta particolarmente indicata per la configurazione di default all'interno di funzioni oppure oggetti.

```javascript
function configuraOpzioni(opzioni) {
  // Se timeout è stato impostato a 0, il valore viene rispettato
  let timeout = opzioni.timeout ?? 3000;
  let tentativi = opzioni.tentativi ?? 3;

  return { timeout, tentativi };
}

let config = configuraOpzioni({ timeout: 0 });
console.log(config.timeout); // 0
```

Se fosse stato utilizzato l'operatore `||`, l'assenza voluta di timeout (valore `0`) sarebbe stata erroneamente sostituita dal valore di default (`3000`).
