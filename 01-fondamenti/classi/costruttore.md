# [[../../appunti-completi#75-costruttore-constructor|Costruttore di Classe]]

Il Costruttore (Constructor) costituisce il metodo primario invocato durante l'istanziazione di una classe in un linguaggio orientato agli oggetti tradizionale.

## 🎯 Il Compito del Costruttore

L'obiettivo esplicito di questo metodo è **inizializzare tutte le informazioni** (statistiche o strutturali) di cui l'istanza generata ha bisogno per mettersi ad operare in autonomia.

Il metodo costruttore:

- Appartiene strettamente alla propria classe genitrice
- Adotta quasi universalmente lo stesso nome nominale della propria classe (o una direttiva specializzata in base al linguaggio)

## 💻 Evocare l'Istanza

Affinché l'Engine interpreti la creazione di un'istanza formale, si è soliti chiamare il construct method per mezzo della keyword `new`:

```javascript
/* Pseudocodice per illustrare il concetto delle classi a ogggetti classici */

class CoolGuy {
  // Dichiarazione parametro
  specialTrick = nothing;

  // Constructor method
  CoolGuy(trick) {
    specialTrick = trick;
  }
}

// Chiamata esplicita in istanziazione
let Joe = new CoolGuy("jumping rope");
```

Il ritorno ottenuto da tale esecuzione si poggia in una pura _copia viva_ della logica classata, popolata da elementi definiti nel blocco del costruttore.

## 🏷️ Tags

- #javascript
- #classi
- #oop
- #costruttore
- #istanza
