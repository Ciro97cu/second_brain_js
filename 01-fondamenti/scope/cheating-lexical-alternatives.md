# [[../../appunti-completi#barare-con-lo-scope-lessicale-cheating-lexical|Scope Lessicale: Alternative alle Modifiche Dinamiche]]

## ✅ Approcci Moderni e Sicuri

Modificare lo scope lessicale a runtime tramite `eval()` o `with` causa inefficienze e problemi di sicurezza. Per ottenere risultati simili, i moderni standard JavaScript offrono alternative più eleganti e performanti.

## 🔄 Alternative a eval()

Invece di eseguire stringhe di testo come codice dinamico, è preferibile ricorrere a funzioni o notazioni standard.

### Accesso a Proprietà Dinamiche

```javascript
var prop = "b";
var obj = { a: 1, b: 2 };

// ❌ Vecchio approccio con eval
eval("console.log(obj." + prop + ")");

// ✅ Bracket notation
console.log(obj[prop]);
```

### Calcoli Dinamici e Valutazione Espressioni

```javascript
// ❌ Uso pericoloso
var result = eval("2 + 2 * 3");

// ✅ Strumenti di parsing dedicati o, in estrema ratio, Function constructor
var calc = new Function("return 2 + 2 * 3");
var result = calc(); // 8
```

L'uso di librerie specializzate in parsing e interpretazione (come `math.js`) risulta la scelta più sicura.

### Esecuzione di Logica Dinamica

```javascript
// ❌ Approccio deprecato
eval("console.log('Hello')");

// ✅ Arrow functions e callback
const code = () => console.log("Hello");
code();
```

## 🔄 Alternative a with

L'assegnazione e la lettura ripetuta delle proprietà di un oggetto non richiedono il costrutto deprecato `with`.

### Lettura Valori

La sintassi di destructuring (ES6+) permette l'accesso pulito e compatto.

```javascript
var obj = { a: 1, b: 2, c: 3 };

// ❌ Con with
with (obj) {
  console.log(a, b);
}

// ✅ Destructuring
const { a, b } = obj;
console.log(a, b);
```

### Configurazione Valori

Per assegnazioni multiple, è preferibile l'uso esplicito dell'oggetto o un riferimento temporaneo.

```javascript
// ✅ Assegnazione diretta (ottimizzabile dall'engine)
obj.a = 2;
obj.b = 3;

// ✅ Riferimento temporaneo se l'espressione originaria è complessa
const target = user.data.preferences;
target.theme = "dark";
target.notifications = true;
```

Tali pratiche, diversamente dalle mutazioni dinamiche di scope, preservano le ottimizzazioni dell'engine (inline caching, lookup statico) e scongiurano i rischi derivanti dai global leak accidentali.

## 📚 Risorse

- MDN Web Docs: Destructuring assignment
- MDN Web Docs: Property accessors

## 📌 Tag

#javascript #scope #alternatives #destructuring #bracket-notation #best-practices
