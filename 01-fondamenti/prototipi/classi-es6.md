# [[../../appunti-completi#10-le-classi-in-es6-sintassi-e-insidie|Le Classi in ES6]]

L'introduzione dello standard ES6 in JavaScript ha fornito una nuova sintassi, capeggiata dalla parola chiave `class`, per ricalcare i classici linguaggi Orientati agli Oggetti. Benché alleggerisca il codice nascondendo la manipolazione esplicita dei prototipi, non si tratta di "vere" classi statiche di programmazione OOP ma continua, nei meandri del motore JS, ad affidarsi ad una fragile delegazione orizzontale.

## 🎯 Concetti Chiave

- **Zucchero Sintattico Vantaggioso**: Nasconde la meccanica grezza dello stato `.prototype`, usa comandi intuitivi come `extends` (per derivare i comportamenti) e `super()` (per polimorfismo relativo che chiama i costruttori o metodi superiori).
- **Illusione Statica**: In C++ o Java, estendere una classe e generarne un'istanza è identico a formare un calco dal cemento, in un blocco isolato perenne. In JS, la classe crea un banale ponte "in tempo reale": se il genitore subisce alterazioni future in memoria, la sua modifica muterà simultaneamente ogni figlia preesistente e futura collegata passivamente ad esso.
- **Esposizione delle Fragilità e Costanti Bug**: L'obbligo di dichiarare puramente metodi isolando i dati nel costruttore rompe violentemente la pulizia visiva non appena sorga la minima necessità di creare uno "stato condiviso" per tutte le discendenze, costringendo il codice a scavalcare l'intero blocco delle classi recuperando a vista il comando storico `Classe.prototype.datiCondivisi = 1;`.

## 💻 Esempi di Codice

### L'Equivoco dell'Ereditarietà Statica in ES6

```javascript
class C {
  rand() {
    console.log("Versione Originale");
  }
}

var c1 = new C();
c1.rand(); // "Versione Originale"

// Nessuna clonazione: JS sfrutta una delega bidirezionale!
// Modificare in un secondo momento il prototipo di C propaga l'effetto ad ogni singola istanza
C.prototype.rand = function () {
  console.log("Il virus dilaga nei figli!");
};

// Tutte le istanze storiche nate "pure" ora mutano ciecamente, rivelando di non essere mai state vere classi.
c1.rand(); // "Il virus dilaga nei figli!"
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Binding Statico di "super" pre-vincolato**: A differenza di `this`, che ricalcola dinamicamente le reti se una funzione passa a diversi oggetti, i rinvii di `super()` sono cementati alla radice esatta in cui un blocco `class` e `extends` vede la luce. Provare a rubare un costrutto o metodo da una classe per donarne la flessibilità interattiva a variazioni parallele comporterà la totale paralisi logica e non avvierà affatto la naturale successione dinamica sperata in altri casi (a meno di complesse macchinazioni manuali, tradendo ogni eleganza ricercata dal comando).
- ❌ **Sovrascrittura Involontaria**: Definire uno stato `this.identificativo = x;` nel corpo di un costruttore farà smettere bruscamente di funzionare qualsiasi metodo battezzato con lo stesso nome `identificativo() { ... }`, rimpiazzando in tutto l'interprete l'azione con un valore elementare stringa (shadowing incidentale).

## 🔗 Collegamenti

**Prerequisiti**:

- [[architettura-oloo]]
- [[limiti-design-oo]]

**Approfondimenti**:

- [[classi-vs-oggetti]]

## 📚 Riferimenti

- [You Don't Know JS: This & Object Prototypes - Appendix A](https://github.com/getify/You-Dont-Know-JS)

---

**Tags**: `#javascript` `#classi` `#es6` `#prototype` `#super`
