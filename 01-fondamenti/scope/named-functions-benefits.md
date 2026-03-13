# [[../../appunti-completi#funzioni-anonime-vs-funzioni-nominate|Vantaggi delle Funzioni Nominate]]

## 🎯 Il Valore delle Espressioni Nominate

Nominare sempre le espressioni di funzione è considerata una _best practice_ fondamentale nell'ecosistema JavaScript. Fornire un identificatore interno risolve strutturalmente i problemi tipici (debugging o auto-riferimento) intrinseci all'approccio con funzioni anonime.

**Regola d'oro**: le dichiarazioni di funzione richiedono sempre un nome, mentre per le espressioni è opzionale ma vi è un ampio consenso sul fatto che dovrebbero possederne uno.

### Vantaggi Principali

1. **Stack Trace Chiaro ed Esplicativo**: Durante una sessione di debugging, il nome della funzione designata appare nitidamente nei messaggi di errore e nei log del call stack. Ciò accelera enormemente l'identificazione e la risoluzione dei problemi.
2. **Auto-riferimento Affidabile**: Il nome della funzione è reso immutabilmente disponibile all'interno del proprio scope. Questo assicura l'esecuzione di ricorsioni sicure e permette alla funzione di deregistrare se stessa (ad esempio da dispatcher di eventi) senza fare affidamento sulle variabili esterne, che potrebbero mutare nel tempo.
3. **Auto-documentazione intrinseca**: Un nome autoesplicativo funge da documentazione in linea permanente, indicando immediatamente l'intento logico di un blocco di codice senza che sia necessario compilarne visivamente l'implementazione interna.
4. **Isolamento e Sicurezza dello Scope**: Il nome assegnato all'espressione di funzione agisce esclusivamente all'interno del proprio perimetro locale, non disperdendosi per inquinare lo scope circostante.

### Esempi Pratici

L'applicazione di nomi è utile in molteplici scenari quotidiani:

```javascript
// ✅ Callback nominati: auto-documentazione e debugging facilitato
valori.map(function raddoppiaValore(numero) {
  return numero * 2; // Intento evidente al primo sguardo
});

// ✅ Event handlers nominati: rendono facile il disaccoppiamento
pulsante.addEventListener("click", function gestisciPressione(evento) {
  // Struttura predisposta per un'eventuale pulizia pulita
});

// ✅ Timer nominati: chiarezza d'intento in operazioni differite
setTimeout(function chiudiConnessioneLenta() {
  console.log("Connessione chiusa per inattività.");
}, 5000);

// ✅ Strutture ricorsive immutabili e sicure
var calcolaFattoriale = function calcoloInterno(n) {
  if (n <= 1) return 1;
  return n * calcoloInterno(n - 1); // Indipendente dalla variabile esterna
};

var riferimento = calcolaFattoriale;
calcolaFattoriale = null;
riferimento(5); // Restituisce 120 e funziona perfettamente in autonomia
```

L'adozione sistematica del nominare intenzionalmente il codice migliora in modo drammatico la purezza e la robustezza del software.

## 📌 Tag

#javascript #functions #named-functions #best-practices #readability
