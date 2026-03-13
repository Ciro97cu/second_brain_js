# [[../../../appunti-completi#311-lidentificatore-this|Problemi con il Binding di this]]

Uno dei problemi più comuni in JavaScript è la **perdita del binding di `this`** quando si passano funzioni come callback o handler. Questo accade perché il call-site determina `this`, non il punto di definizione della funzione.

## 🎯 Indice dei Problemi

In questa sezione esploriamo i problemi di binding e le loro soluzioni:

- [[this-binding-loss|Perdita del Binding]]: Perché `setTimeout` e i callback perdono `this` e come risolvere con arrow functions o `bind()`.
- [[this-binding-exceptions|Eccezioni di Binding]]: Il comportamento imprevisto quando si passano `null` o `undefined` a `call` o `apply`.
- [[this-dmz-object|DMZ Object Pattern]]: Come creare un oggetto sicuro e vuoto come placeholder per `this` ed evitare l'inquinamento globale.
- [[this-indirect-references|Riferimenti Indiretti]]: Come le assegnazioni di funzioni creano riferimenti indiretti che ricadono nel default binding.
- [[this-soft-binding|Soft Binding]]: Un'implementazione custom che fornisce un binding di default sicuro ma flessibile e sovrascrivibile.
- [[this-binding-gotchas|Gotchas o Errori Comuni]]: Trappole comuni come arrow functions usate scorrettamente come metodi o problemi di re-binding.

---

**Tags**: `#javascript` `#this` `#callbacks` `#binding-loss` `#this-problems`
