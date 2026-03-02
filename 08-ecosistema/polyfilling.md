# [[../../appunti-completi#61-polyfilling|Polyfilling]]

Il polyfill è un pezzo di codice che replica il comportamento di una funzionalità JavaScript moderna, permettendone l'uso anche in browser vecchi che non la supportano nativamente.

## 🎯 Concetti Chiave

- **Definizione**: Codice che "riempie" le lacune tra vecchie e nuove funzionalità JavaScript
- **Pattern di guardia**: Controlla se la funzionalità esiste prima di definirla (`if (!feature) { ... }`)
- **Non sovrascrive nativi**: Preserva le implementazioni native quando disponibili
- **Limitazioni**: Non tutte le funzionalità sono completamente polyfillabili

## 💻 Esempi di Codice

### Polyfill per Number.isNaN()

```javascript
// Controlla se esiste già
if (!Number.isNaN) {
  Number.isNaN = function isNaN(x) {
    // NaN è l'unico valore non uguale a se stesso
    return x !== x;
  };
}

// Uso
console.log(Number.isNaN(NaN)); // true
console.log(Number.isNaN("ciao")); // false (meglio del vecchio isNaN)
```

### Polyfill per Array.prototype.includes()

```javascript
if (!Array.prototype.includes) {
  Array.prototype.includes = function (searchElement, fromIndex) {
    if (this == null) {
      throw new TypeError('"this" is null or not defined');
    }

    let array = Object(this);
    let len = array.length >>> 0;
    let k = Math.max(fromIndex >= 0 ? fromIndex : len - Math.abs(fromIndex), 0);

    while (k < len) {
      if (array[k] === searchElement) return true;
      k++;
    }
    return false;
  };
}
```

### Polyfill per String.prototype.startsWith()

```javascript
if (!String.prototype.startsWith) {
  String.prototype.startsWith = function (search, position) {
    position = position || 0;
    return this.indexOf(search, position) === position;
  };
}

let url = "https://example.com";
console.log(url.startsWith("https://")); // true
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Sovrascrivere implementazioni native**: Mai definire un polyfill senza il controllo `if (!feature)`
- ❌ **Polyfill incompleti**: Alcuni polyfill replicano solo parte del comportamento ufficiale
- ❌ **Performance**: I polyfill sono generalmente più lenti delle implementazioni native
- ❌ **Edge cases**: Difficile replicare tutti i casi limite della specifica

## ✅ Best Practices

- ✓ **Usa librerie testate**: Preferisci `core-js`, `es6-shim`, o `polyfill.io` invece di scrivere polyfill custom
- ✓ **Pattern di guardia**: Sempre controllare se la funzionalità esiste prima di definirla
- ✓ **Documentazione**: Documenta quali polyfill usi e perché
- ✓ **Build separati**: Considera di servire polyfill solo ai browser che ne hanno bisogno
- ✓ **Testing**: Testa i polyfill su browser vecchi reali, non solo su emulatori

## 🔗 Collegamenti

**Prerequisiti**:

- [[scope.md|Scope e Variabili Globali]]
- [[prototipi.md|Prototipi e Prototype Chain]]

**Concetti Correlati**:

- [[transpiling.md|Transpiling]]
- [[non-javascript.md|Non-JavaScript e API del Browser]]

**Approfondimenti**:

- Feature detection
- Progressive enhancement
- Browser compatibility

## 📚 Riferimenti

- [MDN - Polyfill](https://developer.mozilla.org/en-US/docs/Glossary/Polyfill)
- [core-js](https://github.com/zloirock/core-js)
- [polyfill.io](https://polyfill.io/)
- [ES5-Shim](https://github.com/es-shims/es5-shim)
- [ES6-Shim](https://github.com/es-shims/es6-shim)

## 📌 Note Personali

I polyfill sono essenziali quando si vuole usare funzionalità moderne mantenendo la compatibilità con browser vecchi. Tuttavia, con l'avanzare del tempo e la dismissione di vecchi browser (es. IE11), la necessità di polyfill si riduce. Le moderne build tool permettono di includere automaticamente solo i polyfill necessari basandosi sui browser target del progetto.

---

**Tags**: `#javascript` `#fondamenti` `#compatibilità` `#polyfill` `#es6` `#browser`
