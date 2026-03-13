# [[../../../appunti-completi#311-lidentificatore-this|Arrow Functions: Best Practices e Paradigmi]]

L'introduzione delle arrow functions impone una scelta architetturale tra il binding dinamico tradizionale e lo scoping lessicale. È fondamentale mantenere coerenza nell'approccio e seguire specifiche best practice.

## Linee Guida di Utilizzo

**Uso raccomandato delle Arrow Functions:**

1. **Callback e limitazione di scope**: Quando è necessario mantenere il `this` del contesto esterno.
2. **Event handler in classi**: Per preservare l'istanza della classe senza dover ricorrere forzatamente a `bind()`.
3. **Metodi degli array**: Per operazioni concise asincrone (`map`, `filter`, `reduce`).

**Uso NON raccomandato (da evitare):**

- Definizione di metodi di oggetti letterali (prediligere il method shorthand).
- Funzioni costruttore con operatore `new`.
- Necessità di gestire un binding dinamico basato sul call-site.
- Necessità di accedere all'oggetto implicito `arguments`.

## Scoping Lessicale vs Binding Dinamico

L'adozione delle arrow function rappresenta un vero cambio di paradigma per JavaScript: si abbandona il meccanismo dinamico in favore della closure lessicale.

### Pre-ES6 vs ES6

Il pattern storico per mantenere il contesto (`var self = this`) viene nativamente superato, benché concettualmente identico sotto un profilo meno verboso:

```javascript
// Pre-ES6 Pattern Lexical (Self)
function Timer() {
  var self = this;
  setInterval(function () {
    self.seconds++;
  }, 1000);
}

// ES6 Pattern Lexical (Arrow)
function Timer() {
  setInterval(() => {
    this.seconds++;
  }, 1000);
}
```

### Coerenza di Stile e Architetturale

Evitare categoricamente di mescolare approcci dinamici e lessicali all'interno della medesima logica architetturale di interazione del codice. È consigliabile scegliere una direzione tecnica univoca.

**Stile Orientato alla Closure (Lessicale Puro):**
Evitare del tutto le regole e il caos di `this` limitandosi all'affidamento all'ambiente e scope esterno delle funzioni.

```javascript
// La funzione non si espone e non impiega nessun this e si fonda sul Lexical Scope
function ControllerClosure(id) {
  var myId = id;
  return {
    init() {
      document.addEventListener("click", () => handleClick());
    },
  };
  function handleClick() {
    console.log("Variabile Locale: " + myId);
  }
}
```

**Stile Orientato agli Oggetti e Metodi:**
Utilizzare coerentemente l'orientamento agli oggetti e favorire il dinamismo:

```javascript
class ControllerOriented {
  id = 42;

  // Arrow function definita come field cattura 'this' istanziato
  handleClick = (evt) => {
    console.log("Valore: " + this.id);
  };

  init() {
    document.addEventListener("click", this.handleClick); // non ha bisogno di context bind() !
  }
}
```

L'uso misto di `self = this` accoppiato a funzioni standard ed arrow functions è il principale errore che conduce a codebase incomprensibili e non mantenibili.
