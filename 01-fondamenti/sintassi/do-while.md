# Ciclo do...while

**Appunti Completi**: [[../../appunti-completi#28-cicli-loops]]

Il ciclo `do...while` è molto simile al `while`, ma con una differenza cruciale: la condizione viene controllata **dopo** ogni iterazione.

Questo garantisce che il blocco di codice venga eseguito **almeno una volta**, anche se la condizione iniziale è falsa.

## Sintassi

```javascript
/*
 * Sintassi do...while
 */

do {
  // codice eseguito almeno una volta
} while (condizione);
```

## Esempi

```javascript
/*
 * Esempio: eseguito almeno una volta
 */

let numero = 10;

do {
  console.log("Numero:", numero);
  numero++;
} while (numero < 5);

// Output: "Numero: 10"
// Il blocco viene eseguito una volta, poi la condizione (10 < 5) è falsa
```

## Confronto while vs do...while

```javascript
/*
 * while - può non eseguire mai
 */

let a = 10;

while (a < 5) {
  console.log("while:", a); // MAI eseguito
}

/*
 * do...while - esegue almeno una volta
 */

let b = 10;

do {
  console.log("do...while:", b); // Eseguito UNA volta
} while (b < 5);

// Output:
// "do...while: 10"
```

## Casi d'Uso

Il `do...while` è utile quando:

- Il blocco deve essere eseguito **almeno una volta**
- Menu interattivi che devono mostrare le opzioni almeno una volta
- Validazione input dove si chiede almeno una volta

```javascript
/*
 * Esempio: menu interattivo
 */

let scelta;

do {
  console.log("1. Opzione A");
  console.log("2. Opzione B");
  console.log("3. Esci");
  scelta = prompt("Scegli un'opzione:");

  // Elabora scelta...
} while (scelta !== "3");
```

## Collegamenti

- [[while]] - Ciclo while (controlla condizione prima)
- [[for]] - Ciclo for (quando il numero di iterazioni è noto)
- [[break-continue]] - Interrompere o saltare iterazioni
- [[condizionali]] - Istruzioni condizionali
