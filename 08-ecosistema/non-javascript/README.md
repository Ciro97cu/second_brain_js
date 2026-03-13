# [[../../appunti-completi#63-non-javascript|Non-JavaScript Index]]

Quando si scrive codice in ambienti reali, gran parte delle funzionalità interagiscono con API fornite dall'ambiente di esecuzione (browser, Node.js), non dal linguaggio JavaScript stesso. Queste sono chiamate "host objects" e "Web APIs".

## 🎯 Concetti Chiave

- **Host Objects**: Oggetti forniti dall'ambiente di esecuzione, non da JavaScript.
- **Web APIs**: Interfacce fornite dal browser per interagire con DOM, rete, storage, ecc.
- **Native Objects**: Oggetti definiti dalla specifica ECMAScript (Array, Object, Date, ecc.).
- **Indipendenza dal linguaggio**: JavaScript definisce il linguaggio e le sue primitive, il browser o il runtime Node.js definiscono le API aggiuntive.

## 📂 Sotto-Argomenti

- [[host-vs-native.md|Host Objects vs Native Objects]]
- [[web-apis.md|Web APIs Comuni (DOM, Fetch, Storage)]]
- [[compatibilita-ambienti.md|Compatibilità tra Ambienti (Feature Detection)]]

## 🔗 Collegamenti

**Prerequisiti**:

- [[../../01-fondamenti/scope/README.md|Scope e Variabili Globali]]
- [[../../01-fondamenti/oggetti/README.md|Oggetti]]

**Concetti Correlati**:

- [[../polyfilling.md|Polyfilling]]
- [[../transpiling.md|Transpiling]]

**Approfondimenti**:

- Web APIs complete list (MDN)
- Node.js built-in modules
- Service Workers e Web Workers

## 📚 Riferimenti

- [MDN - Web APIs](https://developer.mozilla.org/en-US/docs/Web/API)
- [Node.js API Documentation](https://nodejs.org/api/)
- [ECMAScript Specification](https://tc39.es/ecma262/)

---

**Tags**: `#javascript` `#fondamenti` `#ecosistema` `#web-apis` `#node-js`
