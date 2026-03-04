# Closure: Meccanismi di Trasporto [[../../appunti-completi#closure|📚]]

## 🚀 Trasportare Funzioni Fuori dal Loro Scope

La Closure funziona **indipendentemente da come la funzione viene trasportata** al di fuori del suo scope. Non importa se viene restituita come valore di ritorno o passata come argomento: qualunque sia il mezzo utilizzato per trasportare una funzione interna al di fuori del suo Lexical Scope, essa **manterrà sempre un riferimento di closure** allo scope originale.

La funzione potrà sempre accedere a quello scope **ovunque venga eseguita**.

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

## 2. Callback e Timer

```javascript
function wait(message) {
  setTimeout(function timer() {
    console.log(message);
  }, 1000);
}

wait("Hello, closure!"); // Dopo 1 secondo: "Hello, closure!"
```

La funzione `timer` ha una **closure su `message`**. Anche dopo che `wait()` ha terminato, `timer` ricorda `message` e può stamparlo 1 secondo dopo.

### Esempio Pratico: Debounce

```javascript
function debounce(fn, delay) {
  let timeoutId;

  return function (...args) {
    clearTimeout(timeoutId); // Closure su timeoutId
    timeoutId = setTimeout(() => fn(...args), delay);
  };
}

const debouncedSearch = debounce((query) => {
  console.log("Searching for:", query);
}, 300);
```

La funzione restituita mantiene una closure su `timeoutId` e `fn`, permettendo di implementare il pattern debounce.

## 3. Event Handlers

```javascript
function setupButton(buttonId) {
  var clickCount = 0;

  document.getElementById(buttonId).addEventListener("click", function () {
    clickCount++;
    console.log(`Button clicked ${clickCount} times`);
  });
}

setupButton("myButton");
```

Il callback dell'evento ha una **closure su `clickCount`**. Ogni click incrementa e stampa il contatore, anche se `setupButton` ha già terminato.

### Esempio: Rimuovere Event Listener

```javascript
function attachClickHandler(element) {
  let clicks = 0;

  function handler() {
    clicks++;
    console.log(`Clicks: ${clicks}`);

    if (clicks >= 5) {
      element.removeEventListener("click", handler); // Closure su handler stesso
      console.log("Handler removed");
    }
  }

  element.addEventListener("click", handler);
}
```

## 4. Return Values (Ritorno di Funzione)

```javascript
function makeMultiplier(factor) {
  return function (number) {
    return number * factor; // Closure su factor
  };
}

const double = makeMultiplier(2);
const triple = makeMultiplier(3);

console.log(double(5)); // 10
console.log(triple(5)); // 15
```

Restituire una funzione è il modo più comune di sfruttare le closure. La funzione restituita mantiene l'accesso allo scope esterno.

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
