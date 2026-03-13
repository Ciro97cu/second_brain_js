# [[../../appunti-completi#variazioni-del-pattern-iife|Pattern IIFE (Indice)]]

## 📋 Panoramica delle IIFE

Il pattern delle **Immediately Invoked Function Expressions (IIFE)** consiste in funzioni che vengono eseguite nel momento esatto in cui vengono definite. Questo potente costrutto JavaScript viene utilizzato principalmente per creare scope privati, evitare l'inquinamento del namespace globale e incapsulare lo stato in maniera autonoma.

L'argomento è stato suddiviso nei seguenti concetti atomici per facilitarne la massiccia consultazione e l'aggiornamento modulare:

- [[iife-concept|Concetto Base e Forma]]: Comprendere la definizione universale delle IIFE, la differenza basilare tra forme anonime e nominate, e i vantaggi per il debugging di uno stack trace più pulito.
- [[iife-syntax-variations|Variazioni Sintattiche]]: Esplorazione degli stili di invocazione tra operatori unari e parentesi differenti.
- [[iife-arguments-passing|Passaggio di Argomenti]]: Tecniche per iniettare l'oggetto globale in contesti specifici, librerie esterne e pattern protettivi per variabili sensibili come `undefined` che prima potevano esser manipolate.
- [[iife-use-cases|Casi d'Uso Comuni]]: Esempi applicativi pratici che includono grandi blocchi di inizializzazione unici, configurazione di eventi temporanei in caricamento e forte implementazione del Module Pattern prototipo.
- [[iife-umd-pattern|Pattern UMD]]: Approfondimento del pattern storicone Universal Module Definition per la creazione nativa di codice multi-ambiente o cross-environment (Supporto Browser, Node.js e AMD Loaders contemporaneamente).

## 📉 Stato Attuale
Sebbene molte utilità centrali siano state deprecate dall'avvento degli ES6 Modules o dai Bundler che risolvono ogni forma localmente, le IIFE risultano la colonna portante di tonnellate infinite di codice legacy e script liberi tuttora mantenuti in esecuzioni libere sul Browser.

## 🔗 Concetti Correlati

- [[function-as-scope|Funzioni come Scope]] - Il principio concettuale di base delle IIFE
- [[anonymous-vs-named|Funzioni Anonime vs Nominate]] - Regole attuali di best practices
- [[module-management|Module Management]] - L'evoluzione moderna delle soluzioni implementate che risolvono le IIFE
- [[hiding-in-scope|Hiding in Scope]] - Principio generale dell'information hiding in programmazione software
- [[../../appunti-completi#variazioni-del-pattern-iife|Pattern IIFE Completo Riferimento]]

## 📚 Risorse
- "You Don't Know JS" - Volume dedicato interamente a Scope & Closures
- Documentazione base per JavaScript Design Patterns applicabili
- UMD Pattern (Universal Module Definition) implementazioni classiche

## 📌 Tag

#javascript #iife #design-patterns #scope #modules #index #closures
