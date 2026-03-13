# [[../../appunti-completi#immutabilità-degli-oggetti-immutability|Immutabilità degli Oggetti (Immutability)]]

L'immutabilità si riferisce al concetto base che un oggetto, una volta creato, non può essere modificato. Invece di modificare l'oggetto originale, viene creato un nuovo oggetto con le modifiche desiderate. Questo approccio è ampiamente utilizzato nella programmazione funzionale per garantire la prevedibilità e l'affidabilità delle applicazioni.

In JavaScript, per impostazione predefinita ogni oggetto creato è completamente mutabile. Per allinearsi a queste esigenze di sicurezza architetturale, ES5 ha introdotto vari metodi strutturati per imporre e governare tecnicamente livelli diversi di blocco (impedendo l'aggiunta, la riconfigurazione o la modifica delle proprietà).

## 🎯 Concetti Chiave

Tutti questi meccanismi offrono esclusivamente una **Shallow Immutability** (Immunità Superficiale). I metodi bloccano l'oggetto di primo livello sui cui sono chiamati, ma non sigillano ricorsivamente i riferimenti interni di array od oggetti secondari, i quali rimarranno pienamente operabili.

- **Non estendibilità (preventExtensions)**: Niente nuove proprietà.
- **Sigillatura (seal)**: Niente nuove proprietà + niente rimozione/riconfigurazione (ma i valori delle chiavi restano sovrascrivibili).
- **Congelamento totale (freeze)**: Niente nuove, niente rimozioni, nessuna modifica. Tutto bloccato.
- **Costante manuale**: Applicazione atomica manuale dei `property-descriptors`.

## 💻 Esempi di Codice

### 1. Costante di Oggetto

Permette di bloccare non la struttura in sé, ma una singola proprietà specifica manipolando i suoi Descrittori.

```javascript
var obj = {};
Object.defineProperty(obj, "COSTANTE", {
  value: 42,
  writable: false,
  configurable: false,
});
```

### 2. Prevent Extensions

Blocca in via definitiva l'aggiunta di nuove "voci" al dizionario, preservando libertà tecnica sulle già esistenti.

```javascript
var obj = { a: 2 };
Object.preventExtensions(obj);
obj.b = 3; // Fallisce (TypeError in strict mode)
console.log(obj.b); // undefined
```

### 3. Seal (Sigillare)

Come `preventExtensions` ma blocca in automatico a `configurable: false` tutte le proprietà attuali, inibendo perciò i `delete`.

```javascript
var obj = { a: 2 };
Object.seal(obj);
delete obj.a; // Fallisce
```

### 4. Freeze (Congelare)

Come `seal` ma per tutte le variazioni setta in modo cumulativo `writable: false`. Nessuna eliminazione e nessuna modifica dei field primitivi. In sostanza, un'entità perennemente statica.

```javascript
var obj = { a: 2 };
Object.freeze(obj);
obj.a = 5; // Fallisce
console.log(obj.a); // Resta ancorato a 2
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Falso senso di sicurezza e array interni**: Richiamare `Object.freeze()` su un oggetto che al suo interno contiene un array non ostacolerà le routine come l'.`push()` effettuate sopra l'array stesso, in quanto l'immunità non è per propagazione automatica.
- ❌ **Uso e abuso di un Freeze totale in Deep**: Provare ad iterare ricorsivamente per costruire un "Deep Freeze" completo può essere sintomo primario di un programma che si protegge nel modo sbagliato invece di abbracciare la reattività del linguaggio, scatenando effetti collaterali se quegli asset base risultano referenziati da moduli paralleli.

## 🔗 Collegamenti

**Prerequisiti**:

- [[oggetti]]
- [[property-descriptors]]

**Correlati**:

- [[duplicazione-oggetti]]
