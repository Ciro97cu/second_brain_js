# [[../../appunti-completi#77-polimorfismo-polymorphism|Polimorfismo di Classe]]

Il polimorfismo è un concetto fondamentale della programmazione orientata agli oggetti che permette a un unico metodo di avere più definizioni su diversi livelli della catena di ereditarietà, e quindi di cambiare "forma" in base a chi lo fa scattare.

## 🎯 Concetti Chiave

- **Riferimento Relativo (`super`)**: Un figlio può accedere alla versione originale di un metodo del padre usando la parola chiave strutturale `super` (es. `super.drive()`). In questo modo esegue la base e poi può aggiungere le proprie specifiche comodamente.
- **Risoluzione Automatica**: Se un figlio usa un metodo del padre che al suo interno richiama una funzione generica, ma il figlio ha una propria versione di quella specifica funzione, il linguaggio lo capirà in automatico. Il motore non cade nell'errore di usare la funzione del padre, ma avvia sempre il comportamento corretto personalizzato in base alla classe a cui appartiene l'istanza.
- **L'Illusione del Cordone Ombelicale**: Richiamare un metodo genitore dà l'impressione che la classe figlia sia sempre costantemente collegata al suo progenitore. Questo è falso: l'ereditarietà in questi linguaggi significa esclusivamente **effettuare copie**. Quando un figlio fa _override_, conserva semplicemente nei propri archivi sia la propria esecuzione modificata sia la copia incapsulata del metodo originale per potervi attingere in futuro.

## 🔗 Collegamenti

**Prerequisiti**:

- [[ereditarieta]]

---

**Tags**: `#javascript` `#classi` `#oop` `#polimorfismo` `#ereditarieta`
