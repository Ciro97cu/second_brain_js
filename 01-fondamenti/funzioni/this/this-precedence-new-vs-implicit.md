# [[../../../appunti-completi#new-vs-implicit-binding|New vs Implicit Binding]]

Il *new binding* (attivato dall'operatore `new`) rappresenta una delle regole con priorità in assoluto più alta in JavaScript e ha la precedenza totale sull'*implicit binding*.

## Esempio di Precedenza
Quando una funzione viene invocata con l'operatore `new`, viene effettivamente creato un nuovo oggetto e il parametro `this` della funzione vi punta, ignorando totalmente qualsiasi oggetto di contesto che tenterebbe di applicare invece l'*implicit binding*.

```javascript
function foo(something) {
  this.a = something;
}

var obj1 = { foo: foo };

obj1.foo(2);
console.log(obj1.a); // 2 (implicit binding applicato regolarmente)

var bar = new obj1.foo(4);
console.log(obj1.a); // 2 (non modificato)
console.log(bar.a);  // 4 (new ha creato un nuovo target-object)
```

Nonostante la sintassi di chiamata appaia formalmente come un test di *implicit binding* (`obj1.foo(...)`), la presenza della keyword `new` anteposta determina che sia la logica del nuovo costruttore a definire lo "scopo" del `this`. In tale scenario, l'oggetto originario `obj1` rimane intatto e viene iniettato un nuovo oggetto vuoto che diventerà l'effettivo `this` a cui verranno assegnate le varie proprietà modificate dal costruttore.