# [[../../../appunti-completi#this-come-funzione-stessa-l-illusione|this come Funzione Stessa: L'Illusione]]

Una delle confusioni più comuni, a causa del significato inglese della parola, è assumere che `this` si riferisca alla funzione stessa. Dal punto di vista grammaticale può sembrare ragionevole, ma si tratta di un presupposto scorretto in JavaScript.

## 🎯 Concetti Chiave

- `this` non punta in modo automatico alla funzione stessa in cui è definito.
- Le funzioni sono oggetti in JavaScript, pertanto possono avere proprietà, ma `this` non crea un riferimento automatico ad esse.
- Per riferirsi a una funzione dall'interno, si raccomanda l'uso dell'identificatore lessicale (il nome della funzione).
- Altrimenti è necessario forzare esplicitamente il binding di `this` tramite metodi dedicati come `call()`.

## 💻 Il Problema: Tentativo di Tracciare Chiamate

### Codice che Fallisce

Nell'esempio seguente si cerca di tracciare quante volte una funzione viene chiamata, aggiungendo una proprietà `count` direttamente all'oggetto funzione e tentando di incrementarla tramite `this`.

```javascript
function foo(num) {
  console.log("foo: " + num);
  this.count++; // L'illusione: si presume che this sia uguale a foo
}

foo.count = 0; // Aggiunta proprietà count alla funzione foo

for (var i = 0; i < 10; i++) {
  if (i > 5) {
    foo(i);
  }
}
// foo: 6
// foo: 7
// foo: 8
// foo: 9

console.log(foo.count); // 0 -- Il contatore non è stato incrementato
```

**Cosa avviene in realtà**: La funzione viene chiamata 4 volte, ma il valore di `foo.count` rimane 0.

### Spiegazione del Fallimento

1. L'istruzione `foo.count = 0` crea effettivamente una proprietà `count` sull'oggetto funzione `foo`.
2. Quando avviene l'esecuzione tramite `foo(i)` (una chiamata di tipo diretto o *standalone*), l'associazione di `this` all'interno della funzione non punta a `foo`, ma viene applicato il *default binding*.
3. Di conseguenza, `this` fa riferimento all'oggetto globale (oppure risulterà `undefined` se si opera in *strict mode*).
4. L'operazione `this.count++` va così a creare accidentalmente una variabile globale `count` con valore `NaN` (poiché eseguire l'incremento `undefined++` genera `NaN`).
5. La proprietà originale `foo.count` associata alla funzione rimane intoccata al suo valore iniziale di 0.

## 💡 Ragioni Dietro alla Confusione

Le ragioni per cui questo malinteso è così radicato includono diversi fattori:

1. **Suggestione grammaticale**: La parola "this" in inglese evoca l'idea di "se stesso".
2. **Struttura di JavaScript**: Le funzioni in JavaScript sono a tutti gli effetti oggetti con la capacità di ospitare proprie proprietà.
3. **Apparente comodità**: La capacità di memorizzare uno stato all'interno della funzione stessa appare come un design pattern vantaggioso.

La verità strutturale è che `this` viene progettato e impiegato per il **binding dinamico a oggetti esterni** sulla base del contesto di invocazione (*call-site*), e non per generare un'auto-referenza statica all'interno del corpo della funzione.

---

**Tags**: `#javascript` `#this` `#confusioni` `#default-binding`
