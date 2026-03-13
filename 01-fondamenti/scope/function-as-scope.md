# [[../../appunti-completi#funzioni-come-scope|Funzioni come Scope: Indice]]

Il principio generale secondo il quale avvolgere o racchiudere dei blocchi di logica all'interno di una funzione permette di creare uno scope isolato, proteggendo variabili e dichiarazioni dall'ambiente esterno globale e prevenendo collisioni.
Questa struttura raccoglie l'approfondimento di tutte le dinamiche, sintassi e pattern legati alle funzioni impiegate come delimitatori di scope.

## 📑 Argomenti e Sotto-concetti

- **[[function-scope-concept|Concetto Generale e Sintassi]]**
  Differenze tra dichiarazioni e function expressions. Approfondimento sulla mitigazione dell'inquinamento globale tramite blocchi isolati.

- **[[function-scope-naming-recursion|Gestione dei Nomi e Ricursione Interna]]**
  Uso limitato degli identificatori di funzione nelle espressioni e vantaggi per garantire sicurezza nell'esecuzione di richiami ricorsivi autonomi.

- **[[function-scope-iife-patterns|Pattern IIFE, Isolamento e Initialization]]**
  Strategie, benefici e casi d'uso concreti per l'uso immediato (Immediately Invoked Function Expressions) rivolto alle configurazioni complesse o incapsulamento rigoroso.

## 📚 Concetti Legati e Documentazione

- [[hiding-in-scope|Hiding in Scope]] - Motivazioni generali dell'information hiding tramite isolamento
- [[lexical-scope-base|Scope Lessicale Base]] - Fondamenta del paradigma
- MDN: Function Expressions and Scope
- "You Don't Know JS" - Scope & Closures chapter (Kyle Simpson)
