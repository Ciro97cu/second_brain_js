# [[../../../appunti-completi#311-lidentificatore-this|bind() e Hard Binding]]

A differenza di `call()` e `apply()`, il metodo nativo `bind()` non invoca la funzione immediatamente. Crea invece una **nuova funzione** con il valore di `this` permanentemente fissato ("congelato") all'oggetto specificato. Questa tecnica è nota come _Hard Binding_.

## 🎯 Concetti Chiave

- **Nuova Funzione**: Restituisce una copia della funzione originale con il binding applicato.
- **Permanente**: Il binding impostato da `bind()` non può essere sovrascritto, nemmeno usando `call()` o `apply()` successivamente.
- **Pre-configurazione**: Permette la "Partial Application", pre-impostando alcuni argomenti.

## 💻 bind() - La Sintassi

La funzione originale rimane del tutto inalterata.

**Sintassi**: `var nuovaFunzione = funzione.bind(thisArg, arg1, arg2, ...)`

```javascript
function greet() {
  console.log("Hello, " + this.name);
}

var person = { name: "Kyle" };
var boundGreet = greet.bind(person);

boundGreet(); // "Hello, Kyle"
```

### Un Binding Indistruttibile

L'hard binding è garantito. Tentativi di modificarlo avranno fallimento silente (la funzione userà il contesto originale del bind):

```javascript
function foo() {
  console.log(this.a);
}

var obj1 = { a: 2 };
var obj2 = { a: 3 };

var bar = foo.bind(obj1);
bar(); // 2

bar.call(obj2); // 2 (Il bind vince su call!)
```

## 🧠 Partial Application (Currying parziale)

`bind()` permette di "pre-caricare" non solo il contesto `this`, ma anche alcuni parametri iniziali della funzione:

```javascript
function multiply(a, b) {
  return a * b;
}

// Fissa 'this' a null, e il primo argomento 'a' a 2
var double = multiply.bind(null, 2);

console.log(double(5)); // 10 (2 * 5)
console.log(double(10)); // 20 (2 * 10)
```

## ⚠️ Gotcha

### La funzione non viene modificata sul posto

Un errore comune è chiamare `bind()` senza salvare il risultato. Poiché crea e restituisce una _nuova_ funzione, l'istruzione da sola non ha alcun effetto sulla funzione originale.

```javascript
function foo() {
  console.log(this.a);
}
var obj = { a: 2 };

foo.bind(obj); // Crea la nuova funzione ma viene "persa"
foo(); // undefined (la funzione originale non ha il binding!)

var bar = foo.bind(obj); // Utilizzo corretto
bar(); // 2
```

## 💡 Best Practices

1. **Callback sicure**: Si usa estensivamente per passare metodi di un oggetto come callback di eventi o API come `setTimeout`, altrimenti perderebbero il loro `this`.
2. **Memorizzazione**: `bind()` crea una nuova istanza della funzione in memoria ogni volta che viene chiamato. Va evitato il suo uso all'interno di render o loop ad alta frequenza per motivi di performance e garbage collection.
3. **Naming**: È utile rinominare o mantenere chiaro l'intento delle "bound functions" per facilitare il debugging.

---

**Tags**: `#javascript` `#this` `#bind` `#hard-binding` `#explicit-binding`
