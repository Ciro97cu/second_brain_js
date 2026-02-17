# Operatori Matematici (Arithmetic)

**Appunti Completi**: [[../../appunti-completi#5-operatori]]

Gli operatori matematici eseguono operazioni aritmetiche su valori numerici.

## Operatori Binari

- `+` → addizione (e concatenazione stringhe)
- `-` → sottrazione
- `*` → moltiplicazione
- `/` → divisione
- `%` → resto (remainder/modulo)
- `**` → esponenziazione

## Operatori Unari

- `++` → incremento di 1
- `--` → decremento di 1

## Caratteristiche Speciali

**Operatore +**: Ha doppio ruolo

- Con numeri: addizione
- Con stringhe: concatenazione
- Misto: converte numero a stringa e concatena

**Operatore %**: Restituisce il resto della divisione, utile per:

- Verificare numeri pari/dispari
- Operazioni cicliche

**Incremento/Decremento**: Hanno due forme

- Pre-incremento: `++x` (incrementa, poi usa il valore)
- Post-incremento: `x++` (usa il valore, poi incrementa)

## Esempio di Riferimento

```javascript
/* Operatori matematici */

// Addizione
let somma = 5 + 3; // 8
let totale = 10 + 20 + 5; // 35

// Concatenazione stringhe
let saluto = "Ciao" + " " + "mondo"; // "Ciao mondo"
let mix = "Numero: " + 42; // "Numero: 42"

// Sottrazione, moltiplicazione, divisione
let differenza = 10 - 3; // 7
let prodotto = 6 * 7; // 42
let quoziente = 20 / 4; // 5
let decimale = 10 / 3; // 3.3333333333333335

// Resto (remainder)
let resto = 17 % 5; // 2 (17 = 5*3 + 2)
let pari = 10 % 2; // 0 (numero pari)
let dispari = 11 % 2; // 1 (numero dispari)

// Esponenziazione
let potenza = 2 ** 3; // 8 (2³)
let quadrato = 5 ** 2; // 25

// Incremento e decremento
let contatore = 0;
contatore++; // 1
contatore++; // 2
console.log(contatore); // 2

let countdown = 10;
countdown--; // 9
console.log(countdown); // 9

// Pre vs Post incremento
let a = 5;
let b = a++; // b = 5, poi a diventa 6
console.log(a, b); // 6, 5

let c = 5;
let d = ++c; // c diventa 6, poi d = 6
console.log(c, d); // 6, 6

// Uso pratico del resto
function isPari(n) {
  return n % 2 === 0;
}
console.log(isPari(10)); // true
console.log(isPari(7)); // false

// Ciclo con resto (index modulare)
let giorni = ["Lun", "Mar", "Mer", "Gio", "Ven", "Sab", "Dom"];
let giornoCorrente = 15;
let nomeGiorno = giorni[giornoCorrente % 7]; // 15 % 7 = 1 → "Mar"
```

## Punti Chiave

1. **+**: Unico operatore con doppio ruolo (addizione/concatenazione). Se uno degli operandi è stringa, esegue concatenazione

2. **Divisione**: In JavaScript restituisce sempre un numero decimale (non arrotonda)

3. **% (resto)**: Utile per verificare multipli, numeri pari/dispari, operazioni cicliche

4. **++/--**: Attenzione alla posizione (pre vs post). Nella pratica comune, preferire `x++` o `x--` come istruzioni separate

5. **Ordine**: Seguono la precedenza matematica standard (`*`, `/`, `%` prima di `+`, `-`)

## Collegamenti

- [[operatori/assegnamento]] - Operatori composti combinano matematica e assegnamento
- [[operatori/precedenza]] - Ordine di valutazione delle operazioni
- [[../tipi/valori-tipi]] - Gli operatori matematici lavorano principalmente con number
