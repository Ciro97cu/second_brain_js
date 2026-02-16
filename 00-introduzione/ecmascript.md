# ECMAScript

**Tipo**: Nuovo Topic  
**Data**: 13 Febbraio 2026

---

## Descrizione

ECMAScript è una specifica, uno standard tecnico, che definisce le regole, le funzionalità e il comportamento che un linguaggio di scripting deve avere. Non è un linguaggio di programmazione, ma la "ricetta" su cui si basano diversi linguaggi.

JavaScript è l'implementazione più famosa e diffusa dello standard ECMAScript.

## Relazione tra ECMAScript e JavaScript

La relazione tra i due si può riassumere così:

### Nascita e Standardizzazione

JavaScript fu creato da Netscape. Per evitare che ogni browser sviluppasse una propria versione incompatibile del linguaggio, fu necessario creare uno standard. Nel 1997, JavaScript fu sottomesso a Ecma International, un'organizzazione di standardizzazione, che ne formalizzò le specifiche con il nome di ECMAScript.

### Evoluzione Continua

Lo standard ECMAScript si evolve costantemente. Nuove versioni vengono rilasciate (annualmente dal 2015) per aggiungere funzionalità e migliorare il linguaggio. Una delle versioni più importanti è stata ECMAScript 2015 (ES6), che ha introdotto cambiamenti fondamentali come le classi (classes), le funzioni freccia (arrow functions) e i moduli (modules).

### Implementazioni Diverse

Sebbene JavaScript nei browser sia l'implementazione (implementation) principale, non è l'unica. Anche ambienti come Node.js (per lo sviluppo server-side) e Deno implementano lo standard ECMAScript, permettendo di usare una sintassi e funzionalità coerenti in contesti diversi dal web.

## Sintesi

In sintesi, ECMAScript definisce come il linguaggio "dovrebbe" funzionare, mentre JavaScript è il linguaggio che gli sviluppatori usano concretamente, il quale "implementa" quelle definizioni.

## Esempio

```javascript
// ES6 (2015) - Novità principali
let nome = "Mario"; // let e const
const somma = (a, b) => a + b; // arrow function

class Persona {
  // class syntax
  constructor(nome) {
    this.nome = nome;
  }
  saluta() {
    return `Ciao, sono ${this.nome}`; // template literals
  }
}

// Destructuring
const { nome: n, eta } = { nome: "Anna", eta: 30 };
```

## Collegamenti

- [[che-cose-javascript]] - JavaScript implementa ECMAScript
- [[esecuzione]] - Come il codice ECMAScript viene eseguito

## Riferimenti

- [ECMAScript Specification](https://tc39.es/ecma262/)
- [MDN - JavaScript language resources](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Language_Resources)
