# [[../../../appunti-completi#311-lidentificatore-this|New Binding (Regola 4)]]

Quando una funzione viene invocata con `new` davanti, viene chiamata **constructor call**. In questo caso, `this` viene impostato a un nuovo oggetto creato appositamente per questa istanziazione. Questo meccanismo rappresenta la quarta regola (o pattern) del binding di `this` in JavaScript.

Gli argomenti legati al *New Binding* sono stati suddivisi in moduli per facilitarne la consultazione:

- **[[this-new-algorithm]]**: Dettaglia i quattro passaggi segreti messi in moto dall'operatore `new` (creazione dell'oggetto, linking del prototipo, binding di this e return).
- **[[this-new-return-values]]**: Illustra le particolarità che subentrano nel restiture un oggetto esplicito piuttosto che un valore primitivo all'interno del costruttore.
- **[[this-new-patterns]]**: Analizza le convenzioni comuni adottate nella comunità per i costruttori, come la regola del PascalCase, l'uso del prototype per ottimizzare la memoria e vari accorgimenti.
- **[[this-new-gotchas]]**: Espone i tipici errori e bug che si possono verificare nell'invocazione di un costruttore, evidenziando limitazioni strutturali e problemi con le Arrow Functions.
- **[[this-new-vs-classes]]**: Raffronta in maniera sintetica la costruzione d'oggetti nel contesto "storico" di JavaScript rispetto ai paradigmi basati sulla sintassi formale a `class` di ES6.

## 🔗 Riferimenti

- **You Don't Know JS**: this & Object Prototypes - Chapter 2
- **MDN**: [new operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new)
- **MDN**: [instanceof](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/instanceof)
- **MDN**: [Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)

---

**Tags**: `#javascript` `#this` `#new-binding` `#constructor` `#new-operator` `#class`
