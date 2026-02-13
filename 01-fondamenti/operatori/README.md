# Operatori

Gli operatori (operators) sono simboli speciali che eseguono azioni su variabili e valori: calcoli, assegnamenti, confronti e logica condizionale.

## Indice dei Topic

1. **[Assegnamento](./assegnamento.md)** - Operatori `=`, `+=`, `-=`, `*=`, `/=`, etc.
2. **[Matematici](./matematici.md)** - Operatori aritmetici: `+`, `-`, `*`, `/`, `%`, `**`, `++`, `--`
3. **[Confronto ed Uguaglianza](./confronto-uguaglianza.md)** - `===`, `==`, `!==`, `!=`, `<`, `>`, `<=`, `>=`
4. **[Logici](./logici.md)** - `&&`, `||`, `!` e short-circuit evaluation
5. **[Speciali](./speciali.md)** - Ternario `? :`, coalescenza nullish `??`, doppio NOT `!!`
6. **[Precedenza](./precedenza.md)** - Ordine di valutazione degli operatori

## Panoramica

Gli operatori permettono di manipolare e confrontare valori. Si dividono in categorie principali:

- **Assegnamento**: Memorizzano valori nelle variabili
- **Matematici**: Eseguono operazioni aritmetiche
- **Confronto**: Verificano relazioni tra valori (restituiscono booleani)
- **Logici**: Combinano condizioni booleane
- **Speciali**: Sintassi compatte per casi specifici (ternario, default, conversioni)

La precedenza determina l'ordine di valutazione. Le parentesi hanno massima priorità e rendono il codice più leggibile.

## Concetti Chiave

- **=== vs ==**: Preferire `===` (no coercizione). Usare `==` solo consapevolmente
- **Short-circuit**: `&&` e `||` si fermano appena conoscono il risultato
- **?? vs ||**: `??` ignora solo `null`/`undefined`, `||` ignora tutti i falsy
- **Oggetti/Array**: Confrontati per riferimento, non per contenuto
- **Precedenza**: Parentesi per chiarezza quando c'è ambiguità

## Percorso di Apprendimento Consigliato

1. Iniziare da **Assegnamento** per capire come memorizzare valori
2. Studiare **Matematici** per operazioni aritmetiche base
3. Approfondire **Confronto ed Uguaglianza** per la logica condizionale
4. Comprendere **Logici** per combinare condizioni
5. Esplorare **Speciali** per sintassi avanzate
6. Consultare **Precedenza** quando servono espressioni complesse

---

_Ultima modifica: 13 Febbraio 2026_
