# [[../../appunti-completi#75-costruttore-constructor|Costruttore di Classe]]

Il Costruttore (Constructor) è il metodo speciale invocato nel momento in cui una classe viene istanziata per creare un oggetto.

## 🎯 Il Compito del Costruttore

L'obiettivo esplicito di questo metodo è **inizializzare le informazioni** (lo stato o i dati) di base che la nuova istanza userà da lì in avanti per funzionare.

Il metodo costruttore:

- Appartiene alla propria classe originaria.
- Spesso ha esattamente lo stesso nome della classe stessa.

## 💻 Evocare l'Istanza

Per avvisare l'Engine (il motore che esegue il codice) che si desidera creare un'istanza fisica partendo dalla classe, il costruttore viene chiamato usando la parola chiave `new`:

```javascript
/* Pseudocodice per illustrare il concetto delle classi agli ogggetti classici */

class CoolGuy {
  // Variabile interna
  specialTrick = nothing;

  // Metodo Costruttore
  CoolGuy(trick) {
    specialTrick = trick;
  }
}

// Chiamata esplicita per costruire una nuova istanza
let Joe = new CoolGuy("jumping rope");
```

Il risultato di questa chiamata è che il sistema restituisce un **nuovo oggetto** reale (una copia indipendente della logica di classe), nel quale i dati sono già stati popolati secondo quanto scritto nel blocco del costruttore.

## 🏷️ Tags

- #javascript
- #classi
- #oop
- #costruttore
- #istanza
