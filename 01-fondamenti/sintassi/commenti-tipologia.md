# [[../../appunti-completi#22-commenti-nel-codice-code-comments|Tipologie e Sintassi dei Commenti]]

In JavaScript, le annotazioni o commenti costituiscono porzioni di testo inserite direttamente nel codice e ignorate totalmente dal motore di esecuzione. Essi rendono le istruzioni e la logica leggibili per gli sviluppatori, semplificando la futura manutenzione dei file sorgente.

A livello sintattico, il linguaggio fornisce differenti strumenti per la stesura dei commenti, da impiegare in base alle necessità e all'estensione del blocco informativo.

## Commento su Riga Singola (//)

Qualsiasi sequenza di testo preceduta da un doppio slash (`//`) sino alla fine della specifica riga viene trattata dal motore JavaScript come un commento non eseguibile. Questo formato risulta ideale per appunti di natura sintetica.

```javascript
// Inizializzazione della variabile utente
let utente = "Mario"; // Risoluzione di fine riga
```

Risulta consentito l'uso di commenti su righe multiple accodando ulteriori annotazioni a singola riga per strutturare paragrafi testuali.

## Commento Multiriga (/* ... */)

Ogni gruppo testuale posizionato tra l'apertura `/*` e la rispettiva chiusura `*/` viene configurato come blocco continuo di commento prescindendo dalle interruzioni e a capo. 

```javascript
/*
 * L'algoritmo seguente è focalizzato 
 * sull'elaborazione batch dei documenti
 * archiviati localmente
 */
function elaboraArchivio_v2() {
  // Implementazione...
}
```

Questa tipologia si diffonde ampiamente per porzioni corpose di testo e l'esclusione di moduli interi di codice in fase di test. Risulta adatta per l'inserimento all'interno delle espressioni lunghe per etichettare i passaggi, ma deve prestare attenzione agli annidamenti non consentiti.

## Commenti di Documentazione (JSDoc)

I JSDoc rappresentano uno standard convenzionale impiegato come speciale commento multiriga aperto con doppio asterisco `/**` e chiusura `*/`. Essi formalizzano un sistema di descrizioni semantiche utili per strumenti automatizzati, editor moderni (con autocompletamento avanzato) e generatori esterni di documentazione.

```javascript
/**
 * Esegue la fatturazione dell'ordine utente basato sul sistema di prezzi integrato.
 *
 * @param {Object} ordine - Istanza del carrello cliente
 * @param {number} sconto - Valore percentuale dello sconto
 * @returns {number} Totale processato arrotondato a due decimali
 */
function calcolaEmissione(ordine, sconto) {
  // esecuzione del calcolo
}
```

Supportano tag predefiniti fondamentali quali `@param`, `@returns` o `@typedef` utili alla standardizzazione documentale di classi, logiche o tipologie di dati.
