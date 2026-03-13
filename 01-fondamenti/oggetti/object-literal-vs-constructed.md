# [[../../appunti-completi#sintassi-degli-oggetti|Oggetti: Forma Letterale vs Forma Costruita]]

L'instanziazione degli oggetti in JavaScript può avvenire tramite due tecniche e sintassi fondamentali. Da una parte è prevista la **forma letterale** (object literal), mentre dall'altra è utilizzata la **forma costruita** (constructed form). La scelta tra le due ha implicazioni profonde su leggibilità, praticità e standard di codebase moderne.

## Punti Chiave

La decisione pratica e sintattica impone l'adozione di due sintassi opposte:

- **Forma letterale**: Una dichiarazione gerarchica concisa a parentesi `{ key: value }`. Definisce le proprietà, inclusi array o funzioni e li incapsula nell'espressione stessa, a beneficio della logica.
- **Forma costruita**: Sfrutta istruzioni dirette al motore JS come `new Object()` a cui vengono iniettate progressivamente le proprietà, riga dopo riga con identificatori concatenati.

Il **risultato identico**: Entrambe producono lo stesso tipo di oggetto, conservano le medesime capacità e referenziano l'indirizzo esatto; è però la forma e lo statement che si distinguono.

## Linee Guida Pratiche

| Scenario                                        | Forma Raccomandata | Motivo                                   |
| ----------------------------------------------- | ------------------ | ---------------------------------------- |
| Oggetto con struttura nota                      | **Letterale**      | Leggibilità immediata                    |
| Conversione oggetti in testuale                 | **Letterale**      | Compatibilità con API JSON               |
| Creazione con proprietà calcolate               | **Letterale**      | Supporto inline per chiavi dinamiche     |
| Configurazione, opzioni e attributi             | **Letterale**      | Best-practice di settore                 |
| Costruzione condizionale molto complessa        | Costruita          | Chiarezza logica in casi limitati        |
| Spiegazione incrementale dello stato object     | Costruita          | Evidenziazione tecnica progressiva       |

La best practice impone lo standard letterale:
 Quasi nessuno sviluppatore utilizza il costruttore principale puro nel codice moderno. La forma letterale supporta sintassi ES6+ (come proprietà calcolate e spread operator). Si attesta l'assenza di limitazioni prestazionali della sintassi a parentesi contro la concatenazione classica nei moderni JavaScript execution engines, spingendo la standardizzazione verso la forma letterale (`{}`).

## Collegamenti alle Specifiche

Da questo indice, è possibile approfondire i concetti nei seguenti nodi indipendenti:

- [[object-literals]] - Analisi approfondita e vantaggi della dichiarazione letterale
- [[constructed-objects]] - Tecniche e casi d'uso (rari) di `new Object()`
- [[oggetti]] - L'introduzione generale e manipolazione delle strutture a oggetto
- [[../tipi/tipi-e-sottotipi]] - Tipi di base e differenze nel sistema

#oggetti #sintassi #best-practices #literal-form #constructed-form #object-creation
