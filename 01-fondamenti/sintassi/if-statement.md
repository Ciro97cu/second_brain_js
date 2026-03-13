# [[../../appunti-completi#26-istruzioni-condizionali-conditionals|Istruzione if]]

L'istruzione `if` rappresenta la struttura condizionale fondamentale nella programmazione. Essa consente di eseguire un determinato blocco di codice esclusivamente *se una specifica espressione valutata risulta vera*.

La condizione da esaminare viene posta all'interno di parentesi tonde `()` e viene interpretata dal linguaggio producendo un risultato booleano (`true` o `false`). Qualora l'espressione non sia intrinsecamente un booleano, essa viene automaticamente sottoposta al processo di cast logico seguendo le regole interne di truthiness del linguaggio.

```javascript
/*
 * Sintassi base if
 */

if (condizioneDaValutare) {
  // blocco di istruzioni eseguito unicamente se la condizione risulta vera
}

// Esempio d'uso pratico
let etaInAnni = 18;

if (etaInAnni >= 18) {
  console.log("Accesso consentito al sistema");
}

let temperaturaRilevata = 35;

if (temperaturaRilevata > 30) {
  console.log("La temperatura è superiore ai parametri standard");
}
```

Nel caso in cui l'espressione valutata generi il valore `false`, o venga interpretata come *falsy*, il relativo blocco di codice delimitato tra parentesi graffe viene omesso. Il motore prosegue quindi l'esecuzione logica delle istruzioni poste in seguito alla parentesi graffa di chiusura `}` e il programma continua regolarmente senza ulteriori impatti causati dal blocco evitato.

```javascript
/*
 * Dinamiche di salto per condizioni non verificate
 */

let punteggioOttenuto = 45;

if (punteggioOttenuto >= 60) {
  // Questo log o qualsiasi altra operazione
  // prescritta, NON verrà interpretato
  console.log("Certificazione ottenuta con successo"); 
}

console.log("L'analisi dello script è giunta al termine"); // Istruzione invariabilmente processata
```

La padronanza di tale costrutto logico serve come gradino principale su cui si erige qualsiasi flusso decisionale più complesso, restando perno indiscutibile del controllo della ramificazione del codice.
