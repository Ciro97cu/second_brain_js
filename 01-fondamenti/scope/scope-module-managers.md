# [[../../appunti-completi#gestione-dei-moduli-module-management|Scope: Dependency Managers e Regole di Base]]

## Gestori di Dipendenze (Dependency Managers)

L'introduzione dei moduli in JS abilita l'ecosistema a utilizzare "gestori di dipendenze" come npm, che mantengono separate le librerie. Lo scope di un modulo rende possibile importare direttamente ciò di cui c'è bisogno senza dover instanziare nulla sull'oggetto globale.

```json
// package.json
{
  "dependencies": {
    "lodash": "^4.17.21",
    "axios": "^1.0.0"
  }
}
```

Dalle dipendenze locali, ogni parte del modulo diventa facilmente accessibile:

```javascript
// app.js
import _ from 'lodash';
import axios from 'axios';

// Librerie in scope locale, NO globali!
const raddoppiati = _.map([1, 2, 3], n => n * 2);
```

## Struttura dell'Applicazione Modulare

L'architettura classica con i moduli prevede un albero di dipendenze con nodi concatenati tra loro, ad esempio `config.js` \-\> `api-client.js` \-\> `user-service.js` \-\> `app.js`.

Ogni modulo importa solo ciò che gli serve, e crea scope privati a ogni livello. Il risultato è la totale assenza di variabili globali nell'applicazione Javascript sviluppata.

## Scope Lessicale e Moduli

I moduli in JavaScript **non violano** in alcun modo le regole dello scope lessicale del linguaggio, si limitano semplicemente ad appoggiarvisi in questa maniera:

- Ogni file JavaScript trattato come modulo equivale ad una funzione che crea il proprio scope temporaneo privato.
- Utilizzare la keywork `export` serve solamente a rendere accessibili alcuni degli identificatori specifici generati.
- Utilizzare `import` prende gli identificatori dichiarati da qualcos'altro per inserirli in uno scope locale che copre il blocco corrente, anziché quello globale, in un modo equivalente alla dichiarazione con `let` / `const`.
- Il resto delle dichiarazioni e della logica del file rimane privata ed esternamente inaccessibile per sempre, confinata al suo modulo di origine.
