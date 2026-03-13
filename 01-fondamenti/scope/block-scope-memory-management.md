# [[../../appunti-completi#blocchi-come-scope-blocks-as-scopes|Gestione della Memoria con Block Scope]]

## Confinare Dati Temporanei
Per risolvere il problema del mantenimento in memoria di grandi dati inutilizzati dalle closures, si possono usare blocchi espliciti.

```javascript
function process(data) {
  let result;
  {
    // Blocco esplicito per i dati temporanei
    let someReallyBigData = { /* 50MB */ };
    result = doSomething(someReallyBigData);
  }
  // someReallyBigData può essere garbage-collected

  $("#button").click(function click() {
    console.log("Button clicked!");
  });

  return result;
}
```

Al termine dell'esecuzione del blocco interno, la variabile dichiarata con `let` esce dallo scope logico. Il Garbage Collector sa perentoriamente che non sarà più accessibile nel resto del corpo della funzione e libera immediatamente la memoria, anche se le closures successive restano attive a lungo.

### Risoluzione in Cicli con Grandi Dati
I blocchi espliciti diventano cruciali nell'iterazione di cicli che elaborano moli pesanti di informazioni per ogni step.

```javascript
let users = getUsersFromAPI(); 

users.forEach(function (user) {
  let summary;
  {
    let largeUserData = fetchDetailedProfile(user.id); // 5MB
    summary = extractSummary(largeUserData); // 50 bytes
  }
  // largeUserData (5MB) liberato dopo ogni iterazione

  $("#user-" + user.id).click(function () {
    displaySummary(summary); 
  });
});
```

Confidando i dati temporanei in blocchi limitati, si evita che migliaia di closures mantengano inutilmente gigabyte interi di memoria allocata cumulativamente. Invece, risiederà in memoria solo il minuscolo dato strettamente necessario e realmente catturato dalla closure (es. un piccolo oggetto `summary`).
