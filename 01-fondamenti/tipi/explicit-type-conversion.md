# [[../../appunti-completi#13-conversione-di-tipo|Conversione di Tipo Esplicita per Primitivi]]

L'esigenza di far transitare un dato primitivo tra i tipi base in maniera controllata ed espressamente definita in JavaScript prende il nome tipico di conversione esplicita o *type casting*.

## Conversione Esplicita a Number

Esistono approcci diversi per forzare un valore primitivo verso un dominio tipizzato numerico.

### Operatore Unario +

La prassi concisa e diffusa è tramite l'operatore matematico unario `+`. Tenta la conversione dell'intero operando come un numero, compresa la parte ad eventuale virgola mobile, e riducendo i domini a `NaN` quando errati.

```javascript
let str = "42";
let num = +str; // 42

console.log(+"99.99"); // 99.99
console.log(+true); // 1
console.log(+false); // 0
console.log(+""); // 0
console.log(+"testo"); // NaN
```

### Funzioni parseFloat e parseInt

Le global functions di parsing estraggono il valore numerico scartando gli argomenti letterali restanti a seguire della parte interpretabile.

```javascript
// parseInt(string, radix)
console.log(parseInt("42.99")); // 42 (estrae solo intera)
console.log(parseInt("42px")); // 42 (ignora il resto non numerico)

// parseFloat(string)
console.log(parseFloat("99.99€")); // 99.99
```

### Funzione Costruttrice Omissiva (Number)

Richiamata senza la direttiva `new`, porta ad eseguire coercizione esplicita affine all'operatore unario di cui sopra.

```javascript
console.log(Number("42")); // 42
console.log(Number("42px")); // NaN (stringa non valida diversamente da parseInt)
console.log(Number(true)); // 1
```

## Conversione Esplicita a String

### Funzione Costruttrice Omissiva (String)

La transizione sicura di base si esegue chiamando la function preposta priva dell'operatore `new`. Aderisce in assenza di trappole e protegge nei casi di istruzioni sui blocchi vuoti.

```javascript
console.log(String(42)); // "42"
console.log(String(true)); // "true"
console.log(String(null)); // "null"
console.log(String(undefined)); // "undefined"
console.log(String([1, 2])); // "1,2"
```

### Il Metodo .toString()

Le variazioni native di molti prototipi possiedono un override del metodo `.toString()`. È tuttavia carente se invocato sui domini vuoti base per le restrizioni sulle proprieta di riferimento.

```javascript
let num = 42;
console.log(num.toString()); // "42"
console.log(true.toString()); // "true"

// ❌ Errori in assenza del wrapper appropriato
// null.toString();      // TypeError
// undefined.toString(); // TypeError
```

Si raccomanda l'uso di `String()` in scenari dove le variabili non siano controllate, per escludere blocchi fatali.

## Collegamenti

- [[coercizione]] - Differenza con la conversione implicita legata alle espressioni miste
- [[boxing-concept]] - Per il calcolo tramite wrapping temporaneo sulle stringhe
