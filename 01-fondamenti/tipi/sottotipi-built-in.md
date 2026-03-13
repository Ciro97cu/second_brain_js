# [[../../appunti-completi#sottotipi-built-in|Sottotipi di Object Built-in]]

JavaScript offre, oltre ai valori primitivi, un unico tipo complesso: `object`. Tuttavia, esistono diverse costruzioni built-in che si comportano come sottotipi specializzati del tipo oggetto di base, ciascuno con capacità specifiche.

## Function: Callable Objects (First-Class Citizens)

Le funzioni sono oggetti. Più precisamente, si tratta di un sottotipo specializzato di `object` in grado di essere invocato ("callable"). 

```javascript
function saluta(nome) {
  return `Ciao, ${nome}!`;
}

console.log(typeof saluta); // "function"
console.log(saluta instanceof Object); // true

// Proprietà interne accessibili
saluta.linguaggio = "Italiano";
console.log(saluta.length); // 1 (numero di argomenti attesi)
console.log(saluta.name); // "saluta"
```

Le funzioni sono considerate "first-class citizens": possono essere assegnate a variabili, passate come argomenti o restituite da altre funzioni. 

## Array: Oggetti ad Indice Numerico

Anche gli array sono oggetti, ottimizzati per gestire collezioni ordinate e indicizzate numericamente.

```javascript
let numeri = [10, 20, 30];

console.log(typeof numeri); // "object"
console.log(Array.isArray(numeri)); // true

numeri.push(40);
console.log(numeri.length); // 4
```

Essendo oggetti, possono memorizzare anche proprietà non numeriche (sebbene sia una pratica sconsigliata). Queste ultime non influiscono sulla proprietà `length`.

## Altri Sottotipi Specializzati

L'ecosistema JavaScript fornisce ulteriori sottotipi per gestire necessità specifiche:

- **Date**: Gestione strutturata di date e orari.
- **RegExp**: Rappresentazione di espressioni regolari per il pattern-matching interno alle stringhe.
- **Error**: Gestione strutturata delle eccezioni.
- **Map / Set**: Strutture dati esclusive (introdotte in ES6) per gestire collezioni di dati chiave-valore più dinamiche rispetto agli oggetti standard o insiemi di valori univoci.

```javascript
// Date
let adesso = new Date();
console.log(adesso instanceof Date); // true

// RegExp
let pattern = /[a-z]+/i;
console.log(pattern instanceof RegExp); // true

// Map (Chiavi non limitate a stringhe/symbol)
let mappa = new Map();
mappa.set("chiave", "valore");
```