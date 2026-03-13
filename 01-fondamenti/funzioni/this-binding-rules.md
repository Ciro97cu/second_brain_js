# [[../../appunti-completi#311-lidentificatore-this|Le Quattro Regole del Binding di this]]

L'analisi dell'oggetto puntato dalla variabile speciale `this` procede in base a quattro regole fondamentali, valutate dal motore JavaScript nel momento in cui la funzione viene invocata (call-site). Vengono qui presentate in ordine crescente di precedenza.

## 1. Default Binding

Quando una funzione viene invocata **direttamente** senza decorazioni di sintassi, referenziazioni a oggetto o costrutti particolari, la regola di default subentra. Nel browser il target è l'ambiente globale (`window` o equivalente locale in altri environment).

```javascript
function mostraNome() {
  console.log(this.nome);
}

var nome = "Globale";
mostraNome(); // "Globale" (this = window/global)
```

In caso sia applicato il preambolo attivatore `'use strict'`, una regola restrittiva invalida la forma di autoassegnazione standard e fa ricadere `this` al valore `undefined`, lanciando `TypeError` nel caso di manipolazioni di accesso a membro.

## 2. Implicit Binding

Quando un metodo si appoggia a una **struttura** di appartenenza, l'interprete usa quell'oggetto come owner temporaneo.

```javascript
var persona = {
  nome: "Mario",
  saluta: function () {
    console.log("Ciao, sono " + this.nome);
  },
};

persona.saluta(); // "Ciao, sono Mario" (this = persona)
```

**La Perdita del Binding**: Estrarre o copiare la funzione, rompendo il riferimento all'oggetto per invocarla autonomamente, causa la perdita del binding. L'iter viene scalato alla prima regola (Default Binding):

```javascript
var saluto = persona.saluta;
saluto(); // "Ciao, sono Universale", essendo chiamata a sé.
```

## 3. Explicit Binding

Il passaggio da implicit-a-explicit introduce funzioni intrinseche del prototipo base che sovrascrivono il contesto volontariamente. Tramite `.call()` oppure `.apply()`, il `this` prende in affido rigido l'oggetto desiderato, prevaricando i vincoli passati.

```javascript
function descrivi() {
  console.log(this.tipo + ": " + this.nome);
}

var animale1 = { tipo: "Cane", nome: "Fido" };

descrivi.call(animale1); // "Cane: Fido"
```

Queste differiscono unicamente dalla lista argomenti passibile; `call(obj, ...args)`, `apply(obj, [arrayargs])`. È possibile generare e memorizzare definitivamente una function legata indissolubilmente usando la proprietà `bind()`, garantendo un hard-binding inossidabile.

```javascript
setTimeout(persona.saluta.bind(persona), 1000); // Fissato permanentemente
```

## 4. New Binding

Applicando l'operatore `new` di fronte alla chiamata di funzione, il sistema modifica l'essenza dell'inizializzazione della function:

1. Crea spontaneamente un _plain-object_ nuovo e vergine in memoria.
2. Invia tale entità collegata temporaneamente alla funzione.
3. Lo assegna all'identificatore globale del `this` interno.
4. Ritorna tale nuovo contenitore (se non è programmato altrimenti).

```javascript
function Persona(nome, eta) {
  this.nome = nome;
  this.eta = eta;
}

var p1 = new Persona("Mario", 30);
console.log(p1.nome); // "Mario" - `this` era l'oggetto vuoto restituito a p1
```

## Ordine di Precedenza

Per risolvere le ambiguità, il motore JavaScript scandisce l'istanza al call-site in questo ordine di gerarchia di autorizzazione al binding:

1. **New binding**: C'è l'interposizione di un `new`? Il this punta all'oggetto istanziato.
2. **Explicit binding**: C'è `call`, `apply` o un wrapper da `bind`? Il this punta all'oggetto esplicitato tra le parentesi.
3. **Implicit binding**: C'è un decoratore d'accesso con punto `obj.foo()`? Il this indica l'oggetto container adiacente che definisce l'intervallo operativo contestuale.
4. **Default binding**: In ogni altro evento generico residuale non ricadente nelle precedenti categorie, punta all'ambiente root globale.

## Collegamenti

- [[this-binding-intro]] - Spiegazione architettonica del this
- [[this-binding-problems]] - Smarrimento e anomalie comportamentali del this in loop e callback
- [[../oggetti/oggetti]] - Implementazione ed estensione ad alberi oggetto
