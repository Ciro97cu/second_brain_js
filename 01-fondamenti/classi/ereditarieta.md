# [[../../appunti-completi#76-ereditarieta-di-classe-class-inheritance|Ereditarietà di Classe]]

Lo strumento maggiore alla base dell'economia programmatica orientata agli oggetti tradizionali verte sull'**Ereditarietà di classe** (Class Inheritance): in questa prospettiva, le singole forme del software operano allacciate a radici e specializzazioni comportamentali continue tra esse.

## 🎯 Da Genitore a Figlio (Metafora limitata)

Nello schema più classico si individua un assetto teorizzato che si allarga in più stadi differenziati tra l'uno e un altro stadio correlativo:

- Una entità definita di ordine superiore riceve tipicamente l'appellativo di **Classe Genitore** (parent class) poiché accerchia e distribusce ai ranghi il perno comune dei paradigmi standardizzati.
- Di risposta la porzione conseguente formante è indicata come **Classe Figlia** (child class).

> **Nota Teorica**: Nonostante i manuali informatici utilizzino pesantemente la comparativa biologica, essa tralascia meccaniche centrali del coding. Mentre i corredi parentali del mondo empirico evolvono il proprio figlio nel corso del tempo, l'istanza codificata di un blocco genitrice si esaurisce categoricamente in una singola _operazione di copia iniziale_ per generare le istanze figlie in quel frammento temporale esatto.

## 💻 Specializzazione dell'Applicativo (Override)

Costruitasi a sua immagine durante il momento della filiazione, una forma erediteriale secondaria subisce tutti gli indici valoriali dei segmenti sopra descritti ma con lo stralcio in più della specializzazione (ovverosia l'implementazione in prima persona unicamente di regole o peculiarità altrimenti sconosciuti alle origini universali).

```javascript
/* Pseudocodice illustrativo OOP Ereditario */

class Vehicle {
  engines = 1;
  drive() { output( "Driving forward!" ); }
}

class Car inherits Vehicle {
  wheels = 4;
  drive() {
    inherited:drive();  // Estrapola il format iniziale...
    output( "Completato sulle mie ", wheels, " ruote!" ); // ...Specializzandolo
  }
}
```

La `Car`, seppur attingendo palesamente ai costrutti architetturali del suo `Vehicle`, in quanto entità fisica distaccata dall'istanziazione di quest'ultimo implementa i soli costrutti e _sovrascritture_ (_override_) richiesti per il corretto moto della auto formata (come l'addizione strutturale delle quattro ruote).

## 🏷️ Tags

- #javascript
- #classi
- #oop
- #ereditarieta
- #override
