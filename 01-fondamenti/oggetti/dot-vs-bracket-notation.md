# [[../../appunti-completi#dot-vs-bracket-notation|Dot vs Bracket Notation]]

JavaScript offre due sintassi principali per accedere (e assegnare) le proprietà di un oggetto: la **dot notation** (`.`) e la **bracket notation** (`[]`). La scelta tra le due dipende dalla natura del nome della proprietà.

## Le Due Sintassi

```javascript
var myObject = {
  a: 2,
};

/* Dot notation (property access) */
myObject.a; // 2

/* Bracket notation (key access) */
myObject["a"]; // 2
```

Entrambe le notazioni accedono alla stessa posizione in memoria e restituiscono lo stesso valore. Benché a volte vengano chiamate "property access" e "key access", i termini sono intercambiabili, e si riferiscono alla stessa operazione.

## Dot Notation: Semplicità e Leggibilità

La dot notation è preferibile quando possibile, poiché risulta più concisa e leggibile. Tuttavia, richiede che il nome della proprietà sia un **Identifier** JavaScript valido.

Un identifier valido:
- Inizia con una lettera, `_` o `$`.
- Contiene solo lettere, numeri, `_` o `$`.
- Non contiene spazi, trattini o caratteri speciali.

```javascript
var persona = {
  nome: "Mario",
  _private: "dato",
  $special: "valore",
};

/* Validi con dot notation */
persona.nome;
persona._private;
persona.$special;

/* Sintassi non valida */
// persona.first-name;  // Syntax Error (trattino)
// persona.123abc;      // Syntax Error (inizia con numero)
```

## Bracket Notation: Flessibilità Assoluta

La bracket notation accetta **qualsiasi stringa UTF-8/Unicode** come nome di proprietà, aggirando le limitazioni degli identifier. È l'unica opzione quando il nome della proprietà contiene caratteri speciali o non è un identifier valido.

```javascript
var obj = {
  "Super-Fun!": "valore",
  "first-name": "Mario",
  "😊": "emoji",
};

/* Validi con bracket notation */
obj["Super-Fun!"];
obj["first-name"];
obj["😊"];

/* Impossibili con dot notation */
// obj.Super-Fun!;      // Syntax Error
// obj.first-name;      // Syntax Error
```

## Scelta della Sintassi

Si raccomanda di usare la dot notation come impostazione predefinita quando il nome della proprietà è fisso, noto a priori e compatibile con le regole degli identifier. La bracket notation diventa necessaria per nomi con caratteri speciali o quando l'accesso deve essere risolto in modo dinamico.

## Collegamenti
- [[property-access]] - Riepilogo e indice dell'accesso alle proprietà.
- [[dynamic-property-access]] - Utilizzo di espressioni e variabili con bracket notation.
