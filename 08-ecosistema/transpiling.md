# [[../appunti-completi#62-transpiling|Transpiling]]

Il transpiling è il processo logico di conversione del codice JavaScript moderno in una versione equivalente con sintassi più vecchia, garantendo la compatibilità con i browser datati. È l'unione dei concetti di "transforming" e "compiling".

## 🎯 Concetti Chiave

- **Trasformazione sintattica**: Converte la nuova sintassi in sintassi equivalente antecedente.
- **Operazione a build-time**: Avviene durante la fase di preparazione, non a runtime.
- **Source maps**: Mantengono il tracciamento tra il codice originale e quello transpilato per agevolare il debugging.
- **Differenza da polyfill**: Mentre il polyfilling aggiunge funzionalità mancanti a livello di API, il transpiling traduce l'intera sintassi.

## 💻 Esempi di Codice

### Arrow Functions e Default Parameters

```javascript
// ES6 (Codice sorgente moderno)
const doppi = [1, 2, 3].map((n) => n * 2);
function saluta(nome = "Ospite") {
  console.log(`Ciao, ${nome}`);
}

// ES5 (Codice transpilato per retrocompatibilità)
var doppi = [1, 2, 3].map(function (n) {
  return n * 2;
});
function saluta(nome) {
  if (nome === undefined) {
    nome = "Ospite";
  }
  console.log("Ciao, " + nome);
}
```

### Classes e Destructuring

```javascript
// ES6
class Animale {
  constructor(nome) {
    this.nome = nome;
  }
}
const { nome } = new Animale("Cane");

// ES5 (transpilato)
function Animale(nome) {
  this.nome = nome;
}
var nome = new Animale("Cane").nome;
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Assenza di transpiling**: Il codice ES6+ non verrà analizzato correttamente dai browser obsoleti.
- ❌ **Transpilazione di librerie esterne**: Includere la cartella `node_modules` nel processo genera spesso errori e rallenta la build.
- ❌ **Configurazione errata del target**: Una transpilazione eccessiva (es. ES3) introduce codice verboso; una troppo limitata non supporta i device più vecchi.

## ✅ Best Practices

- ✓ **Utilizzare preset dinamici**: Configurare gli strumenti affinché il processo si basi su un elenco mirato di browser (es. `@babel/preset-env` e `browserslist`).
- ✓ **Source maps in sviluppo**: Generare sempre le source maps per consentire l'ispezione del codice sorgente nel browser.
- ✓ **Integrazione in CI/CD**: Automatizzare la build e il transpiling per non doverci pensare a livello locale prima della pubblicazione.

## 🔗 Collegamenti

**Prerequisiti e Correlati**:

- [[../01-fondamenti/scope/scope|Scope e Lexical Environment]]
- [[../01-fondamenti/funzioni/funzioni|Funzioni]]
- [[polyfilling|Polyfilling]]
- [[non-javascript/README|Ecosistema Non-JavaScript]]

**Approfondimenti**:

- Typescript e Type Checking
- Tree shaking e Code Splitting

## 📚 Riferimenti

- [Babel](https://babeljs.io/)
- [SWC](https://swc.rs/)
- [esbuild](https://esbuild.github.io/)

---

**Tags**: `#javascript` `#ecosistema` `#transpiling` `#babel` `#build-tools` `#compatibilità`
