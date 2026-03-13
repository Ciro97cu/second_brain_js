# [[../../../appunti-completi#311-lidentificatore-this|Precedenza delle Regole di Binding]]

Quando **più di una regola** per determinare il valore di `this` potrebbe applicarsi allo stesso call-site, è fondamentale conoscere l'**ordine di precedenza** per stabilire quale avrà la meglio. 

La risoluzione si basa su una rigorosa priorità, in cui alcune invocazioni speciali prevalgono sempre su altri tipi di chiamata.

## Indice dei Concetti

Per padroneggiare in modo completo l'argomento, sono stati definiti i singoli scenari in dettaglio:

- **[[this-precedence-algorithm]]**: Spiega la gerarchia completa delle regole (dai 4 livelli di priorità) e l'algoritmo step-by-step per individuare infallibilmente il valore di `this`.
- **[[this-precedence-explicit-vs-implicit]]**: Mette a confronto le chiamate applicate come metodi contro i binding forzati esplicitamente, evidenziando il vincitore.
- **[[this-precedence-new-vs-implicit]]**: Mostra in che modo l'operazione di istanziazione surclassi i contesti nativi.
- **[[this-precedence-new-vs-hard]]**: Rivela il potenziale assoluto della keyword `new`, perfino in grado di ignorare le blindature dell'hard binding, essenziale per la *partial application*.

---

**Tags**: `#javascript` `#this` `#precedence` `#binding-rules` `#new` `#bind` `#partial-application`
