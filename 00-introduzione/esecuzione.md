# Esecuzione

**Tipo**: Nuovo Topic  
**Data**: 13 Febbraio 2026  
**Appunti Completi**: [[../appunti-completi#14-esecuzione]]

---

## Descrizione

Per poter eseguire (to execute o run) le istruzioni, un programma deve essere tradotto in un formato che il computer possa comprendere. Questo compito è svolto da programmi speciali chiamati interpreti (interpreters) o compilatori (compilers).

## Interpretazione vs Compilazione

### Interpretazione (Interpreting)

L'interpretazione consiste nel tradurre ed eseguire il codice sorgente (source code) riga per riga, ogni volta che il programma viene avviato.

### Compilazione (Compiling)

La compilazione traduce l'intero programma in anticipo. Quando il programma viene eseguito, è la versione già compilata (in linguaggio macchina) ad essere avviata.

## JavaScript e la Compilazione JIT

Comunemente si dice che JavaScript sia un linguaggio interpretato, ma questa è un'imprecisione. Il motore JavaScript (JavaScript engine) in realtà compila (compiles) il codice "al volo" (on the fly) e poi esegue immediatamente il risultato. Questo processo è noto come **compilazione JIT (Just-In-Time)**.

## Esempio

```javascript
// Il JavaScript engine (es. V8) esegue:
// 1. PARSING - analizza il codice
// 2. COMPILAZIONE JIT - compila "al volo"
// 3. ESECUZIONE - esegue il codice compilato

function calcola(a, b) {
  return a + b;
}

let risultato = calcola(5, 3);
console.log(risultato); // 8
```

## Collegamenti

- [[programma]] - Il programma viene eseguito dal JavaScript engine
- [[sintassi/statement]] - Le istruzioni vengono compilate ed eseguite

## Riferimenti

- [V8 JavaScript Engine](https://v8.dev/)
- [MDN - JavaScript Engine](https://developer.mozilla.org/en-US/docs/Glossary/Engine/JavaScript)
