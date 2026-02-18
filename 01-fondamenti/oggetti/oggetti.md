# [[../../appunti-completi#36-oggetti-objects|Oggetti (Objects)]]

Il tipo **object** è un valore composto che raggruppa dati e funzionalità correlate. Organizza i dati come collezione di **proprietà** (coppie chiave-valore).

## Creazione e Accesso

```javascript
// Definizione oggetto
let persona = { nome: "Mario", eta: 30, isAttivo: true };

// Dot notation (più comune)
console.log(persona.nome); // "Mario"

// Bracket notation (proprietà con spazi o variabili)
let campo = "eta";
console.log(persona[campo]); // 30 (accesso dinamico)
```

## Manipolazione Proprietà

```javascript
let auto = { marca: "Fiat", modello: "500" };

auto.anno = 2020; // Aggiungere
auto.anno = 2021; // Modificare
delete auto.anno; // Eliminare (sconsigliato per performance)
```

## Performance: Fast vs Dictionary

- **Oggetti "Fast"**: Struttura stabile → ottimizzati con hidden classes
- **Oggetti "Dictionary"**: Struttura mutata con `delete` → più lenti

## Alternative Immutabili a delete

**Destrutturazione (raccomandato)**:

```javascript
let persona = { nome: "Mario", eta: 30, email: "mario@example.com" };

// Rimuovere email creando nuovo oggetto
let { email, ...personaSenzaEmail } = persona;
console.log(personaSenzaEmail); // { nome: 'Mario', eta: 30 }
```

**Object.entries + filter**:

```javascript
let personaPubblica = Object.fromEntries(
  Object.entries(persona).filter(([chiave]) => chiave !== "email"),
);
```

## Oggetti come Riferimenti

Le variabili contengono **riferimenti** agli oggetti, non i valori diretti.

```javascript
let obj1 = { x: 10 };
let obj2 = obj1; // stesso riferimento

obj2.x = 20;
console.log(obj1.x); // 20 (modificato tramite obj2)

// Oggetti identici ma riferimenti diversi
let a = { x: 10 };
let b = { x: 10 };
console.log(a === b); // false (diversi in memoria)

// Copia indipendente (shallow)
let copia = { ...obj1 };
copia.x = 30;
console.log(obj1.x); // 20 (originale non modificato)
```

## Collegamenti

- [[tipi/valori-tipi]] - Object è uno dei tipi fondamentali
- [[tipi/tipizzazione-dinamica]] - Le proprietà possono avere qualsiasi tipo
- [[tipi/coercizione]] - Conversione da/verso oggetti
- [[array/array]] - Array sono oggetti speciali per collezioni ordinate
- [[funzioni/funzioni]] - Le funzioni sono oggetti speciali
