# [[../../appunti-completi#63-non-javascript|Compatibilità e Ambienti]]

## 🎯 Concetto

Quando si scrive codice "universale" (isomorphic / universal JavaScript) che deve funzionare sia nel browser che su Node.js (React o framework Full-Stack), è cruciale testare la presenza di determinate feature all'interno dell'ambiente di esecuzione (Feature Detection) piuttosto che assumere ingenuamente il contesto di esecuzione basandosi su variabili come `window` o l'User Agent.

## 💻 Codice

### Feature Detection Pattern

Controllare esplicitamente un'API senza causare un errore "is not defined", basandosi sul controllo di tipi globale per gli host object.

```javascript
// Controllare la disponibilità dell'API asincrona o nativa prima dell'uso
if (typeof localStorage !== "undefined") {
  localStorage.setItem("key", "value");
}

if (typeof fetch === "function") {
  fetch(url).then(/* callback di rete */);
}

// Usare `in` testando il Global Object
if ("geolocation" in navigator) {
  navigator.geolocation.getCurrentPosition(callback);
}
```

### Ambienti JavaScript a confronto

Diverse destinazioni d'uso possiedono set di Host Objects differenti:
- **Browser**: Dispone tipicamente di `window`, `document`, manipolazioni di DOM, `localStorage` / Storage API, `fetch`.
- **Node.js**: Dispone di `global`, `process`, accesso diretto al file system via moduli nativi (`fs`), networking a basso livello (`http`).
- **Web Workers / Service Workers**: Dispongono di un contesto isolato chiamato `self`, uso di Cache API e IndexedDB, ma **assoluto divieto e impossibilità di accesso al DOM**.

## ✅ Best Practices

- **Test di Esistenza Robusti**: Usare sistematicamente `typeof variabile !== "undefined"` per verificare l'esistenza di host objects. Trovarsi di fronte allo strict-mode innalzerà errori fatali se si tentasse l'uso senza controlli.
- **Evitare Environment Sniffing**: Non tentare mai di predire l'ecosistema analizzando la stringa dell'User-Agent o del pacchetto node. Questa pratica cade facilmente in obolescenza o introduce vettori di falso positivo.
- **Isolare i Polyfill**: Fornire implementazioni alternative (Polyfill) laddove le API corrette mancassero di default in vecchi ambienti operativi o runtime specifici (ad esempio `fetch` in versioni molto antiche di Node.js, prima che venisse incluso nei pacchetti nativi globali).

---

**Tags**: `#javascript` `#compatibilita` `#feature-detection` `#ambiente` `#isomorphic`
