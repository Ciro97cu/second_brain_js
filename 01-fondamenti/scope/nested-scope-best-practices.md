# [[../../appunti-completi#scope-annidato-nested-scope|Errori Comuni e Best Practices nello Scope]]

Nella gestione degli scope annidati e della scope chain, è facile incorrere in malintesi sulla direzione della ricerca e sulla visibilità delle variabili. L'uso accurato previene errori silenziosi.

## Errori Comuni

### Confondere direzione della ricerca

L'Engine JavaScript risale sempre verso l'esterno, senza mai esplorare i livelli più interni.

```javascript
function esterna() {
  let x = 10;

  function interna() {
    console.log(x); // ✅ OK, risale a esterna
  }

  interna();
}

console.log(x); // ❌ ReferenceError: non può scendere negli scope interni
```

### Aspettarsi l'accesso a variabili "fratello"

Gli scope che si trovano allo stesso livello nidificato (ovvero che non sono reciprocamente annidati l'uno nell'altro) agiscono come moduli isolati e non riescono in nessun modo a condividere le loro variabili locali e di conseguenza causano un errore durante l'esecuzione del codice.

```javascript
function funzioneA() {
  let x = 10;
}

function funzioneB() {
  console.log(x); // ❌ ReferenceError: funzioneA e funzioneB sono "fratelli", non annidati
}
```

## Best Practices per l'Architettura

**Comprendere la direzione risolutiva**: La ricerca degli identificatori procede sempre ed esclusivamente **dal locale al globale**, mai il contrario.

**Minimizzare livelli di annidamento**: Troppi livelli annidati rendono difficile tracciare il percorso della scope chain e frammentano la qualità del codice. È consigliabile mantenere una struttura prevalentemente piatta e chiara.

**Naming esplicito**: Si raccomanda di utilizzare nomi significativi, estesi e unici per evitare confusione durante l'interazione degli scope annidati.

```javascript
// ❌ Troppi livelli annidati (difficile e faticoso da interpretare visualmente)
function a() {
  function b() {
    function c() {
      function d() {
        // L'operazione "mentale" di mapping variabile-scope è troppo frammentata
      }
    }
  }
}

// ✅ Struttura più piatta e chiara (preferibile)
function elaboraDati(input) {
  const config = caricaConfig();
  return trasformaDati(input, config);
}

function trasformaDati(dati, config) {
  // Logica e riferimenti separati, scope nettamente tracciabile.
}
```
