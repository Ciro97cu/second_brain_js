# [[../../../appunti-completi#this-come-funzione-stessa-le-soluzioni|this come Funzione Stessa: Le Soluzioni]]

Quando si comprende che `this` non punta automaticamente alla funzione stessa durante un'invocazione standard, è necessario valutare le opzioni corrette per gestire lo stato correlato alla funzione oppure per forzare esplicitamente l'associazione del contesto.

## ⚠️ Soluzioni Alternative (Basate sullo Scope)

Per evitare le complessità associate a `this`, si ricorre spesso a soluzioni basate sullo scope lessicale. Sebbene funzionanti, queste ignorano la comprensione profonda di come opera il binding in JavaScript.

### Soluzione con Oggetto Esterno

Una pratica comune prevede l'utilizzo di un oggetto separato creato nell'ambiente circostante.

```javascript
var data = { count: 0 };

function foo(num) {
  console.log("foo: " + num);
  data.count++; // Sfrutta il lexical scope
}

for (var i = 0; i < 10; i++) {
  if (i > 5) {
    foo(i);
  }
}

console.log(data.count); // 4 - Esecuzione corretta
```

**Valutazione**: Risolve il sintomo architetturale, ma rinuncia a imparare i meccanccanismi di `this`, affidandosi unicamente allo scope lessicale esterno.

### Soluzione con Nome della Funzione Lessicale

Un approccio analogo sfrutta l'identificatore lessicale con cui la funzione è stata definita.

```javascript
function foo(num) {
  console.log("foo: " + num);
  foo.count++; // Si riferisce direttamente all'oggetto funzione tramite il suo nome lessicale
}

foo.count = 0;

for (var i = 0; i < 10; i++) {
  if (i > 5) {
    foo(i);
  }
}

console.log(foo.count); // 4 - Esecuzione corretta
```

**Valutazione**: Anche questa opzione aggira `this`, facendo completo affidamento sullo scope lessicale.

#### La Questione delle Funzioni Anonime

Il limite della referenza al nome della funzione emerge in maniera evidente qualora non esista un nome (funzioni anonime).

```javascript
setTimeout(function () {
  // Risulta impossibile riferirsi a se stessa tramite nome lessicale
  // poiché l'identificatore è assente.
}, 10);
```

Per necessità di auto-riferimento statico interno, come la ricorsione, è indicato impiegare funzioni nominate (named functions) evitando quelle anonime.

## ✅ Soluzione Corretta: Forzare this con i Metodi Ereditati

Per risolvere la problematica abbracciando l'architettura dinamica di JavaScript, l'approccio ideale consiste nel forzare esplicitamente il contesto in fase di esecuzione.

```javascript
function foo(num) {
  console.log("foo: " + num);
  this.count++; // Grazie al binding esplicito, this corrisponde a foo
}

foo.count = 0;

for (var i = 0; i < 10; i++) {
  if (i > 5) {
    /*
     * L'utilizzo di call() forza il binding in modo che "this"
     * corrisponda intenzionalmente all'oggetto funzione (foo) stesso
     */
    foo.call(foo, i);
  }
}

console.log(foo.count); // 4 - Esecuzione corretta e coerente col motore
```

**La spiegazione**: Utilizzando il metodo `.call()`, non si elude la valutazione dinamica. Al contrario, si applica una tecnica definita _explicit binding_ controllando esattamente a cosa l'identificatore `this` debba riferirsi.

## 📊 Confronto Analitico degli Approcci

| Approccio                                   | Risultato Operativo | Utilizzo di this  | Valutazione Tecnica                               |
| ------------------------------------------- | ------------------- | ----------------- | ------------------------------------------------- |
| `this.count++` in chiamata diretta          | ❌ Fallisce         | Sì (involontario) | Si poggia sul Default Binding (globale/undefined) |
| Oggetto esterno `data.count++`              | ✅ Completa         | No                | Elusione tramite Lexical Scope                    |
| Nome funzione `foo.count++`                 | ✅ Completa         | No                | Elusione tramite Lexical Scope                    |
| Explicit binding tramite `foo.call(foo, i)` | ✅ Completa         | Sì (volontario)   | Abbraccia l'Explicit Binding gestito              |

---

**Tags**: `#javascript` `#this` `#binding` `#call` `#lexical-scope`
