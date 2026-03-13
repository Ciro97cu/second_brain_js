# [[../../appunti-completi#5-operatori|Doppio NOT (!!)]]

Il costrutto del "doppio NOT" (`!!`) non costituisce un singolo operatore indipendente, ma rappresenta l'utilizzo consecutivo di due operatori logici NOT (`!`) allo scopo di forzare la conversione esplicita di un qualsiasi valore nel suo equivalente booleano (`true` o `false`).

## Meccanismo di Conversione

Il primo operatore `!` converte il valore originario nel suo opposto booleano, valutando se esso sia internamente "truthy" o "falsy". Il secondo `!` inverte nuovamente il risultato, ripristinando la logica posizionale di partenza ma ancorandola a un tipo booleano primitivo.

```javascript
let valore = "test";

// Primo passaggio: converte un valore truthy in false
console.log(!valore); // false

// Secondo passaggio: inverte il false in true
console.log(!!valore); // true
```

## Comportamento con Valori Diversi

La conversione tramite `!!` riflette accuratamente in quali circostanze JavaScript considera le variabili piene o vuote:

```javascript
// Valori Truthy (diventano true)
console.log(!!"Hello"); // true
console.log(!!42);      // true
console.log(!![]);      // true (array vuoto)
console.log(!!{});      // true (oggetto vuoto)

// Valori Falsy (diventano false)
console.log(!!0);         // false
console.log(!!"");        // false
console.log(!!null);      // false
console.log(!!undefined); // false
```

## Contesti di Utilizzo

L'utilizzo del doppio NOT risulta particolarmente diffuso quando occorre garantire che una funzione o una proprietà restituisca esclusivamente un tipo booleano rigoroso, anziché consentire il propagarsi di oggetti, stringhe o assenza di valore.

```javascript
function verificaPresenzaDati(input) {
  return !!input; // Forza Boolean, evitando return di oggetti completi
}

let userData = { email: "mail@test.it" };
let isValid = !!userData.email; 
```

Nelle valutazioni condizionali esplicite (come le istruzioni `if` o le iterazioni `while`), l'operazione di casting booleano e il motore JavaScript operano automaticamente sulle condizioni; l'uso del doppio NOT risulta pertanto logicamente ridondante ed evitabile. 

L'alternativa equivalente, talvolta preferita per chiarezza esplicita, consiste nell'uso della funzione nativa `Boolean(valore)`.
