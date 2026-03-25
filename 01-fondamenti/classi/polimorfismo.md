# [[../../appunti-completi#77-polimorfismo-polymorphism|Polimorfismo di Classe]]

Il polimorfismo è un concetto fondamentale della programmazione orientata agli oggetti che permette a un unico metodo di avere più definizioni su diversi livelli della catena di ereditarietà, e quindi di cambiare "forma" in base a chi lo fa scattare.

## 🎯 Concetti Chiave

- **Riferimento Relativo (`super`)**: Un figlio può accedere alla versione originale di un metodo del genitore tramite la parola chiave `super` (es. `super.drive()`). In questo modo può eseguire le istruzioni di base per poi aggiungerne di nuove per specializzarsi.
- **Risoluzione Automatica**: Se un metodo originario del genitore invoca a sua volta una funzione generica, ma il figlio ha già effettuato l'override con la propria versione, il linguaggio fa scattare automaticamente il comportamento del figlio invece di quello ereditato.
- **L'Illusione del Cordone Ombelicale**: L'utilizzo ricorrente del polimorfismo dà l'impressione che la classe figlia rimanga perennemente collegata al genitore originale in esplorazione. Nei linguaggi di classe questo è falso: la classe archivia copie fisiche del metodo genitore, conservandole incapsulate parallelamente alle proprie pronte all'uso.

## 💻 Esempi di Codice

### Esempio Concettuale (`super`)

```javascript
/* Pseudocodice per indicare l'uso del polimorfismo */

class Parent {
  speak() {
    output("Hello!");
  }
}

class Child inherits Parent {
  speak() {
    super.speak(); // Polimorfismo: Accesso al metodo originale
    output("How are you?");
  }
}
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Confondere `super` in JS con altri linguaggi**: In vari linguaggi, `super` accede staticamente a una classe. In JS (che usa prototipi sotto il cofano), le logiche di polimorfismo nascondono un collegamento dinamico, creando confusione nel tracking di esecuzione.

## ✅ Best Practices

- ✓ **Incapsulamento**: Sfruttare il polimorfismo per mantenere la logica base al sicuro (nella classe principale) ed espandere le varianti localmente solo nei singoli figli, senza intaccare gli altri.

## 🔗 Collegamenti

**Prerequisiti**:

- [[ereditarieta|Ereditarietà di Classe]]

**Approfondimenti**:

- [[ereditarieta-multipla|Ereditarietà Multipla]]

## 📚 Riferimenti

- [MDN - super](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/super)

## 📌 Note Personali

---

**Tags**: `#javascript` `#classi` `#oop` `#polimorfismo` `#ereditarieta`
