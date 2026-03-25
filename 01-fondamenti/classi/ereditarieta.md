# [[../../appunti-completi#76-ereditarieta-di-classe-class-inheritance|Ereditarietà di Classe]]

Lo strumento maggiore alla base della programmazione orientata agli oggetti è l'**Ereditarietà** (Class Inheritance): permette alle classi di operare collegate tra loro condividendo schemi e comportamenti base.

## 🎯 Concetti Chiave

- **Classe Genitore (parent class)**: Definisce le regole e i comportamenti generali (es. un generico "Veicolo").
- **Classe Figlia (child class)**: Si appoggia al genitore copiandone inizialmente tutte le basi per poi specializzarsi.
- **La metafora biologica è limitata**: Nei linguaggi di programmazione classici, la classe figlia acquisisce una singola e forte _copia iniziale_ delle capacità genitoriali in un preciso momento, per poi vivere come elemento autonomo e slegato nella successiva esecuzione in memoria.
- **Specializzazione (Override)**: La classe figlia può definire regole esclusive o _sovrascrivere_ un comportamento ereditato per adattarlo al meglio rispetto all'archetipo del genitore.

## 💻 Esempi di Codice

### Esempio Base

```javascript
/* Pseudocodice illustrativo OOP Ereditario */

class Vehicle {
  engines = 1;

  drive() {
    output( "Driving forward!" );
  }
}

class Car inherits Vehicle {
  wheels = 4; // Specializzazione (Regola estranea al genitore)

  drive() {
    inherited:drive();  // Estrapola il format iniziale copiato...
    output( "Completato sulle mie ", wheels, " ruote!" ); // ...e lo sovrascrive (override)
  }
}
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Collegamento in tempo reale**: È un errore comune credere che genitore e figlio siano dinamicamente collegati a runtime (nei linguaggi class-oriented). Questo modello effettua invece una copia dura e permanente.

## ✅ Best Practices

- ✓ **Generalizzazione corretta**: Mantenere nella classe genitore solo le proprietà universali condivise da tutti i futuri componenti della gerarchia.

## 🔗 Collegamenti

**Prerequisiti**:

- [[costruttore|Costruttore di Classe]]

**Approfondimenti**:

- [[polimorfismo|Polimorfismo di Classe]]
- [[ereditarieta-multipla|Ereditarietà Multipla]]

## 📚 Riferimenti

- [MDN - Class Inheritance](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes#sub_classing_with_extends)

## 📌 Note Personali

---

**Tags**: `#javascript` `#classi` `#oop` `#ereditarieta` `#override`
