# [[../../appunti-completi#310-il-pattern-modulo-modules|Module Pattern]]

Il Module Pattern è storico approccio in JavaScript per creare un livello di incapsulamento prima dell'avvento dei moduli ES6 nativi. Si basa sull'utilizzo delle closure per mantenere uno stato privato inaccessibile dall'esterno, esponendo solo un'interfaccia pubblica (API).

## Concetti del Module Pattern

Il pattern sfrutta le funzioni (Spesso IIFE) come isolatori di scope. I diversi aspetti e configurazioni del Modulo sono stati suddivisi in approfondimenti specifici:

- **Concetti Base**: requisiti necessari per definire un vero modulo tramite closure. Vedi [[module-pattern-concept|Module Pattern Concept]].
- **La struttura canonica**: come i dati privati vengono incapsulati e resi disponibili tramite oggetti. Vedi [[revealing-module-pattern|Revealing Module Pattern]].
- **Istanza Singola**: creazione di moduli statici, non instanziabili più volte. Vedi [[singleton-module-pattern|Singleton Module Pattern]].
- **Configurazioni e Dinamicità**: passaggio di argomenti al modulo e modifica dell'API in tempo reale. Vedi [[module-pattern-variants|Module Pattern Variants]].

Oggi le logiche del Module Pattern sono in gran parte automatizzate o sostituite dai moduli in formato ES6 (import / export).
