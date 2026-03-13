# [[../../appunti-completi#blocchi-come-scope-blocks-as-scopes|let e const nei Cicli (Loops)]]

## 🔄 `let` nei Cicli for

Una delle applicazioni più evidenti e vantaggiose del **block scope** (`let`) è nel contesto dei cicli temporali e ripetitivi come il loop `for`.

I loop `for` che utilizzano `var` espongono le variabili allo scope superiore e presentano problemi derivati dalle **closures** all'interno dell'iterazione.

```javascript
// Con var: problematico
for (var i = 0; i < 5; i++) {
  setTimeout(function () {
    console.log(i); // Stampa sempre 5!
  }, 100);
}
// Problema: 'i' è condivisa, alla fine vale 5

// Con let: corretto
for (let j = 0; j < 5; j++) {
  setTimeout(function () {
    console.log(j); // Stampa 0, 1, 2, 3, 4
  }, 100);
}
// 'j' è RICREATA ad ogni iterazione con block scope
```

## 🔁 Rebinding per Iterazione

L'uso di `let` nell'intestazione del ciclo non si limita a legare la variabile al corpo del ciclo. In realtà, **ri-lega (rebinds) la variabile a ogni singola iterazione**, assicurandosi di riassegnarle il valore corretto che aveva alla fine del passaggio precedente.

```javascript
for (let i = 0; i < 5; i++) {
  console.log(i);
}

// Dietro le quinte, è come se il codice funzionasse così:
{
  let i = 0;
  if (i < 5) {
    console.log(i);
    i++;
  }
}
{
  let i = 1; // Nuovo binding con valore precedente
  // ... e così via fino a i = 5
}
```

Questo **rebinding automatico** è ciò che permette alle closures nei loop di funzionare correttamente con `let`, cosa impossibile con `var`.

## 🔒 `const` nei Cicli

`const` crea variabili che non possono essere riassegnate, limitando le possibilità di interazione nei cicli come il `for` incrementale classico.

```javascript
// ❌ ERRORE con for classico (i viene riassegnato)
for (const i = 0; i < 5; i++) {
  // TypeError - Poiché la struttura re-inizializza 'i++' a ogni turno.
  console.log(i);
}
```

Tuttavia, `const` lavora nativamente nei cicli logici interattivi non dipendenti da un accumulatore assegnato: il `for...of` ed il `for...in`. In questo contesto, l'iterazione fornisce ogni volta un nuovo iteratore del binding come un nuovo blocco distinto.

```javascript
// ✅ OK con for...of (ogni iterazione ha nuovo binding)
const arr = [10, 20, 30];
for (const value of arr) {
  console.log(value); // 10, 20, 30
}

// ✅ OK con for...in
const obj = { a: 1, b: 2 };
for (const key in obj) {
  console.log(key, obj[key]); // "a" 1, "b" 2
}
```
