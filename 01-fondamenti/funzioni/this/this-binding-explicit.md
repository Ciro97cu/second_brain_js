# [[../../../appunti-completi#Explicit Binding|Explicit Binding (Regola 3)]]

L'**explicit binding** è la regola che consente di forzare una funzione a utilizzare un oggetto specifico come contesto (`this`). Avviene richiamando metodi disponibili nativamente per tutte le funzioni, evitando modifiche strutturali all'oggetto bersaglio.

Questo argomento è stato suddiviso in concetti modulari consultabili nei seguenti approfondimenti atomici:

- **[Utilizzo di call e apply](./this-explicit-call-apply.md)**: Funzionamento di base, differenze di sintassi nell'invio dei parametri e il fenomeno del boxing automatico per i valori primitivi.
- **[Hard Binding e configurazione persistente](./this-hard-binding.md)**: Tecniche per evitare la perdita di contesto con i callback, chiusure (closures) manuali e documentazione di `Function.prototype.bind()`.
- **[Contesti API e Pattern d'uso](./this-hard-binding-utilities.md)**: Passaggio del contesto a funzioni built-in quali iteratori sugli array (`forEach`, `map`), borrowing di metodi preesistenti e manipolazione degli argomenti.

Questa separazione logica permette l'indagine mirata sui diversi approcci con cui il linguaggio consente l'assegnazione controllata e immutabile del `this`.

---

**Tags**: `#javascript` `#this` `#explicit-binding` `#call` `#apply` `#bind` `#hard-binding`
