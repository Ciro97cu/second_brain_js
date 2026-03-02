# [[../../appunti-completi#62-transpiling|Transpiling]]

Il transpiling è il processo di conversione del codice JavaScript moderno in una versione equivalente con sintassi più vecchia, compatibile con browser datati. È l'unione di "transforming" e "compiling".

## 🎯 Concetti Chiave

- **Trasforma sintassi**: Converte nuova sintassi JS in vecchia sintassi equivalente
- **Build-time operation**: Avviene durante la fase di build, non a runtime
- **Source maps**: Mantiene il collegamento tra codice originale e transpilato per debugging
- **Differenza da polyfill**: Polyfill aggiunge funzionalità mancanti, transpiling traduce sintassi

## 💻 Esempi di Codice

### Arrow Functions

```javascript
// ES6 (scrivi questo)
const doppi = [1, 2, 3].map((n) => n * 2);

// ES5 (viene transpilato così)
var doppi = [1, 2, 3].map(function (n) {
  return n * 2;
});
```

### Default Parameters

```javascript
// ES6
function saluta(nome = "Ospite") {
  console.log("Ciao, " + nome);
}

// ES5 (transpilato)
function saluta(nome) {
  if (nome === undefined) {
    nome = "Ospite";
  }
  console.log("Ciao, " + nome);
}
```

### Template Literals

```javascript
// ES6
const nome = "Mario";
const età = 30;
const msg = `Ciao, sono ${nome} e ho ${età} anni`;

// ES5 (transpilato)
var nome = "Mario";
var età = 30;
var msg = "Ciao, sono " + nome + " e ho " + età + " anni";
```

### Destructuring

```javascript
// ES6
const { nome, età } = persona;
const [primo, secondo] = array;

// ES5 (transpilato)
var nome = persona.nome;
var età = persona.età;
var primo = array[0];
var secondo = array[1];
```

### Classes

```javascript
// ES6
class Animale {
  constructor(nome) {
    this.nome = nome;
  }
  parla() {
    console.log(this.nome + " fa un verso");
  }
}

// ES5 (transpilato)
function Animale(nome) {
  this.nome = nome;
}
Animale.prototype.parla = function () {
  console.log(this.nome + " fa un verso");
};
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Dimenticare di transpilare**: Codice ES6+ non funzionerà in browser vecchi senza transpiling
- ❌ **Transpilare node_modules**: Tipicamente non si transpilano le dipendenze, causando errori
- ❌ **Source maps mancanti**: Senza source maps, il debugging diventa difficile
- ❌ **Target sbagliato**: Transpilare troppo (ES3) rallenta il codice, troppo poco (ES2020) rompe i vecchi browser

## ✅ Best Practices

- ✓ **Usa Babel con preset-env**: Transpila automaticamente solo ciò che serve in base ai browser target
- ✓ **Configura browserslist**: Definisci i browser da supportare (`> 0.5%, last 2 versions`)
- ✓ **Abilita source maps**: Essenziali per debugging (`devtool: 'source-map'` in webpack)
- ✓ **Modern + Legacy builds**: Servi codice moderno ai browser recenti, transpilato ai vecchi
- ✓ **CI/CD integration**: Integra il transpiling nella pipeline di build automatica

## 🔗 Collegamenti

**Prerequisiti**:

- [[scope.md|Scope]]
- [[funzioni.md|Funzioni]]
- [[arrow-functions.md|Arrow Functions]]
- [[classes.md|Classes]]

**Concetti Correlati**:

- [[polyfilling.md|Polyfilling]]
- [[non-javascript.md|Non-JavaScript]]
- Build tools (webpack, rollup, vite)

**Approfondimenti**:

- TypeScript (transpiler con type-checking)
- Source maps
- Tree shaking
- Code splitting

## 📚 Riferimenti

- [Babel - The JavaScript Compiler](https://babeljs.io/)
- [Babel preset-env](https://babeljs.io/docs/en/babel-preset-env)
- [TypeScript](https://www.typescriptlang.org/)
- [SWC - Super-fast TypeScript/JavaScript compiler](https://swc.rs/)
- [esbuild - An extremely fast JavaScript bundler](https://esbuild.github.io/)
- [Browserslist](https://github.com/browserslist/browserslist)

## 📌 Note Personali

Il transpiling è diventato uno standard nel workflow JavaScript moderno. Babel è il transpiler de facto, ma alternative come SWC ed esbuild stanno guadagnando popolarità per la loro velocità. Con TypeScript, si ottiene anche il type-checking oltre al transpiling.

**Perché usare il transpiling**:

1. **Leggibilità**: Scrivi codice moderno, pulito e conciso
2. **Performance**: Browser recenti possono ricevere codice ottimizzato
3. **Feedback**: Testa nuove funzionalità e fornisci feedback al TC39
4. **Manutenibilità**: Codice più facile da mantenere e capire

---

**Tags**: `#javascript` `#fondamenti` `#transpiling` `#babel` `#build-tools` `#es6` `#compatibilità`
