# [[../../appunti-completi#75-costruttore-constructor|Costruttore di Classe]]

Il Costruttore (Constructor) è il metodo speciale invocato nel momento in cui una classe viene istanziata per creare un oggetto.

## 🎯 Concetti Chiave

- **Obiettivo**: L'obiettivo esplicito di questo metodo è inizializzare le informazioni (lo stato o i dati) di base che la nuova istanza userà da lì in avanti per funzionare.
- **Appartenenza**: Appartiene alla propria classe originaria.
- **Denominazione**: Spesso ha esattamente lo stesso nome della classe stessa.
- **Creazione dell'Oggetto**: Il risultato della chiamata al costruttore è la restituzione da parte del sistema di un nuovo oggetto reale (una copia indipendente della logica di classe), nel quale i dati sono già stati popolati.

## 💻 Esempi di Codice

### Esempio Base

```javascript
/* Pseudocodice per illustrare il concetto delle classi agli oggetti classici */

class CoolGuy {
  // Variabile interna
  specialTrick = nothing;

  // Metodo Costruttore
  CoolGuy(trick) {
    specialTrick = trick;
  }
}

// Chiamata esplicita per costruire una nuova istanza (evocare l'istanza)
let Joe = new CoolGuy("jumping rope");
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Dimenticare l'istanziazione**: In alcuni linguaggi o pattern la mancata chiamata tramite la keyword prevista porta ad errori di contesto (riferimento errato a variabili non ancora copiate).

## ✅ Best Practices

- ✓ **Inizializzazione completa**: Assicurarsi di impostare tutte le proprietà necessarie per lo stato iniziale dell'oggetto direttamente nel corpo del costruttore.

## 🔗 Collegamenti

**Prerequisiti**:

- [[teoria-classi|Teoria delle Classi]]

**Concetti Correlati**:

- [[istanziazione|Istanziazione come Operazione di Copia]]

**Approfondimenti**:

- [[ereditarieta|Ereditarietà di Classe]]

## 📚 Riferimenti

- [MDN - Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)

## 📌 Note Personali

---

**Tags**: `#javascript` `#classi` `#oop` `#costruttore` `#istanza`
