# [[../../appunti-completi#71-teoria-delle-classi-class-theory|Teoria delle Classi]]

Nella programmazione orientata agli oggetti (Object-Oriented, OO) i dati e i comportamenti associati vengono raggruppati all'interno di un'unica struttura chiamata "classe". Essenzialmente si tratta di un _pattern di design_, ovvero un modo per organizzare il codice e modellarne la logica.

## 🎯 Concetti Chiave

- **Classe (Blueprint)**: Serve a delineare un progetto base o un profilo generico (es. classe generica `Veicolo`). L'intento primario è creare regole standard per evitare di duplicare il codice in futuro.
- **Ereditarietà**: È il meccanismo tramite il quale una classe più specifica (es. `Automobile`) "copia" le basi di una classe genitore (`Veicolo`) e aggiunge o modifica i propri dettagli esclusivi.
- **Istanziazione**: È il processo pratico in cui la teoria (la classe) si trasforma in un elemento reale in memoria. Dall'istanziazione si ottiene un "Oggetto" (l'istanza), popolato coi suoi dati concreti.
- **Polimorfismo**: La capacità di un'istanza figlia di sovrascrivere (override) e personalizzare i comportamenti che ha ereditato dal genitore.

## ⚠️ Gotcha / Attenzioni

- ❌ **Sovrastima del Paradigma**: Le classi non sono la legge assoluta della programmazione. In linguaggi come Java sembrano l'unica via possibile, ma nell'informatica sono solo una delle tante scelte (come la programmazione funzionale). L'uso delle classi dipende prettamente dalle scelte del team e dalla comodità.

## 🔗 Collegamenti

**Approfondimenti**:

- [[classi-in-javascript]]
- [[istanziazione]]

---

**Tags**: `#javascript` `#classi` `#OO` `#pattern`
