# [[../../appunti-completi#nomi-delle-proprietà-come-stringhe|Nomi delle Proprietà come Stringhe]]

Negli oggetti JavaScript, **i nomi delle proprietà sono sempre e solo stringhe** (o, a partire da ECMAScript 6, dei `Symbol`). Qualsiasi altro tipo di dato utilizzato come chiave di un oggetto viene convertito automaticamente e implicitamente in stringa dal motore del linguaggio.

## Coercizione Automatica

Se si tenta di utilizzare un valore che non sia una stringa come nome per una determinata proprietà (tramite la sintassi bracket), JavaScript ne forza la conversione invocando internamente il metodo `toString()`.

```javascript
var myObject = {};

/* Assegnazione con chiavi non-stringa */
myObject[true] = "foo"; // true viene forzato in "true"
myObject[3] = "bar"; // il numero 3 diventa "3"
myObject[myObject] = "baz"; // l'oggetto viene serializzato a "[object Object]"

/* Lettura sfruttando le chiavi testuali convertite */
console.log(myObject["true"]); // "foo"
console.log(myObject["3"]); // "bar"
console.log(myObject["[object Object]"]); // "baz"
```

Questo comportamento nasconde un'insidia comune: poiché ogni oggetto base viene convertito, senza override espliciti, nella stringa `"[object Object]"`, utilizzare svariati oggetti distinti come chiavi sovrascrive sempre la sola proprietà di quel medesimo nome sul target.

## Numeri come Chiavi (Array vs Oggetti)

La natura testuale di tutte le chiavi genera spesso confusione durante l'utilizzo dei numeri, poiché questi assumono valenza identica a stringhe.

```javascript
var arr = ["a", "b", "c"];

/* Indici numerici divengono stringhe per l'astrazione JSON nativa degli array */
console.log(arr[0]); // "a"
console.log(arr["0"]); // "a"

console.log(Object.keys(arr)); // ["0", "1", "2"]
```

### La Differenza Architetturale

L'ingannevole familiarità sintattica occulta una rilevante differenza concettuale tra usare indici in un array nativo rispetto a impiegare chiavi numerate in un oggetto base:

1. **Array**: Strutture pre-ottimizzate per collezioni ordinate fondate nativamente su indici. Gestiscono proprietà specifiche e mutevoli (`length`) assorbendo regole specializzate interne ai compilatori per alte prestazioni.
2. **Oggetti Base**: Inserendovi proprieta denominate come `obj[0] = 10` si costruiscono mere stringhe nominali senza ordimento intrinseco, al di fuori d'ogni ottimizzazione matematica in sequenza e sprovviste del corredo Array (es. array map).

Si incoraggia fortemente l'impiego degli oggetti solo qualora per natura lo stoccaggio richieda mappature nominali destrutturate, relegando al tipo Array ogni sequenzialmente relazionata collezione numerica.
