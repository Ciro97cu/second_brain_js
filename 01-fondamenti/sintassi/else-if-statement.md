# [[../../appunti-completi#26-istruzioni-condizionali-conditionals|Condizioni Multiple con else if]]

In circostanze ove sia richiesto il partizionamento della logica attraverso una catena di opzioni alternative consecutive, diventa pratica standard far uso della direttiva `else if`. Il motore analizza tutte le diramazioni proposte procedendo **sequenzialmente dall'alto verso il basso**. Al verificarsi della primissima espressione in grado di fornire risultato affermativo (`true`), la valutazione si interrompe istantaneamente, espletando esclusivamente la componente di codice accorpata a tale selezione specifica.

```javascript
/*
 * Implementazione della catena completa if...else if...else
 */

let votoFinalizzato = 85;

if (votoFinalizzato >= 90) {
  console.log("Fascia d'Eccellenza");
} else if (votoFinalizzato >= 75) {
  console.log("Esito: Buono");
} else if (votoFinalizzato >= 60) {
  console.log("Esito: Sufficiente");
} else {
  console.log("Esito: Insufficiente");
}
```

**Caratteristica preminente da osservare**: Solo il **primo contingente di istruzioni** provvisto di una regola equivalente alla verità produrrà un effetto nel circolo dell'applicazione. Nessuna ulteriore disamina prenderà parte ai cicli di elezione, ignorando parimenti tutte le istruzioni consecutive inserite nel reticolo, perfino qualora manifestino logiche di per sé corrette.

```javascript
let quantitaGenerata = 100;

if (quantitaGenerata > 50) {
  console.log("Superato limite cinquanta percento"); // Selezionato, azzerando i controlli inferiori
} else if (quantitaGenerata > 75) {
  console.log("Superato limite tre quarti"); // Totalmente saltato nel flusso esecutivo, nonostante l'assioma sia retto
}
```

Il blocco gestito tramite la macroistruzione `else` diviene il ramo di ripiego; qualora accadesse che all'interno della struttura **nessuna combinazione valga come confermata**, subentrerà la porzione delegata all'alternativa generica finale, conducendo a compimento i processi in via esclusiva e in sicurezza operativa per scongiurare vuoti applicativi.
