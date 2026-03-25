# [[../../appunti-completi#811-linaffidabilita-della-proprieta-constructor|L'inaffidabilità della proprietà .constructor]]

L'uso di `a.constructor === Foo` nutre l'illusione fittizia secondo cui l'istanza `a` contenga un collegamento rigido verso il suo costruttore. In realtà la proprietà `.constructor` è solo una delega per indirizzamento, facilmente manipolabile e universalmente inaffidabile per gestire logiche di business nel linguaggio JavaScript.

## 🎯 Concetti Chiave

- **Risoluzione tramite Delega**: L'istanza creata con `new` non dispone quasi mai originariamente di una proprietà `.constructor`; cerca nella catena e trova quella istanziata di default nel prototipo padre.
- **Assegnazione di default fragile**: Il `.prototype` riceve la sua dotazione standard (incluso il `.constructor`) solo alla prima passata in memoria. Se l'intero oggetto proto viene successivamente riassegnato, il constructor default cade nel dimenticatoio.
- **Scalata a vuoto**: Perse le tracce del costruttore originale, le nuove istanze passano le richieste fino allo strato `Object.prototype.constructor`, ritornando così `Object` pur essendo state istanziate da un'altra funzione.

## 💻 Esempi di Codice

### Fallimento del Riferimento di Costruzione

```javascript
function Foo() {
  /* ... */
}

// Sostituzione irreversibile del prototipo originale
Foo.prototype = {
  /* ... */
};

const a1 = new Foo();

console.log(a1.constructor === Foo); // false!
console.log(a1.constructor === Object); // true!
```

## ⚠️ Gotcha / Errori Comuni

- ❌ **Design basati sul controllo del costruttore**: Creare controlli logici affidandosi all'assunto "questo oggetto è costruito da..." utilizzando `istanza.constructor`, una pratica che porta quasi sempre a bug architetturali a causa dell'alta volatilità del suo binding effettivo.

## ✅ Best Practices

- ✓ **Duck Typing e controlli sicuri**: Invece di far affidamento su `.constructor`, preferisci test e check più sicuri basati sulle feature/comportamenti effettivi di un oggetto (ad es. l'operatore `instanceof` gestito con cautela o il più sicuro Duck Typing) oppure valuta logiche strutturate e immutabili ove possibile.

## 🔗 Collegamenti

**Prerequisiti**:

- [[meccaniche-classi]]
- [[catena-prototipi]]

**Concetti Correlati**:

- [[costruttore]]

**Approfondimenti**:

- [[duck-typing]]

## 📚 Riferimenti

- Libro: "You Don't Know JS"
- Capitolo: Prototypes

## 📌 Note Personali

[Spazio per riflessioni, domande, applicazioni personali]

---

**Tags**: `#javascript` `#prototipi` `#constructor` `#delega`
