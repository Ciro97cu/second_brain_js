# [[../../appunti-completi#modello-contents|Il Modello dei Contenuti (Contents) degli Oggetti]]

Quando ci si riferisce ai valori residenti all'interno delle proprietà di un oggetto, si sfrutta largamente il concetto di _"contenuto fisico"_ (appunto, "contents"). Pur trattandosi di un modello mentale assai proficuo, calato nelle specificità del motore JavaScript di basso livello esso risulta astratto ed impreciso.

## La Realtà Tecnica dei Riferimenti

Tecnicamente, non è consigliabile pensare in JavaScript a un oggetto come un agglomerato denso atto a chiudere o inglobare materiale "dentro" le proprie parentesi, qualora i valori in essere spazino dal primitivo al complesso: l'oggetto è una rudimentale e flessibile tabella associativa.

Pertanto, le entità mantengono e raggruppano essenzialmente i **nomi delle loro proprietà**, corredati ognuno a **delle referenze**, o puntatori. Ciascun riferimento punta alle reali allocazioni allocate nella memoria preposta (Heap).

```javascript
var myObject = {
  a: 2,
};

/*
 * Modello concettuale (semplificato comunemente)
 * -> myObject racchiude il numero 2 nella voce 'a'
 *
 * Realtà Tecnica dei Riferimenti
 * -> myObject detiene 'a', allocata come riferimento
 *    che guarda e segue il posizionamento dove il numero 2 stagna
 */
```

## Implicazioni Pratiche della Referenziazione

Tale separazione architettonica decodifica la logica "per riferimento", fondamentale nel passaggio e la coabitazione dei tipi d'oggetto: differenti variabili in possesso del medesimo oggetto non condividono in vero una scatola "contenitiva", ma una copia nuda del proprio puntatore.

```javascript
var obj1 = { x: 10 };
var obj2 = obj1; // Entrambi mirano alla stessa destinazione in memoria

/* Mutare una rotta la rende visibile ad ambedue le sponde */
obj2.x = 20;
console.log(obj1.x); // 20
```

Il fatto ineluttabile di avere un valore slegato in una referenza autonoma garantisce alla natura debolmente tipizzata di mutare un oggetto "genitore" lasciando al tempo stesso propaggini vive per tutta la base code ove sia diffuso il suo puntatore iniziale.
