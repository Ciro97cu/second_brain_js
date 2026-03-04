# [[../../appunti-completi#nascondere-nello-scope-hiding-in-plain-scope|Nascondere nello Scope (Hiding in Plain Scope)]]

## 🎯 Concetto

Invece di dichiarare una funzione e poi aggiungere codice, si può "avvolgere" del codice esistente in una funzione per **nasconderlo**. Questo crea una nuova "bolla di scope" che protegge variabili e funzioni dalla vista esterna.

**Principio del Minimo Privilegio**: Esporre solo ciò che è strettamente necessario, nascondendo i dettagli implementativi.

## 💻 Pattern Base

### Cattiva Pratica: Tutto Globale

```javascript
// ❌ Dettagli implementativi esposti
function doSomething(a) {
  b = a + doSomethingElse(a * 2);
  console.log(b * 3);
}

function doSomethingElse(a) {
  return a - 1;
}

var b; // Globale, modificabile da chiunque
```

### Buona Pratica: Dettagli Nascosti

```javascript
// ✅ Dettagli privati nello scope interno
function doSomething(a) {
  function doSomethingElse(a) {
    return a - 1; // Helper privato
  }

  var b;
  b = a + doSomethingElse(a * 2);
  console.log(b * 3);
}

// b e doSomethingElse NON accessibili dall'esterno
```

## 💡 Esempi Pratici

### API Pubblica con Dettagli Privati

```javascript
function creaContatore(iniziale) {
  let contatore = iniziale || 0; // PRIVATO

  function valida(valore) {
    // Helper PRIVATO
    return typeof valore === "number" && valore >= 0;
  }

  // API PUBBLICA
  return {
    incrementa: () => ++contatore,
    decrementa: () => (contatore > 0 ? --contatore : contatore),
    imposta: (val) => (valida(val) ? (contatore = val) : contatore),
    leggi: () => contatore,
  };
}

let c = creaContatore(10);
c.incrementa(); // 11
// c.contatore // undefined - protetto!
```

### Prevenzione Collisioni

```javascript
// ❌ PROBLEMA: Collisione di variabili
function foo() {
  function bar(a) {
    i = 3; // Sovrascrive la 'i' del for!
    console.log(a + i);
  }

  for (var i = 0; i < 10; i++) {
    bar(i * 2); // CICLO INFINITO!
  }
}
```

```javascript
// ✅ SOLUZIONE: Variabile locale (shadowing)
function foo() {
  function bar(a) {
    var i = 3; // Nuova variabile locale
    console.log(a + i);
  }

  for (var i = 0; i < 10; i++) {
    bar(i * 2); // Funziona correttamente
  }
}
```

## ⚠️ Quando Usare

1. **Protezione Dati**: Variabili che non devono essere modificate dall'esterno
2. **Prevenzione Collisioni**: Evitare conflitti di nomi con scope esterno
3. **Encapsulation**: Nascondere helper functions e stato interno
4. **Module Pattern**: Creare API pubbliche con implementazione privata

## ✅ Benefici

- **Sicurezza**: Dati interni non modificabili dall'esterno
- **Manutenibilità**: Cambiare implementazione senza rompere API pubblica
- **Debugging**: Scope ridotto = meno ricerca per bug
- **Design Robusto**: Interfacce chiare, dettagli nascosti

## 🔗 Concetti Correlati

- [[lexical-scope-base|Scope Lessicale]] - Meccanismo di base
- [[nested-scope|Scope Annidato]] - Come si creano le "bolle"
- [[scope-namespaces|Namespace Globali]] - Pattern a livello di libreria
- [[../../appunti-completi#nascondere-nello-scope-hiding-in-plain-scope|Hiding in Scope Completo]]

## 📚 Risorse

- "You Don't Know JS" - Scope & Closures, Chapter 3
- Principle of Least Privilege (Software Design)

## 📌 Tag

#javascript #scope #encapsulation #design-patterns #least-privilege #hiding #collision-avoidance
