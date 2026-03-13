# [[../../appunti-completi#scope-annidato-nested-scope|La Metafora dell'Edificio nello Scope]]

La scope chain in JavaScript può essere visualizzata in modo intuitivo come un **edificio a più piani**. Questo stratagemma visivo è vitale per comprendere le gerarchie di blocco e funzione:

- **Piano terra** = Scope corrente (dove si esegue il codice nel momento specifico).
- **Piani superiori** = Scope esterni, ovvero i contenitori di quel blocco/funzione.
- **Attico** = Scope globale (ultimo piano).

Se l'Engine cerca un identificatore "prende l'ascensore" e parte dal piano dove si trova, salendo in cascata verso le zone superiori alla ricerca del riferimento giusto.

```javascript
// EDIFICIO CON 4 PIANI
let piano4 = "Attico - Globale"; // Piano 4 (Top)

function entraNelPalazzo() {
  let piano3 = "Terzo piano"; // Piano 3

  function scendiAlSecondo() {
    let piano2 = "Secondo piano"; // Piano 2

    function scendiAlPrimo() {
      let piano1 = "Piano terra"; // Piano 1 (Ground)

      // Dal piano terra, l'Engine può salire fino all'attico
      console.log(piano1); // ✅ Piano corrente (non serve l'ascensore)
      console.log(piano2); // ✅ Sale di 1 piano
      console.log(piano3); // ✅ Sale di 2 piani
      console.log(piano4); // ✅ Sale di 3 piani (attico)
    }

    scendiAlPrimo();

    // Dal secondo piano NON si può scendere al piano terra
    // console.log(piano1); // ❌ L'ascensore va solo verso l'alto!
  }

  scendiAlSecondo();
}

entraNelPalazzo();
```

**Regola chiave**: L'ascensore va **solo verso l'alto** (verso scope esterni), mai verso il basso. Questa restrizione unidirezionale garantisce che gli scope interni abbiano accesso al contesto esterno, ma gli scope esterni non possano interferire con lo stato interno (concetto di incapsulamento). Si tratta di un principio fondamentale per isolare lo stato in JavaScript.
