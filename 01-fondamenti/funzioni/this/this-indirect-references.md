# [[../../../appunti-completi#311-lidentificatore-this|Riferimenti Indiretti di this]]

Un'altra situazione che causa l'applicazione inattesa del **default binding** è la creazione, intenzionale o accidentale, di **riferimenti indiretti** alle funzioni. Questo avviene tipicamente durante delle catene di assegnazioni.

## Il Problema dell'Assegnazione

Un'assegnazione restituisce sempre un reference che fa capo al valore assegnato in fondo alla riga. Se il valore ritornato è un metodo di oggetto, l'espressione restituisce l'oggetto funzione "nudo" perdendo la parentela.

```javascript
function foo() {
  console.log(this.a);
}

var a = 2; // Variabile globale (in non-strict mode)
var o = { a: 3, foo: foo };
var p = { a: 4 };

o.foo(); // 3 (implicit binding regolare)

// Assegnazione ed esecuzione immediata concatenata
(p.foo = o.foo)(); // 2 (default binding!)
```

## Perché Succede?

L'espressione nel caso soprastante `p.foo = o.foo` valuta come suo output di ritorno finale la function reference ad esso riferito, originaria come `foo` in anonimato. 

Aggiungendo l'operatore parentesi `()` per invocarla si forza il calcolo alla base dell'oggetto, ed il vero callsite per interpretare il `this` diventerà l'esecuzione globale della funzione, non `p.foo()` né `o.foo()`.

La funzione subisce così un **default binding** naturale, finendo agganciata al modulo o allo scope globale di window in base al motore ed eventuale strict flag. Rispettate la massima attenzione ad evitare i ritorni impliciti concatenati nel code di produzione per evitare comportamenti incomprensibili per la view.

---

**Tags**: `#javascript` `#this` `#indirect-references` `#scoping` `#default-binding`
