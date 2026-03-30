# [[../../appunti-completi#816-riepilogo-dai-prototipi-alla-delegazione|Delegazione vs Ereditarietà]]

JavaScript implementa un meccanismo di risoluzione delle proprietà attraverso la catena del `[[Prototype]]`. Sebbene somigli all'ereditarietà (Inheritance) dei linguaggi orientati agli oggetti classici (Class-Oriented), la differenza fondamentale è che in JS **nessun oggetto né le sue proprietà vengono mai copiati**. Pertanto, il termine più corretto per definire questa relazione è **Delegazione** (Behavior Delegation).

## 🎯 Concetti Chiave

- **Il Meccanismo [[Get]]**: In assenza di una proprietà, JavaScript risale la catena dei link formata dal `[[Prototype]]` alla ricerca di una corrispondenza, fermandosi a `Object.prototype`. Un meccanismo concettualmente affine alla _Scope Chain_.
- **La Finzione dei "Costruttori"**: Chiamando una funzione col prefisso `new`, non si sta istanziando una Classe come accade ad esempio in Java o C++, ma si sta solo forzando un link fiduciario tra l'oggetto neonato e il campo `.prototype` della funzione.
- **Nessuna Copiatura**: Negli ecosistemi Class-Oriented puri, i comportamenti vengono riprodotti su ogni singola istanza in via genealogica. In JavaScript, gli oggetti sono entità paritarie che comunicano e delegano l'un l'altro solo referenziandosi per tramite di un collegamento bidirezionale, senza traslazioni o repliche di proprietà.

## ⚠️ Gotcha / Errori Comuni

- ❌ **Forzare il mentale "Model Class-Oriented" in JS**: Tentare di applicare paradigmi di ereditarietà classica, classi padre e classi figlie ad ogni costo rischia di tradursi in architetture goffe, che cercano costantemente di mascherare l'intrinseca natura a "Delegazione" del `[[Prototype]]`.
- ❌ **Sovraccarico terminologico**: L'uso frequente (benchè tollerato storicamente) delle espressioni "classi" o "ereditarietà prototipale" confonde i nuovi sviluppatori; tali etichettature precludono la piena comprensione delle differenze meccaniche di allocazione e ridondanza dei dati.

## ✅ Best Practices

- ✓ **Abbracciare l'OLOO**: Promuovere e implementare i pattern "Object Linked to Other Objects" abbracciando in modo consapevole la Behavior Delegation, slegandosi dalle dinamiche orientate prettamente al mixin classista o al polymorfismo.
- ✓ **Prediligere `Object.create()`**: Usare metodi moderni che dichiarano l'intenzione al collegamento con un delegato rispetto all'offuscante parola chiave `new` e ai presunti finti costruttori.

## 🔗 Collegamenti

**Prerequisiti** (concetti da conoscere prima):

- [[catena-prototipi]]
- [[illusione-classi]]

**Concetti Correlati**:

- [[object-links]]
- [[delegazione-interna]]

## 📚 Riferimenti

- [MDN - Object prototypes](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes)
- _You Don't Know JS_ - Cap. 5 (Review)

---

**Tags**: `#javascript` `#prototipi` `#ereditarietà` `#delegazione`
