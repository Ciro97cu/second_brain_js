# [[../../appunti-completi#71-teoria-delle-classi-class-theory|Teoria delle Classi]]

Nella programmazione orientata agli oggetti (Object-Oriented, OO) i dati e il comportamento ad essi associato vengono raggruppati all'interno di un'unica struttura chiamata "classe". Essenzialmente si tratta di un pattern architetturale, di un modo di organizzare la modellazione della logica aziendale.

## 🎯 Concetti Chiave

- **Astrazione e Classificazione**: Una classe serve tipicamente per delineare un profilo astratto (es. un generico "Veicolo"). L'intento primario è evitare la duplicazione delle metodologie definenendo "schemi" comuni a tutti i tipi di discendenti.
- **Ereditarietà**: Elemento principe delle classi. In caso fosse necessario definire un'Automobile, si dichiara che essa _eredita_ i comportamenti generali della sua classe madre (veicolo), assumendone le regole basi ma espandendole con elementi unici.
- **Istanziazione**: Mentre la classe copre il ruolo dell'impianto teorico, esso va trasferito in memoria per diventare manipolabile. Questa azione, l'istanziazione, porta alla nascita del vero "Oggetto", entità popolabile con dati specifici (es. il telaio dell'automobile X).

## ⚠️ Gotcha / Errori Comuni

- ❌ **Sovrastima Architetturale**: L'essere orientati ad oggetti è unicamente uno degli innumerevoli formalismi di "design pattern" proposti nell'informatica. Non vi sono regole empiriche per dover ritenere questo paradigma fondante o universalmente corretto rispetto ad esempio alla via funzionale: l'adesione ad esso varia sulla comodità logica riscontrata nel team.

## 🔗 Collegamenti

**Approfondimenti**:

- [[classi-in-javascript]]
- [[istanziazione]]

---

**Tags**: `#javascript` `#classi` `#OO` `#pattern`
