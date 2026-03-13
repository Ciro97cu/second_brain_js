# [[../../appunti-completi#le-bolle-di-scope-annidate|Best Practices per le Bolle di Scope]]

La visualizzazione mentale o astratta delle bolle di scope agevola istantaneamente la comprensione sui diritti di accessibilità della memoria ed evita incomprensioni sui valori manipolabili per i relativi scope.

Viene considerata appropriata la prassi di assicurare nel software lo sviluppo di una chiara gerarchia interna.

```javascript
// Chiara gerarchia
function elabora() {
  // Bolla elabora
  let dati = [1, 2, 3];

  function trasforma(item) {
    // Bolla trasforma, internata dentro elabora
    return item * 2; // Accede lecitamente a 'dati' (nella bolla confinante ed esterna)
  }

  return dati.map(trasforma);
}
```

Di controparte, è considerata una pratica sgradevole appesantire le letture con una quantità indiscriminata o soverchiante di livelli di annidamento. La tracciatura si tramuta velocemente un peso critico e insostenibile mentalmente per il mantenimento.

```javascript
// Da evitare categoricamente: annidamento disorganizzato e incomprensibile
function a() {
  function b() {
    function c() {
      function d() {
        // ...
      }
    }
  }
}

// Preferibile: la struttura lineare, piana e con astrazione del flusso di esecuzione
function processa(input) {
  const risultato = trasforma(input);
  return valida(risultato);
}
```

## 🔗 Collegamenti

- [[scope-bubbles]]
