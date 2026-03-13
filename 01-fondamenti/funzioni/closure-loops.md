# [[../../appunti-completi#39-scope-closure-e-illuminazione-enlightenment|Closure: Gestione nei Cicli]]

## 🔄 Cicli e Closure

L'esempio più comune utilizzato per illustrare problematiche legate alle Closure coinvolge un semplice ciclo `for`. Questo scenario confonde spesso gli sviluppatori e porta a risultati inaspettati.

Si consideri il seguente codice, dal quale ci si aspetterebbe logicamente la stampa dei numeri da 1 a 5, uno al secondo:

```javascript
for (var i = 1; i <= 5; i++) {
  setTimeout(function timer() {
    console.log(i);
  }, i * 1000);
}
```

### Il Problema

Eseguendo questo codice, il risultato è sorprendente: viene stampato il numero **6 per cinque volte**.

Il motivo risiede nel fatto che la callback `timer` viene eseguita solo dopo che il ciclo ha terminato la sua intera esecuzione. Quando i timer scattano, accedono al valore corrente di `i`, che è diventato 6 (la condizione che fa terminare il ciclo). 

A causa dell'uso di `var`, tutte e cinque le funzioni condividono lo stesso ambito globale o di funzione e, di conseguenza, riferiscono la medesima variabile `i`.

### Soluzione Storica: IIFE

Per risolvere il problema prima dell'avvento di ES6, era necessario creare uno Scope nuovo e dedicato per ogni iterazione del ciclo utilizzando una IIFE:

```javascript
for (var i = 1; i <= 5; i++) {
  (function(j) {
    setTimeout(function timer() {
      console.log(j); // Usa la variabile locale j
    }, j * 1000);
  })(i); // Passa il valore corrente di i all'IIFE
}
```

Questo approccio "congela" il valore di `i` in una nuova variabile `j` per ogni iterazione, creando uno scope separato.

### Soluzione Moderna: Block Scoping con `let`

Con ES6, la soluzione è molto più elegante. La dichiarazione `let` trasforma essenzialmente il blocco in uno Scope su cui è possibile applicare la Closure.

Inoltre, esiste un comportamento speciale per le dichiarazioni `let` nell'intestazione di un ciclo `for`: la variabile **viene dichiarata nuovamente per ogni singola iterazione**, inizializzata con il valore dell'iterazione precedente.

```javascript
for (let i = 1; i <= 5; i++) {
  // Un nuovo scope viene creato ad ogni iterazione
  setTimeout(function timer() {
    console.log(i); // Stampa 1, 2, 3, 4, 5
  }, i * 1000);
}
```

In questo scenario, Scope di Blocco e Closure lavorano in perfetta sinergia, risolvendo il problema in modo pulito e intuitivo.

## ✅ Punti Chiave

1. **Il Problema di `var`** - Le variabili dichiarate con `var` nei cicli sono condivise da tutte le iterazioni.
2. **IIFE** - Funzionano creando uno scope separato per ogni iterazione.
3. **Il Vantaggio di `let`** - Crea automaticamente un nuovo scope di blocco ad ogni iterazione nei cicli `for`.

## 🔗 Collegamenti

- [[closure-concept|Concetto di Closure]]
- [[../scope/block-scope-loops|Block Scope nei Loop]]
- [[iife|IIFE (Immediately Invoked Function Expression)]]

## 📚 Risorse

- "You Don't Know JS" - Scope & Closures

## 📌 Tag

#javascript #closure #loop-closure #let #var #iife #block-scope
