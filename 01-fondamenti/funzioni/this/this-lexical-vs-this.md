# [[../../../appunti-completi#confusione-2-this-come-riferimento-allo-scope-lessicale|This vs Scope Lessicale]]

Cercare di usare `this` per attraversare o unire gli scope lessicali è un errore fondamentale perché si tratta di due meccanismi completamente separati in JavaScript. Non esiste alcun ponte tra il lookup lessicale e il binding di `this`.

## ⚠️ Perché NON Esiste il Ponte

### Scope Lessicale: Meccanismo 1

```javascript
function outer() {
  var x = 10;

  function inner() {
    console.log(x); // Accesso lessicale - funziona ✅
  }

  inner();
}
```

**Caratteristiche**:

- Determinato **al momento della scrittura** (author-time).
- Lookup basato su closure e scope esterno.
- Accesso via **identificatori** (nomi di variabili).
- Risolto tramite una chain di scope (`[[Scope]]` interno).

### this Binding: Meccanismo 2

```javascript
function foo() {
  console.log(this.value);
}

var obj = { value: 42, foo: foo };

obj.foo(); // Binding di this - funziona ✅
```

**Caratteristiche**:

- Determinato **al momento della chiamata** (call-time).
- Punta a un oggetto in base al call-site.
- Accesso via **proprietà** dell'oggetto.
- Regole di binding specifiche (default, implicit, explicit, new).

### I Due Meccanismi Sono Separati

Un singolo frammento di codice può utilizzare entrambi i meccanismi, ma essi non interagiscono tra loro:

```javascript
function outer() {
  var x = 10;

  return function inner() {
    // Lexical scope: accede a 'x' ✅
    console.log(x);

    // this binding: accede a proprietà di 'this' ✅
    console.log(this.value);

    // Non si può usare 'this' per accedere a 'x' ❌
    // console.log(this.x); // undefined
  };
}

var obj = {
  value: 42,
  fn: outer(),
};

obj.fn(); // Stampa prima 10, poi 42
```

## 📊 Confronto Meccanismi

| Feature         | Lexical Scope            | this Binding              |
| :-------------- | :----------------------- | :------------------------ |
| Determinato     | Author-time (scrittura)  | Call-time (esecuzione)    |
| Accede a        | Variabili locali/esterne | Proprietà di oggetti      |
| Sintassi        | Identificatore (`x`)     | Membro (`this.x`)         |
| Meccanismo      | Closure, scope chain     | Call-site, regole binding |
| Modificabile    | No (fisso)               | Sì (call/apply/bind)      |
| Ponte tra i due | **NON ESISTE**           | **NON ESISTE**            |
