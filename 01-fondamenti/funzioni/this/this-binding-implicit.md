# [[../../../appunti-completi#311-lidentificatore-this|Implicit Binding (Regola 2)]]

L'**implicit binding** è la seconda regola in ordine di importanza per determinare il valore di `this` in JavaScript. Si verifica quando una funzione viene chiamata in quanto metodo appartenente a un oggetto. Durante tale invocazione, l'oggetto contenitore (definito come contesto d'esecuzione del call-site) assume automaticamente il ruolo del valore `this`.

Il principio essenziale dietro all'implicit binding si basa sull'individuazione del possessore momentaneo del contesto.

## Il Call-Site e l'Oggetto Contenitore

Quando un blocco funzionale viene invocato tramite l'accesso alle proprietà di un oggetto (es. `obj.foo()`), la regola impone che l'oggetto che precede il punto diventi il contesto di riferimento `this`.

```javascript
function foo() {
  console.log(this.a);
}

const obj = {
  a: 2,
  foo: foo,
};

// Qui obj assegna implicitamente il proprio target
obj.foo(); // 2 (this risulta essere obj)
```

Anche nel caso in cui `foo` sia dichiarata esternamente all'oggetto associato, JavaScript valuta il suo richiamo in funzione del **call-site**.

## Riferimenti Privi di Possesso

Un fraintendimento comune è ritenere che la funzione diventi "proprietà esclusiva" dell'oggetto in questione. In realtà, l'oggetto `obj` contiene unicamente un riferimento (reference link) allo spazio di memoria della funzione `foo`.

```javascript
function foo() {
  console.log(this.a);
}

// L'esistenza della funzione risulta essere ancora globale
console.log(typeof foo); // "function"

const obj = {
  a: 2,
  foo: foo, // Un semplice riferimento assegnato sulla base delle propriety dell'oggetto!
};

foo(); // undefined (oppure errore in strict mode in quanto non vi è implicit binding)
obj.foo(); // 2 (entra in gioco l'implicit binding per quest'ultimo)
```

In scenari più complessi con chiamate nidificate ad attori multipli, diviene fondamentale capire l'esclusiva valenza e il comportamento esibito da [[this-implicit-chain|catene di oggetti]].

## Fenomeni Degenerativi e Forzature

Data la volatilità dell'implicit binding, quest'ultimo soffre della propensione di peridersi in determinate circostanze causate da:

- Assegnazione dei riferimenti e passaggio tramite funzione ([[this-implicit-lost|Implicitly Lost: Perdita del Contesto]])
- Impiego nei timer e passaggi di Callback a manipolatori di librerie ([["Implicitly Lost" rispetto a Problemi Relativi|this-binding-problems]])
- Manipolazioni Forzate da parte del DOM e degli [[this-implicit-event-handlers|Event Handlers]].

Questi frangenti trasformano invariabilmente un richiamo referenziato (simile al metodo di oggetto) in esecuzione standard che adotta la [[this-binding-default|Default Binding (Regola 1)]]. Lavorando in modo impreciso e tralasciando queste sfumature strutturali della "Perdita del contesto" e della "Forzatura negli eventi DOM" ci si espone ad esecuti irrimediabilmente guasti e inaffidabili.

## Precedenza

Tale binding si colloca come più forte rispetto al default puro, ma risulta essenzialmente vulnerabile quando conteso da forzature causate dai richiami di Explicit, Hard, e New bindings (vedere [[this-binding-precedence|Ordine di Precedenza]] globale).

## 📚 Collegamenti e Approfondimenti

- [[this-concept|Comprendere cos'è this in profondità]]
- [[this-implicit-chain|Implicit: Risalire L'Ultimo Livello di Oggetti]]
- [[this-implicit-lost|Implicitly Lost: Perdita con Assegnamento e Callback]]
- [[this-implicit-event-handlers|Implicit e Manipolazione: Forzature Event Handlers]]
- [[this-binding-problems|Problematiche Callback: Correlato a Implicitly Lost]]
- [[this-call-apply-bind|Soluzioni: Explicit Binding con call/apply/bind]]
- [[this-arrow-functions|Soluzioni: Comportamento Lexical Binding delle Arrow]]

---

**Tags**: `#javascript` `#this` `#implicit-binding` `#methods`
