# [[../../appunti-completi#funzioni-come-scope|Funzione come Scope: Nomi e Ricorsi]]

## 💡 Nome della Funzione: Posizione e Accessibilità

La gestione e l'accesso al nome della funzione cambiano in modo significativo tra le dichiarazioni e le espressioni di funzione.

### Nelle Dichiarazioni

Nelle dichiarazioni, il nome della funzione è reso accessibile nello scope esterno in cui la funzione viene definita.

```javascript
function nomeDichiarazione() {
  /* ... */
}
console.log(nomeDichiarazione.name); // Accessibile e visibile esternamente
```

### Nelle Espressioni

Nelle espressioni di funzione (in particolare nelle *named function expressions*, ovvero le espressioni denominate), il nome della funzione risulta inaccessibile dall'esterno. Tale identificatore viene limitato al solo scope interno della funzione stessa.

```javascript
var varEsterna = function nomeEspressione() {
  // 'nomeEspressione' accessibile SOLO qui dentro
  console.log(nomeEspressione.name);
};

console.log(varEsterna.name); // "nomeEspressione" (accessibile tramite la variabile)
// console.log(nomeEspressione); // ReferenceError (NON presente nello scope esterno!)
```

## 🔄 Ricorsione con Nome Privato

Un vantaggio fondamentale dell'utilizzo di espressioni di funzione denominate risiede nella sicurezza offerta durante operazioni per chiamate a se stessa, come la ricorsione. Ciò garantisce un riferimento affidabile alla funzione, immune da alterazioni esterne.

```javascript
var fattoriale = function fatto(n) {
  if (n <= 1) return 1;
  return n * fatto(n - 1); // Riferimento sicuro a 'fatto' internamente
};

fattoriale(5); // 120
// fatto(5); // ReferenceError se chiamato dall'esterno

// La ricorsione opera correttamente anche in caso di riassegnazione
var temp = fattoriale;
fattoriale = null; // Il riferimento esterno viene perso/distrutto
temp(5); // 120 - internamente la funzione usa ancora 'fatto'!
```

Questo approccio previene le anomalie legate all'eliminazione o modifica di variabili esterne che fanno da puntatori alla funzione e mantiene incapsulato e consistente il riferimento per la logica ricorsiva.

## 🔗 Riferimenti

- [[function-scope-concept|Funzione come Scope: Concetti]]
- [[lexical-scope-base|Scope Lessicale]]

## 📌 Tag

#javascript #scope #function-expressions #recursion #named-functions #privacy
