# [[../../appunti-completi#63-non-javascript|Web APIs Comuni]]

## 🎯 Concetto

I browser offrono una vasta gamma di API (Web APIs) che non fanno parte dello standard JavaScript vero e proprio ma permettono al codice di prendere vita: manipolare pagine HTML, effettuare richieste di rete e gestire lo storage locale. Tali API vengono tradizionalmente messe a disposizione tramite il "Global Object" del browser (`window`).

## 💻 Codice

### DOM API, Browser Elements e Temporizzazione

```javascript
// document e window (Host Objects) e API Globali
let elemento = document.getElementById("mioId");

elemento.addEventListener("click", function () {
  console.log("Evento intercettato!");
});

window.scrollTo(0, 100);

// setTimeout e setInterval appartengono alle API del browser, non a JS nativo
setTimeout(() => console.log("Esecuzione ritardata"), 1000);
```

### Console API e Dialoghi

Rispetto a JavaScript puro, `console` è un tool di debug host-provided, non una direttiva nativa.

```javascript
console.warn("Attenzione");
console.table([{ nome: "Mario" }, { nome: "Luigi" }]);
console.time("misurazione");

// API di Dialogo (bloccanti il Main Thread JavaScript)
let conferma = confirm("Azione irreversibile?");
```

### Fetch API (Rete) e Storage Locale

```javascript
// Rete e Storage (disponibile nativamente nel browser, e via polyfill su versioni Node anziane)
fetch("https://api.example.com/data")
  .then((res) => res.json())
  .then(console.log);

localStorage.setItem("chiave", "valore");
sessionStorage.setItem("temporaneo", "dato");
```

## ⚠️ Gotcha

- **Blocco dell'esecuzione**: Le chiamate di interfaccia base come `alert()`, `prompt()` e `confirm()` bloccano il thread principale asincrono, interrompendo l'esecuzione di qualsiasi altro script ed impedendo all'utente di selezionare interazioni della UI finchè non gestite.
- **Limiti di Storage**: Storage API, specialmente `localStorage` che viaggia in totale sincronicità, rallentano le performance durante la lettura di grossi volumi testuali persistenti. Non utilizzarlo per estesi dati applicativi, ma solo per preferenze semplici o piccoli token.
- **Ritorno asincrono**: Nessuna Web API in grado di contattare la rete è sincrona. Tutte ritornano `Promises` basate sulla disponibilità della risposta.

---

**Tags**: `#javascript` `#web-apis` `#browser` `#dom` `#fetch`
