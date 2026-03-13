# [[../../appunti-completi#26-istruzioni-condizionali-conditionals|L'Alternativa else]]

Nello sviluppo di software strutturato, emerge spesso la necessità di stabilire un comportamento in fallback o diametralmente opposto al caso positivo. Quando risulta obbligatorio definire un percorso alternativo da adottare qualora la condizione iniziale delineata dall'istruzione `if` venga valutata come falsa, si fa ricorso all'istruzione `else`.

```javascript
/*
 * Architettura della struttura if...else
 */

let etaRegistrata = 15;

if (etaRegistrata >= 18) {
  // Primo scenario: Condizione soddisfatta
  console.log("Utente considerato maggiorenne");
} else {
  // Secondo scenario: Condizione disattesa
  console.log("Utente considerato minorenne");
}
```

La clausola accessoria `else` garantisce un **percorso nettamente esclusivo**: in un costrutto del genere, sempre e unicamente uno dei due segmenti di codice presenti viene processato in un singolo passaggio di esecuzione. Le tempistiche o lo stato non permetteranno mai che i due blocchi vengano eseguiti a cascata indipendentemente dalle variazioni di flusso interne successive.

```javascript
/*
 * Selezione definita dei percorsi d'analisi
 */

let misurazioneOra = 14;

if (misurazioneOra < 12) {
  console.log("Rilevata fascia oraria mattutina");
} else {
  console.log("Rilevata fascia oraria post-meridiana o serale");
}
```

Implementare il ramo supplementare attraverso `else` chiarisce le operazioni e incrementa la robustezza funzionale. Questo meccanismo di programmazione permette agli algoritmi di rispondere in maniera deterministica, definendo esplicitamente le direttive base o i casi di deflusso senza trascurare le casistiche inattese e mitigando ogni potenziale incertezza decisionale.
