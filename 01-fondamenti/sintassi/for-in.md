# Ciclo for...in

**Appunti Completi**: [[../../appunti-completi#28-cicli-loops]]

Il ciclo `for...in` è specifico per iterare sulle **proprietà enumerabili** di un oggetto.

Ad ogni iterazione, la variabile del ciclo assume il **nome** (la chiave) della proprietà corrente, come stringa.

## Sintassi

```javascript
/*
 * Sintassi for...in
 */

for (let chiave in oggetto) {
  // lavora con chiave
}
```

## Esempi con Oggetti

```javascript
/*
 * Iterare su oggetto
 */

let persona = {
  nome: "Mario",
  cognome: "Rossi",
  eta: 30,
};

for (let proprieta in persona) {
  console.log(proprieta + ":", persona[proprieta]);
}

// Output:
// "nome: Mario"
// "cognome: Rossi"
// "eta: 30"
```

## ⚠️ Importante: NON Usare con Array

`for...in` **non è raccomandato per array**.

```javascript
/*
 * for...in con array (SCONSIGLIATO)
 */

let numeri = [10, 20, 30];

for (let indice in numeri) {
  console.log(typeof indice); // "string" (!)
  console.log(indice, numeri[indice]);
}

// Output:
// "string"
// "0" 10
// "1" 20
// "2" 30

// Problemi:
// - indice è una stringa, non un numero
// - Potrebbe includere proprietà inaspettate
// - Non garantisce l'ordine
```

## ✅ Per Array, Usare for...of

```javascript
/*
 * for...of con array (CONSIGLIATO)
 */

let numeri = [10, 20, 30];

for (let numero of numeri) {
  console.log(numero);
}
```

## Tabella Riepilogativa

| Ciclo      | Uso                        | Itera su   |
| ---------- | -------------------------- | ---------- |
| `for...of` | Array, stringhe, iterabili | **Valori** |
| `for...in` | Oggetti                    | **Chiavi** |

## Casi d'Uso

Il `for...in` è ideale quando:

- Devi iterare sulle **proprietà** di un oggetto
- Ti servono i **nomi delle chiavi**
- Lavori con oggetti plain (non array, non iterabili)

```javascript
/*
 * Esempio pratico: contare proprietà
 */

let config = {
  debug: true,
  timeout: 5000,
  retries: 3,
};

let count = 0;
for (let key in config) {
  count++;
}

console.log("Numero di configurazioni:", count); // 3
```

## Collegamenti

- [[for-of]] - Ciclo for...of (per valori iterabili)
- [[for]] - Ciclo for tradizionale
- [[../oggetti/oggetti]] - Oggetti in JavaScript
- [[../array/array]] - Array (non usare for...in)
