# [[../../appunti-completi#Coercizione Booleana Implicita|Coercizione Booleana Implicita]]

In JavaScript, quando un valore non booleano viene utilizzato in un **contesto che si aspetta un booleano** (come la condizione di un `if`, l'operando di un operatore logico o un ciclo), il linguaggio lo converte implicitamente in `true` o `false`.

Questo processo è noto come **coercizione booleana implicita**.

## Meccanismo di Base

Il motore JavaScript applica internamente la funzione astratta `ToBoolean` ai valori che necessitano di conversione. In base al risultato di questa operazione, i valori vengono classificati in due categorie fondamentali:

- **Falsy**: valori che si convertono in `false`.
- **Truthy**: valori che si convertono in `true`.

## Contesti di Coercizione

La coercizione booleana avviene automaticamente in specifici contesti sintattici e operazionali:

1. **Istruzioni condizionali**: all'interno della guardia di un `if` o di un `else if`.
2. **Cicli**: nelle condizioni di terminazione di `for`, `while`, e `do...while`.
3. **Operatori logici**: negli operandi degli operatori `&&` (AND), `||` (OR) e `!` (NOT).
4. **Operatore ternario**: nella condizione antecedente al simbolo `?`.

```javascript
/*
 * Esempi di coercizione implicita
 */

// Contesto if
let nomeUtente = "Mario";
if (nomeUtente) { // La stringa "Mario" è truthy
  console.log("Variabile valorizzata");
}

// Contesto cicli
let array = [1, 2, 3];
while (array.length) { // array.length > 0 è truthy, 0 è falsy
  array.pop();
}

// Contesto operatori logici
let configurazione = configUtente || configDefault;
```

Nel caso dell'operatore logico OR (`||`), il meccanismo restituisce il primo operando se esso risulta truthy, altrimenti restituisce il secondo operando, sfruttando direttamente la coercizione per assegnare valori di fallback.

## Differenza con l'Uguaglianza

È fondamentale distinguere la coercizione booleana pura (come nel caso degli `if`) dal comportamento dell'operatore di uguaglianza debole (`==`).

Il controllo di truthy/falsy non corrisponde all'uguaglianza con `true` o `false`. Ad esempio, un array vuoto `[]` è truthy in un costrutto `if`, ma il confronto `[] == true` restituisce `false` a causa delle regole complesse di coercizione dell'operatore `==`.

L'uso di `===` o della conversione esplicita evita queste ambiguità:

```javascript
// Array vuoto è truthy nell'if
let arrayVuoto = [];
if (arrayVuoto) {
  console.log("Eseguito"); // Eseguito
}

// Confronto diretto con uguaglianza debole fallisce
console.log([] == true); // false
```
