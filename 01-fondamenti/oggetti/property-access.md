# [[../../appunti-completi#accesso-alle-proprietà-degli-oggetti|Accesso alle Proprietà (Property Access)]]

JavaScript gestisce l'accesso e l'assegnazione dei valori degli oggetti (o alle variabili al loro interno definite) attraverso un efficace set minimale di regole per le proprietà e i loro costrutti lessicali.

Il tema è stato riorganizzato atomicamente nei seguenti concetti primari:

- [[dot-vs-bracket-notation]] - Differenze di base tra notazione col punto (`.`) e tramite parentesi quadre (`[]`).
- [[dynamic-property-access]] - Utilizzo e risoluzione in run-time mediante variabili (bracket access).
- [[computed-property-names]] - Costruzione di chiavi dinamiche a compile-time (object-literals) mediante ES6.
- [[property-names-as-strings]] - Coercizione di tutte le chiavi inserite in stringhe primitive.
- [[property-contents-model]] - Visione puntiforme e meccanismo di stoccaggio referenziale.

## Utilizzo Consolidato e Raccomandazioni Generali

Le **best practices** consolidano la gestione del codice nel seguente approccio combinato: si fissa la **dot notation** per l'espletamento primario e leggibile di routine standard o dove l'identificativo esista di base a compile-time. L'alternativa flessibile, la **bracket notation**, viene ripresa qualora sussistano l'esigenza di una computazione dinamica, il passaggio d'input esterni irrisolvibili nell'editor o il ricorso a set contenenti caratteri fuorilegge come i classici _trattini hyphen_.

```javascript
/* Panoramica Integrata delle Sintassi */
var config = {
  host: "localhost",
  "api-key": "abc123",
};

/* Dot notation per nomi puliti */
console.log(config.host); // "localhost"

/* Bracket access per chiavi "irregolari" e/o composizione dinamica */
var specialProperty = "api-key";
console.log(config[specialProperty]); // "abc123"
```
