# [[../../../appunti-completi#311-lidentificatore-this|Gotchas ed Errori Comuni di this]]

L'uso del `this` ed il diffuso proliferare di Arrow Functions porta spesso a errori concettuali di facile raggruppamento che finiscono puntualmente su Stack Overflow o creano problemi con refactoring che mischiano class syntax a funzioni factory legacy.

## Arrow Functions come Metodi

Non usare **mai** le arrow functions come diretti metodi assegnati ad un oggetto letterale. Esse non generano implicit bindings! Non hanno proprio uno storage object a cui allineare un loro `this`.

```javascript
// ❌ SBAGLIATO
var obj = {
  value: 42,
  getValue: () => {
    console.log(this.value); // undefined! (Cattura global object letale per errore)
  },
};

obj.getValue();
```

**Correzione**: Preferisci la shorthand o la parola chiava nativa che forzano la referenza al wrapper (object) locale all'interpretazione:

```javascript
// ✅ CORRETTO
var obj = {
  value: 42,
  getValue() {
    return this.value;
  }, // Shorthand
};
```

## bind() Multipli (Over-Binding)

Imporre una concatenazione forzosa della pipeline su bind per re-instradare su un secondo istante della traccia di stato non muta la natura del bind originario primitivo:

```javascript
function foo() {
  console.log(this.a);
}

var boundContext1 = foo.bind({ a: 1 });
var boundContext2 = boundContext1.bind({ a: 2 }); // SECONDO BIND (viene totalmente ignorato silente)

boundContext2(); // 1 (Estrae la prima originaria!)
```

## Performance nei Rendering Loops Reattivi

L'innesto di un `bind(this)` che punta a stati per generare handlers negli scope dei rendering visuali di vari framework (React/Vue/ecc...) comporta penalità. Niente di bloccante, ma i loop re-istanziano e allocano in memoria anonime a profusione.

```javascript
// ❌ Sbagliato
items.forEach((item) => {
  render(<Button onClick={() => this.handleClick(item)} />); // Nuovo puntatore ad ogni micro-render
});

// ✅ Corretto (per framework moderni OOP non basati su component functional approach)
var handlersSalvati = items.map((item) => this.handleClick.bind(this, item));
// Consuma e usa references identiche di bound precalcolati
```

---

**Tags**: `#javascript` `#this` `#gotchas` `#common-errors`
