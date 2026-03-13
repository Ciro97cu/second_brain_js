# [[../../appunti-completi#blocchi-come-scope-blocks-as-scopes|Comportamento del Garbage Collector]]

## Cosa il GC Può Determinare
Il motore elabora le informazioni sullo scope per decidere quali riferimenti possono essere liberati in sicurezza. Utilizzando lo scope di blocco esplicito nella sintassi ES6, si forniscono al GC confini chiari in base ai quali liberare o trattenere le allocazioni in memoria.

```javascript
function example() {
  let outer = "mantieni questo";
  {
    let temp = createLargeObject(); // 50MB
    outer += process(temp);
  }
  // GC libera 'temp'
  return outer;
}
```

Il GC può liberare la variabile dal momento in cui è dichiarata in un blocco ormai terminato e nessuna closure esterna può più risalirvi in alcun modo, trovandosi in uno scope lessicale inaccessibile.

## Differenza con Function Scope (`var`)
Utilizzare costrutti `var` costringe il motore a comportamenti altamente conservativi che impediscono la pulizia ottimale in determinate architetture e flussi asincroni.

```javascript
function example() {
  var outer = "mantieni questo";
  {
    var temp = createLargeObject(); // 50MB
    outer += process(temp);
  }
  // temp non può essere liberato in modo certo
  return outer;
}
```

Essendo `var` vincolato al solo scope di funzione o globale, al termine del blocco il riferimento permane come potenziale accesso futuro per il tracciamento del motore, rimandandone forzosamente la deallocazione di memoria al termine del runtime della funziona madere.

## Linee Guida sull'Ottimizzazione
L'uso stringente di blocchi espliciti è caldamente raccomandato per:
- Dati temporanei superiori a 1MB.
- Scenari architettati con closures di lunga vita (ascoltatori di eventi, timer).
- Molteplici iterazioni in mapping o cicli asincroni con dati pesanti in entrata.

Non è necessario (e spesso eccessivo) utilizzarli per variabili primitive minuscole, strutture molto leggere, o funzioni isolate che terminano rapidamente senza creare closures persistenti. Abusare di tali strutture genera un accumulo di dichiarazioni logiche non proporzionale ai reali benefici sul footprint di RAM.
