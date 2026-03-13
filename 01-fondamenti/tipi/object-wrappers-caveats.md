# [[../../appunti-completi#35-boxing-e-metodi-dei-primitivi|Le Insidie dei Wrapper Objects]]

Sebbene JavaScript fornisca i costruttori in forma di wrapper objects (come `String`, `Number`, `Boolean`), l'istanziazione manuale di questi wrapper introduce una serie di complicazioni e insidie che è meglio evitare.

## Problemi di Uguaglianza Stretta

Un wrapper object crea un nuovo oggetto nello heap. L'operatore di uguaglianza stretta `===` differenzia i tipi di riferimento ed i tipi primitivi.

```javascript
var primitivo = "testo";
var wrapper = new String("testo");

console.log(primitivo == wrapper); // true (coercizione implicita)
console.log(primitivo === wrapper); // false! (tipi differenti: string vs object)
```

Anche paragonando due wrapper object creati con il medesimo valore nominalmente si otterranno riferimenti diversi, risultando in falsi logici.

```javascript
var w1 = new String("testo");
var w2 = new String("testo");
console.log(w1 === w2); // false (riferimenti ad oggetti diversi)
```

## L'Insidia dei Booleani Wrapper

L'uso di `new Boolean()` è un tipico anti-pattern che introduce una trappola logica pericolosa. Qualsiasi oggetto in JavaScript, a prescindere dal suo stato o valore temporaneo, è implicitamente valutato come *truthy* se forzato in un controllo booleano coercitivo.

```javascript
/* Il valore booleano false viene avvolto in un oggetto */
var falseWrapper = new Boolean(false);

if (falseWrapper) {
  console.log("Eseguito!"); // ⚠️ Questo blocco VERRÀ eseguito!
}
```

Poiché `falseWrapper` è istanziato da un costruttore (e quindi è di tipo "object"), la coercizione logica implicita lo valuta come vero. Questo occulta il valore contenuto generando ambiguità.

## Nessun Vantaggio Tangibile

L'utilizzo intenzionale e forzato delle forme costruttrici al posto dei letterali è considerato ridondante e prolisso. Il motore JavaScript esegue egregiamente il boxing temporaneo in background al momento del bisogno in modo trasparente e maggiormente performante, rimosso il fardello legato alla manuale e successiva pulizia in memoria per allocazioni ripetitive.

A meno di specifici scenari in cui occorra sovrascrivere o aumentare i prototipi di base in maniera isolata, una base robusta richiede l'osservanza stringente all'esclusivo uso dei valori immutabili preposti. 

## Collegamenti

- [[native-wrappers-vs-primitives]] - Forma letterale vs built-ins
- [[truthy-falsy]] - La valutazione di verità implicita degli oggetti
- [[coercizione-booleana]] - Come JavaScript valuta i riferimenti come positivi
