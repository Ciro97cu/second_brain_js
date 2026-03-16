# [[../../appunti-completi#76-ereditarieta-di-classe-class-inheritance|Ereditarietà di Classe]]

Lo strumento maggiore alla base della programmazione orientata agli oggetti è l'**Ereditarietà** (Class Inheritance): permette alle classi di operare collegate tra loro condividendo schemi e comportamenti base.

## 🎯 Da Genitore a Figlio (Metafora limitata)

Nello schema più classico si individuano due ruoli chiave:

- **Classe Genitore** (parent class): definisce le regole e i comportamenti generali (es. un generico _Veicolo_).
- **Classe Figlia** (child class): si appoggia al genitore copiandone inizialmente tutte le basi per poi specializzarsi.

> **Nota Teorica**: I manuali informatici usano la comparativa biologica (padre e figlio) che può confondere. Nel mondo della programmazione, la classe figlia acquisisce una singola forte **copia iniziale** delle capacità in quel momento esatto dal genitore, per poi vivere come elemento autonomo e slegato nella successiva esecuzione in memoria.

## 💻 Specializzazione (Override)

Dopo aver copiato la forma della genitrice, la forma ereditaria seconda subisce l'azione della **specializzazione**: si possono definire regole esclusive estranee al genitore o _sovrascrivere_ (_override_) un comportamento ereditato per adattarlo al meglio.

```javascript
/* Pseudocodice illustrativo OOP Ereditario */

class Vehicle {
  engines = 1;
  drive() { output( "Driving forward!" ); }
}

class Car inherits Vehicle {
  wheels = 4; // Specializzazione (Regola estranea al genitore)
  drive() {
    inherited:drive();  // Estrapola il format iniziale copiato...
    output( "Completato sulle mie ", wheels, " ruote!" ); // ...e lo sovrascrive (override)
  }
}
```

La `Car`, attingendo all'architettura generica del suo `Vehicle`, implementa solo quelle sovrascritture (_override_) esclusive necessarie per renderla un'auto reale, come l'aggiunta strutturale di quattro ruote o un tipo diverso di guida.

## 🏷️ Tags

- #javascript
- #classi
- #oop
- #ereditarieta
- #override
