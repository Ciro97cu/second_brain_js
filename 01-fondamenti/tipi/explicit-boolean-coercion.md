# [[../../appunti-completi#Coercizione Booleana Esplicita|Coercizione Booleana Esplicita]]

Mentre la coercizione implicita avviene in contesti condizionali per opera dell'engine JavaScript, è spesso necessario convertire **esplicitamente** un valore di qualsiasi tipo nel suo corrispondente primitivo booleano (`true` o `false`).

La coercizione esplicita migliora la leggibilità del codice, comunicando in modo inequivocabile l'intenzione di ottenere un valore logico.

## Funzione Globale Boolean()

L'approccio più dichiarativo per forzare un valore a booleano è l'utilizzo della funzione costruttrice nativa `Boolean()` (chiamata senza l'operatore `new`).

Questa funzione riceve un qualsiasi argomento e restituisce `true` per valori truthy e `false` per valori falsy.

```javascript
/*
 * Uso di Boolean() per coercizione esplicita
 */

const stringaValida = Boolean("ciao"); // true
const stringaVuota = Boolean(""); // false
const numeroZero = Boolean(0); // false
const numeroValido = Boolean(42); // true
const oggettoVuoto = Boolean({}); // true
```

## La Doppia Negazione (!!)

Un idoma estremamente comune e conciso in JavaScript sfrutta l'operatore unario di negazione logica (`!`). Il simbolo esegue una conversione implicita a booleano, ma ne inverte contestualmente il valore di verità.

Applicando una **seconda negazione**, il valore viene riportato alla sua polarità originale, ottenendo di fatto una coercizione esplicita e sicura.

```javascript
/*
 * Uso della doppia negazione !!
 */

// Passaggio logico:
// 1. !"ciao" → !true → false
// 2. !false → true

const isValido = !!"testo"; // true
const isAssente = !!""; // false
const isZero = !!0; // false
const isPopolato = !![1, 2]; // true
```

Nonostante la sintassi con `Boolean()` sia considerata da alcuni più chiara contestualmente, la notazione `!!` è adottata largamente nell'ecosistema, specialmente alla restituzione dei valori da funzioni predicato o quando si manipola lo stato in framework come React.

```javascript
function hasItems(cart) {
  // Restituisce un booleano puro, non un numero
  return !!cart.length;
}
```

## Operatori Bitwise NOT (~)

Meno utilizzato di frequente ma storicamente implementato per controlli specifici, l'operatore bitwise NOT (`~`) restituisce `-(N+1)`. Combinato con controlli come `indexOf` (che ritorna `-1` quando un elemento non viene trovato), veniva adoperato come meccanismo di coercizione per ottenere valori controllabili in un `if`.

Oggi, l'uso di questi stratagemmi è considerato superato in virtù dell'uso di costrutti più chiari come `Array.includes()` e della coercizione esplicita tramite i costrutti precedenti.
