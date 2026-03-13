# [[../../appunti-completi#hoisting-funzioni-concetto|Concetto di Hoisting delle Funzioni]]

## Concetto Principale

Le **function declarations** in JavaScript vengono **hoisted completamente** (dichiarazione e corpo testuale inclusi). L'approccio differisce da quello adottato per le comuni variabili empiriche, laddove unicamente l'astratta dichiarazione risulta sottoposta al meccanismo di sollevamento. Questo permette formalmente la chiamata della funzione testé definita ancor prima che la medesima si rintracci fisicamente elaborando dal vertice basso del file.

Le **function expressions** subiscono un comportamento associato univocamente alle regole dell'hoisting ordinario: unicamente il costrutto variabile incassante l'assegnazione sale fino al limite estremo gerarchicocon successiva assegnazione di codice. È interdetto il sollevamento omofono dell'intero corpo implementato al suo asse interno.

## Function Declarations (Hoisted Completamente)

Le dichiarazioni di funzioni possiedono un sollevamento assoluto in testa al tracciato logico:

```javascript
// Codice scritto tipico
foo(); // "Hello!" - Funziona regolarmente

function foo() {
  console.log("Hello!");
}

// Come viene interpretato dal motore di runtime
function foo() {
  // L'intera funzione compilata assume posizione prioritaria
  console.log("Hello!");
}

foo(); // "Hello!"
```

In pre-elaborazione l'intera funzione diviene processata e reindirizzata ai ranghi superiori del relativo scope genitore.

### Hoisting in Scope Annidati

La reattività all'innalzamento si adatta e rimane circoscritta esclusivamente allo scope di derivazione:

```javascript
function outer() {
  inner(); // Invocazione valida e autorizzata

  function inner() {
    console.log("Inner function");
  }
}

outer(); 
```

## Function Expressions (Solo Variabile Hoisted)

Le function expressions ricadono sotto normative strettamente associate alle variabili: la mera dichiarazione della variabile d'appoggio sale nel costrutto gerarchico.

```javascript
// Codice inserito dal programmatore
foo(); // TypeError: foo is not a function

var foo = function () {
  console.log("Hello!");
};

// Come viene interpretato operativamente
var foo; // L'engine eleva solo la dichiarazione iniziale
foo(); // TypeError (si rileva assenza funzionale in un contenuto transitoriamente "undefined")

foo = function () {
  // L'assegnazione è persistente nella collocazione originaria prevista
  console.log("Hello!");
};
```

Qualora `foo` sorga quale istanziazione supportata da clausole ristrette `let` e `const`, le variabili giacciono entro la protettiva e nota "Temporal Dead Zone" bloccandone forzatamente qualsiasi accesso preventivo con segnale di eccezione d'istanzializzazione (tipo ReferenceError).

## Named Function Expressions

Eventuali function expressions contrassegnate formalmente da identificativo (es. named functions) applicano identico rigorismo all'identificatore globale esterno. Il nome proprio interno vige invece con operatività strettamente locale e funzionale alla medesima macroistruzione interna, oscurando tale etichetta al di fuori dei confini propri.
