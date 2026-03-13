# [[../../appunti-completi#scelta-verifiche-strutture-dati|Scelta e Verifica delle Strutture Dati]]

Il sistema dei tipi impone un'attenzione meticolosa alla selezione delle strutture dati più appropriate per ciascun utilizzo, oltre che al controllo sulla natura degli elementi manipolati. L'operatore `typeof` può presentare diverse ambiguità quando applicato a determinati costrutti (ad esempio per array o entità `null`).

## Verifiche dei Tipi

Evidenziando i problemi dell'operatore generico `typeof` quando si distinguono array, null o sottotipi:

```javascript
// typeof si dimostra impreciso negli array (ritorna "object")
let arr = [1, 2, 3];
console.log(Array.isArray(arr)); // true (Modo corretto e diretto)

// instanceof si applica a eventuali sottotipi 
console.log(arr instanceof Array); // true

// typeof null causa bug retrocompatibili
let nullo = null;
if (nullo === null) {
  // Questa comparazione diretta risulta sicura e idonea
}
```

## Come Scegliere la Struttura Identificativa

Secondo standard consolidati, si consiglia l'adozione di un'entità differente per finalità precise:

- **Array**: Esclusivamente per **collezioni ordinate**. La natura numerica ed automatizzata degli indici consente l'uso dei metodi iterativi (es. `.map()`, `.filter()`). 
- **Oggetto Letterale (Object)**: Principalmente per le **chiavi arbitrarie** che necessitano di mappatura descrittiva con comportamento associativo (es. configurazioni server).

```javascript
// Array: Sequenze ed elaborazione indici
let punteggi = [95, 87, 92];

// Object: Mappatura chiave-valore eterogenea
let configurazione = {
  host: "localhost",
  port: 3000
};
```

- **Function**: Incapsulamento di frammenti algoritmici. Trattandosi di un cittadino di prima classe ("callable object"), trova utilità per la logica reiterabile ed implementazione callback.
- **Map**: Ideale per memorizzare accoppiamenti dinamici quando lo schieramento delle chiavi richiede flessibilità aggiuntiva, accettando chiavi basate non solamente sulle stringhe convenzionali (es. oggetti iterati, istanze di classi come identificatori).
- **Set**: Utile al fine di rimuovere repliche da sorgenti dati originari disorganizzati per favorire l'unicità.