# [[../../../appunti-completi#311-lidentificatore-this|New Binding: Comportamento del Return]]

Quando si istanzia un oggetto tramite una constructor call con `new`, il comportamento della parola chiave `return` all'interno della funzione cambia rispetto a un'invocazione standard.

## Return Implicito (Normale)

In assenza di un'istruzione `return`, viene ritornato automaticamente il nuovo oggetto creato dai passaggi iniziali dell'operatore `new`.

```javascript
function Foo(name) {
  this.name = name;
  // Nessun return esplicito
}

var obj = new Foo("test");
console.log(obj.name); // "test" (obj è il nuovo oggetto)
```

## Return Esplicito di Oggetto

Se viene ritornato manualmente un **oggetto** qualsiasi (incluso un array o una funzione), questo valore sovrascrive l'oggetto creato automaticamente dal `new`. L'oggetto originariamente creato viene scartato.

```javascript
function Foo() {
  this.name = "foo";

  // Return esplicito di un nuovo oggetto
  return {
    name: "bar",
  };
}

var obj = new Foo();
console.log(obj.name); // "bar" (l'oggetto restituito esplicitamente ha la precedenza)
```

## Return di Valore Primitivo

Se invece si tenta di ritornare un valore **primitivo** (come una stringa, un numero o un booleano), tale valore viene silenziosamente ignorato e la funzione si limita a ritornare l'oggetto creato inizialmente dal `new`.

```javascript
function Foo(name) {
  this.name = name;

  return 42; // Un valore primitivo viene ignorato
}

var obj = new Foo("test");
console.log(obj.name); // "test" (ritorno regolare del nuovo oggetto)
console.log(obj); // { name: "test" } (non 42)
```

La regola generale stabilisce che solamente il ritorno esplicito di un oggetto è in grado di sovrascrivere il normale comportamento e l'esito finale dell'operatore `new`.
