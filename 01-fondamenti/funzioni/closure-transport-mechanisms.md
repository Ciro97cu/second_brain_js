# Closure nel Mondo Reale [[../../appunti-completi#closure|📚]]

## Closure Ovunque nel Codice Quotidiano

Gli esempi visti finora erano costruzioni accademiche utili a definire il concetto. Tuttavia, la promessa iniziale era dimostrare che la Closure è ovunque nel codice che scriviamo quotidianamente. È il momento di osservare questa verità.

Qualunque sia il mezzo utilizzato per trasportare una funzione fuori dal suo Lexical Scope, essa manterrà un riferimento allo scope in cui è stata originariamente dichiarata (al momento della scrittura, o "author-time") e lo utilizzerà ovunque venga eseguita.

## 1. Passare come Argomento

```javascript
function foo() {
  var a = 2;

  function baz() {
    console.log(a); // 2
  }

  bar(baz); // Passa baz come argomento
}

function bar(fn) {
  fn(); // ⚡ CLOSURE! - Esegue baz, che ricorda 'a'
}

foo();
```

**Cosa succede**:

1. `foo()` definisce `a` e `baz()`
2. `foo()` passa `baz` alla funzione `bar` (che è fuori dallo scope di `foo`)
3. `bar` esegue `fn()` (che è `baz`)
4. `baz()` accede ancora a `a`, anche se eseguita dentro `bar`

## Timer e Callback

Si consideri un classico esempio di utilizzo di un timer:

```javascript
function wait(message) {
  setTimeout(function timer() {
    console.log(message);
  }, 1000);
}

wait("Hello, closure!");
```

In questo codice, la funzione interna timer viene passata all'utility setTimeout. La funzione timer possiede una Closure sullo scope di wait, mantenendo quindi un riferimento alla variabile message.

Mille millisecondi dopo l'esecuzione di wait, quando il suo scope interno dovrebbe essere teoricamente sparito, quella funzione anonima mantiene ancora vivo il collegamento a quello scope. All'interno dell'Engine, l'utility setTimeout invoca la funzione passata, e il riferimento al Lexical Scope risulta ancora intatto. Questa è la Closure.

## Event Handlers

Lo stesso principio si applica, ad esempio, nella gestione degli eventi (qui in stile jQuery, ma valido per qualsiasi framework):

```javascript
function setupButton(btn) {
  let name = "Brian";
  let selector = "#" + btn;

  $(selector).click(function activator() {
    console.log("Activating: " + name);
  });
}

setupButton("my-button");
```

## Funzioni Come Valori di Prima Classe

Essenzialmente, ogni volta che si trattano le funzioni come valori di prima classe e le si passano in giro (come callback), è molto probabile che si stia esercitando la Closure. Che si tratti di timer, gestori di eventi, richieste Ajax o Web Workers, se si passa una funzione callback che accede al proprio scope lessicale, si sta utilizzando la Closure.

## ✅ Punti Chiave

1. **Indipendente dal meccanismo** - La closure funziona con return, argomenti, callbacks, eventi
2. **Scope persistente** - Lo scope rimane vivo indipendentemente da dove la funzione viene eseguita
3. **Pattern comuni** - Timer, eventi, factory functions usano tutti le closure
4. **Garbage Collection** - Lo scope viene mantenuto finché esiste un riferimento alla funzione

## 🔗 Collegamenti

- [[closure-concept|Concetto di Closure]] - Definizione e funzionamento base
- [[closure-patterns|Pattern Pratici]] - Usi comuni delle closure
- [[funzioni|Funzioni]] - Le funzioni come first-class citizens
- [[../../appunti-completi#closure|Closure Completo]]

## 📚 Risorse

- MDN: Closures
- JavaScript.info: Closure

## 📌 Tag

#javascript #closure #callbacks #event-handlers #timers #function-transport
