# [[../../appunti-completi#scope-lessicale-vs-accesso-a-proprietà|Scope Chain vs Prototype Chain]]

La ricerca lungo gli scope annidati e la ricerca lungo la catena dei prototipi vengono spesso confuse, ma regolano aspetti separati del linguaggio JavaScript.

## Differenze Nelle Dinamiche di Risoluzione

Lo scope lessicale opera unicamente per trovare il riferimento alla base dell'espressione (il primo identificatore dell'istruzione). Questa operazione sfrutta le regole dettate dallo scope chain: partendo dallo scope isolato dall'istruzione in corso e risalendo sino in cima (lo scope globale).

L'accesso a una proprietà di un oggetto delega la ricerca alla relativa prototype chain dell'oggetto in memoria. Qualora la proprietà richiesta non si trovasse sull'oggetto stesso, la ricerca subirebbe un rinvio al `[[Prototype]]` nativo dell'oggetto, estrapolando dati finché la root base non restituisce `null`.

```javascript
// La ricerca SCOPE avviene negli scope lessicali annidati (la scope chain)
// La ricerca PROTOTYPE avviene nella catena dei prototipi dell'oggetto

let obj = Object.create({ ereditato: "valore prototipo" });
obj.proprio = "valore proprio";

function verifica() {
  // 'obj' è risolto tramite la SCOPE CHAIN (trovato nello scope esterno)
  // 'proprio' è risolto direttamente sull'oggetto in memoria
  console.log(obj.proprio); // "valore proprio"

  // 'obj' è sempre risolto tramite la SCOPE CHAIN
  // 'ereditato' è risolto tramite la PROTOTYPE CHAIN inerente all'oggetto
  console.log(obj.ereditato); // "valore prototipo"
}

verifica();
```

## Strumenti per la Sicurezza tra Catene

Nel contesto in cui è in analisi una catena di operandi su proprietà, è raccomandata l'adozione dell'operatore chain di tipo optional (`?.`) per evitare arresti critici del thread del browser (`TypeError`). Da notare che la validazione della scope chain non muta, perciò persisterà il fattore critico dell'eventuale ReferenceError:

```javascript
let config = { server: { host: "localhost" } };

// Optional chaining previene un TypeError (nel caso in cui 'server' non esistesse),
// restituendo 'undefined'. Tuttavia, 'config' necessita di rientrare nello scope 
// accessibile per prevenire il sollevamento di un ReferenceError.
console.log(config?.server?.port); // undefined (l'esecuzione prosegue regolarmente)
```

Tutte queste pratiche garantiscono la distinzione in fase programmatica delle architetture dell'ecosistema, separando gli scope referenziali dai flussi in memoria propri degli oggetti.
