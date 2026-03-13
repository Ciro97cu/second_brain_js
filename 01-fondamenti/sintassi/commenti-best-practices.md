# [[../../appunti-completi#22-commenti-nel-codice-code-comments|Commenti: Best Practices]]

Affinché la stesura del codice non subisca colli di bottiglia e rimanga pienamente funzionale, occorre applicare principi ben equilibrati per documentare la logica delle applicazioni in maniera ottimizzata e poco confusionaria.

## Spiegare il Perché e non il Cosa

Una pratica diffusa ritiene fondamentale che un commento di utilità espliciti il motivo (il "perché") risiedente dietro una specifica scelta tecnica o di calcolo, evitando di parafrasare passaggi logici manifesti e autodescrittivi. Il "cosa fa" il codice si deve riflettere integralmente nei nomi chiari e informativi riservati a variabili e funzioni.

```javascript
// CATTIVA PRATICA: si limita a tradurre verbalmente il codice
let aliquotaScelta = totaleCorrente * 0.15; // Viene moltiplicato per 0.15

// BUONA PRATICA: indica la motivazione operativa/di business
// Standard tariffario internazionale limitato per nazioni non EU e acquisti extra
let aliquotaTasse = totaleSpesa * 0.15;
```

## Bilanciare i Quantitativi di Note

Sebbene il codice debba possedere un'infrastruttura di testi descrittivi nei pressi degli algoritmi complessi, non risulta corretto descrivere ogni singola riga d'assegnamento. Testi sproporzionati confondono spesso il lettore distogliendo la concentrazione dalle componenti applicative stesse e necessitano continua ristesura per manutenere l'allineamento.

## Manutenzione Attiva dell'Informazione

L'invecchiamento dei commenti espone l'impianto generale a criticità sostanziali qualora procedure e costanti risultino non coerenti con le implementazioni originali. Occorre accertarsi puntualmente che i commenti seguano lo scorrere degli aggiornamenti nel sorgente e corrispondano con trasparenza alla build in essere.

```javascript
// Commento non mantenuto da evitare!
// Viene eseguita sempre connessione su Porta 9000
const avviaServizio = (dynHost, webPort = 443) => {
  /* ... */
};
```

In sintesi, la struttura del codice ben redatta funge essa stessa da prima traccia di documentazione per limitare i commenti solo ai punti oscuri o inusuali.
