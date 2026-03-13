# [[../../appunti-completi#63-non-javascript|Host vs Native Objects]]

## 🎯 Concetto

È fondamentale distinguere tra gli oggetti definiti dalla specifica ECMAScript (Native Objects) e quelli forniti dall'ambiente in cui JavaScript viene eseguito (Host Objects). 

- **Native Objects**: Parte intrinseca del linguaggio puro. Esistono in qualsiasi ambiente JavaScript con implementazioni standard concordate a priori. Esempi: `Array`, `Object`, `Date`, `RegExp`.
- **Host Objects**: Dipendono interamente dall'ambiente (Browser, Node.js). Non sono garantiti ovunque e seguono regole proprie al di fuori di ECMAScript. Esempi: `window`, `document`, `process` (Node.js).

## 💻 Codice

```javascript
// ✅ NATIVE OBJECTS (JavaScript puro)
let array = new Array(1, 2, 3); // Parte di ECMAScript
let date = new Date(); // Parte di ECMAScript
let regex = new RegExp("pattern"); // Parte di ECMAScript
console.log(typeof Array); // "function"

// ❌ HOST OBJECTS (forniti dall'ambiente)
let div = document.createElement("div"); // Browser spec
let xhr = new XMLHttpRequest(); // Browser spec
console.log(typeof document); // "object" (host object)
console.log(typeof window); // "object" (host object)
```

## ⚠️ Gotcha ed Errori Comuni

- **Confondere la disponibilità**: Assumere che `document` sia disponibile in Node.js o che `require()` sia disponibile nativamente in un browser causa immediatamente errori di riferimento e cadute di esecuzione.
- **Tipizzazione ambigua**: Gli host objects non seguono necessariamente le stesse regole sintattiche o di performance dei native objects, essendo spesso ponti verso codice macchina (ad esempio C++ nei browser web). Il loro comportamento "riflette" ma non necessariamente implementa fedelmente un vero oggetto ECMAScript.

---

**Tags**: `#javascript` `#host-objects` `#native-objects` `#ecmascript`
