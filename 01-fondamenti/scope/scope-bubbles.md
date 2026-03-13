# [[../../appunti-completi#le-bolle-di-scope-annidate|Bolle di Scope]]

Le **bolle di scope** rappresentano visivamente gli scope annidati: ogni funzione o blocco crea una "bolla" contenuta in quella esterna.

## 🎯 Concetto Chiave

Lo scope può essere visualizzato come **bolle annidate** l'una dentro l'altra. Ogni bolla rappresenta uno scope e può contenere altre bolle più piccole.

### Gerarchia delle Bolle

```javascript
// ESEMPIO CON 3 BOLLE
function foo(a) {
  // Bolla 2: contiene a, b, bar
  let b = a * 2;

  function bar(c) {
    // Bolla 3: contiene c
    console.log(a, b, c);
  }

  bar(b * 3);
}

foo(2); // Bolla 1 (Globale): contiene foo
```

**Struttura**:

1. **Bolla 1 (Globale)** → Contiene `foo`
2. **Bolla 2 (foo)** → Contiene `a`, `b`, `bar`
3. **Bolla 3 (bar)** → Contiene `c`

**Regola fondamentale**: Una bolla è sempre **interamente contenuta** in un'altra, mai parzialmente.

## 💻 Visualizzazione Completa

```javascript
// BOLLE ANNIDATE: 4 livelli
let globale = "Bolla 1 (Attico)";

function livello1() {
  let locale1 = "Bolla 2";

  function livello2() {
    let locale2 = "Bolla 3";

    function livello3() {
      let locale3 = "Bolla 4 (Piano Terra)";

      // Dal piano terra, posso "salire" fino all'attico
      console.log(locale3); // ✅ Bolla corrente
      console.log(locale2); // ✅ Risale di 1 livello
      console.log(locale1); // ✅ Risale di 2 livelli
      console.log(globale); // ✅ Risale di 3 livelli
    }

    livello3();

    // Dal livello 2, posso salire ma NON scendere
    console.log(locale2); // ✅ Bolla corrente
    console.log(locale1); // ✅ Risale
    console.log(globale); // ✅ Risale
    // console.log(locale3); // ❌ Non posso scendere
  }

  livello2();
}

livello1();
```

## 🏗️ Contenimento Rigoroso

```javascript
// ✅ CORRETTO: Annidamento completo
function esterna() {
  // Bolla esterna
  let x = 10;

  function interna() {
    // Bolla interna DENTRO esterna
    console.log(x); // Accede a bolla esterna
  }
}

// ❌ IMPOSSIBILE: Bolla parzialmente in due scope
// Una funzione non può essere "metà" in uno scope e "metà" in un altro
```

## ✅ Best Practices

**Visualizza le bolle mentalmente**: Aiuta a capire quali variabili sono accessibili.

```javascript
// ✅ Chiara gerarchia
function elabora() {
  // Bolla elabora
  let dati = [1, 2, 3];

  function trasforma(item) {
    // Bolla trasforma, dentro elabora
    return item * 2; // Può accedere a 'dati' (bolla esterna)
  }

  return dati.map(trasforma);
}
```

**Evita troppi livelli**: Difficile tracciare le bolle.

```javascript
// ❌ Troppo annidato
function a() {
  function b() {
    function c() {
      function d() {
        // Quale bolla?
      }
    }
  }
}

// ✅ Struttura piatta
function processa(input) {
  const risultato = trasforma(input);
  return valida(risultato);
}
```

## 🔗 Collegamenti

- [[scope-lookup]] - Processo di ricerca nelle bolle
- [[lexical-scope-base]] - Scope lessicale base
- [[nested-scope]] - Scope annidati

## 📌 Note Aggiuntive

- La metafora delle **bolle** rende intuitivo lo scope annidato
- Ogni funzione o blocco crea una nuova bolla
- Le bolle rappresentano la struttura **lessicale** (definita alla scrittura)
