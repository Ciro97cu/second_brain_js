# [[../../appunti-completi#96-modelli-mentali-a-confronto-oo-vs-oloo|Modelli Mentali a Confronto (OO vs OLOO)]]

Il confronto fra il costrutto classico orientato agli oggetti fittizio (OO) e il costrutto nativo a delegazione (OLOO) in JavaScript evidenzia una profonda discrepanza nell'infrastruttura necessaria per ottenere il medesimo risultato funzionale. Lo stile a classi richiede un bagaglio mentale opprimente, in netto contrasto con l'estrema pulizia formale e relazionale.

## 🎯 Concetti Chiave

- **Burocrazia vs Pulizia**: Sebbene sia nel pattern OO sia nell'OLOO lo scopo ultimo sia interconnettere oggetti (es. un oggetto delegatore che preleva da uno delegato), il primo impone di impantanarsi costantemente con keyword `.prototype`, ricalibrazione del `.constructor` e l'uso offuscato di `new`.
- **La Ragnatela Mentale**: Costruire finte classi in JS richiede allo sviluppatore l'assimilazione tacita di una fitta rete di referenziazioni intrinseche secondarie generate forzatamente dal motore (legami incrociati costruttore/prototipo).
- **Trasparenza Relazionale**: Nello stile OLOO gli unici link generati sono quelli intenzionali programmati via `Object.create()`. L'assenza di finti genitori neutralizza le diramazioni accessorie.

## ⚠️ Gotcha / Errori Comuni

- ❌ **Equiparare la verbosità alle funzionalità**: Trattare la sintassi per estesa `Class-Oriented` come intrinsecamente più "capace" o "potente". Adottare OLOO snellisce il codice e la ragnatela mentale senza perdere alcuna flessibilità tecnica.

## ✅ Best Practices

- ✓ **Minimizzare il debito cognitivo**: Laddove sia possibile ottenere interazioni, recuperi dati e stampe perfettamente aderenti ad una catena, l'architettura che non richiede di padroneggiare costumi pretenziosi (ossia la delegazione OLOO) vince oggettivamente per chiarezza espositiva nel mantenimento a lungo termine del software.

## 🔗 Collegamenti

**Prerequisiti** (concetti da conoscere prima):

- [[pattern-oloo]]
- [[behavior-delegation]]

**Concetti Correlati**:

- [[illusione-classi]]
- [[ereditarieta-prototipale-delega]]

## 📚 Riferimenti

- _You Don't Know JS_ - Cap. 6 (Behavior Delegation - Mental Models Compared)

---

**Tags**: `#javascript` `#prototipi` `#design-pattern` `#confronto` `#oloo`
