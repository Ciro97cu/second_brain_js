# [[../../appunti-completi#63-non-javascript|Non-JavaScript]]

Quando si scrive JavaScript per il web, gran parte del codice interagisce con API fornite dal browser (o da Node.js), non dal linguaggio JavaScript stesso. Queste sono chiamate "host objects" e "Web APIs".

## 🎯 Concetti Chiave

- **Host Objects**: Oggetti forniti dall'ambiente di esecuzione (browser, Node.js), non da JavaScript
- **Web APIs**: Interfacce fornite dal browser per interagire con DOM, rete, storage, ecc.
- **Native Objects**: Oggetti definiti dalla specifica ECMAScript (Array, Object, Date, ecc.)
- **Differenza critica**: JavaScript definisce il linguaggio, il browser definisce le API

## 💻 Esempi di Codice

### DOM API (Browser Only)

```javascript
// document è un host object, non parte di JavaScript
let elemento = document.getElementById("mioId");
elemento.addEventListener("click", function () {
  console.log("Cliccato!");
});

elemento.style.color = "red";
elemento.innerHTML = "Nuovo testo";
elemento.classList.add("attivo");
```

### Window Object (Browser)

```javascript
// window è il global object nel browser
console.log(window.innerWidth); // Larghezza finestra
console.log(window.location.href); // URL corrente
window.scrollTo(0, 100); // Scroll della pagina

// setTimeout/setInterval sono API del browser
setTimeout(() => console.log("Dopo 1s"), 1000);
setInterval(() => console.log("Ogni 2s"), 2000);
```

### Console API

```javascript
// console NON è parte di JavaScript, è fornito dall'ambiente
console.log("Log normale");
console.warn("Attenzione!");
console.error("Errore!");
console.table([{ nome: "Mario" }, { nome: "Luigi" }]);

console.time("operazione");
// ... codice ...
console.timeEnd("operazione"); // Mostra tempo
```

### Dialog API (Browser)

```javascript
// alert, confirm, prompt sono API del browser
alert("Messaggio"); // Blocca esecuzione

let conferma = confirm("Sei sicuro?");
if (conferma) {
  console.log("Confermato");
}

let nome = prompt("Come ti chiami?", "Mario");
console.log("Ciao, " + nome);
```

### Fetch API (Browser/Node.js polyfilled)

```javascript
// fetch è una Web API, non JavaScript nativo
fetch("https://api.example.com/data")
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error(error));
```

### Storage API (Browser)

```javascript
// localStorage e sessionStorage sono API del browser
localStorage.setItem("chiave", "valore");
let valore = localStorage.getItem("chiave");
localStorage.removeItem("chiave");

sessionStorage.setItem("temporaneo", "dato");
```

### Native vs Host Objects

```javascript
// ✅ NATIVE OBJECTS (JavaScript puro)
let array = new Array(1, 2, 3); // Parte di ECMAScript
let date = new Date(); // Parte di ECMAScript
let regex = new RegExp("pattern"); // Parte di ECMAScript
console.log(typeof Array); // "function"

// ❌ HOST OBJECTS (forniti dall'ambiente)
let div = document.createElement("div"); // Browser
let xhr = new XMLHttpRequest(); // Browser
console.log(typeof document); // "object" (host object)
console.log(typeof window); // "object" (host object)
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Assumere disponibilità universale**: `document` non esiste in Node.js, `require()` non esiste nel browser
- ❌ **Feature detection mancante**: Non controllare se un'API esiste prima di usarla
- ❌ **Confondere native e host**: `Array.isArray()` è nativo, `document.querySelector()` è host
- ❌ **Sincronizzazione errata**: `alert()`, `prompt()`, `confirm()` bloccano l'esecuzione (sincroni)

## ✅ Best Practices

- ✓ **Feature detection**: Controlla sempre se un'API esiste prima di usarla
- ✓ **Environment detection**: Distingui tra browser, Node.js, Worker, ecc.
- ✓ **Polyfill quando necessario**: Usa polyfill per API mancanti (es. `fetch` in IE)
- ✓ **Evita API bloccanti**: Preferisci interfacce moderne a `alert()`, `prompt()`, `confirm()`
- ✓ **Consulta documentazione**: MDN per browser, Node.js docs per Node

## 🔗 Collegamenti

**Prerequisiti**:

- [[scope.md|Scope e Variabili Globali]]
- [[oggetti.md|Oggetti]]

**Concetti Correlati**:

- [[polyfilling.md|Polyfilling]]
- [[transpiling.md|Transpiling]]
- [[async-await.md|Async/Await e Promises]]

**Approfondimenti**:

- Web APIs complete list (MDN)
- Node.js built-in modules
- Service Workers
- Web Workers
- IndexedDB

## 📚 Riferimenti

- [MDN - Web APIs](https://developer.mozilla.org/en-US/docs/Web/API)
- [MDN - Document Object Model (DOM)](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)
- [Node.js API Documentation](https://nodejs.org/api/)
- [ECMAScript Specification](https://tc39.es/ecma262/)
- [Can I Use](https://caniuse.com/) - Browser compatibility checker

## 📌 Note Personali

È fondamentale distinguere tra JavaScript puro (ECMAScript) e le API fornite dall'ambiente. Quando si passa da browser a Node.js, o quando si scrive codice universale (isomorphic/universal), questa distinzione diventa critica.

**Feature Detection Pattern**:

```javascript
// Sempre controllare disponibilità
if (typeof localStorage !== "undefined") {
  localStorage.setItem("key", "value");
}

if (typeof fetch === "function") {
  fetch(url);
}

if ("geolocation" in navigator) {
  navigator.geolocation.getCurrentPosition(callback);
}
```

**Ambienti JavaScript**:

- **Browser**: `window`, `document`, DOM, Web APIs
- **Node.js**: `global`, `process`, `require`, file system, HTTP
- **Web Workers**: `self`, no DOM, subset di Web APIs
- **Service Workers**: `self`, Cache API, no DOM

---

**Tags**: `#javascript` `#fondamenti` `#browser` `#web-apis` `#dom` `#host-objects` `#node-js`
