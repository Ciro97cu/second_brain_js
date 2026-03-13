# [[../../appunti-completi#switch-strict-equality|Switch - Uguaglianza Stretta ed Espressioni]]

Il costrutto `switch` in JavaScript utilizza l'**uguaglianza stretta** (`===`) per operare le proprie conformità. Questo significa formalmente che non viene mai applicata alcuna coercizione di tipo implicita durante la disamina dei casi.

## Confronto Strict (`===`)

Poiché il controllo si attiene in modalità estremamente severa alle regole sintattiche, il confronto tra valori di tipo differente fallisce d'ufficio, sebbene gli stessi potessero risultare uguali avvalendosi dell'uguaglianza debole (`==`).

```javascript
let numero = "2"; // Tipo stringa

switch (numero) {
  case 2: // Tipo number
    console.log("Due (numero)"); // Non eseguito
    break;
  case "2": // Tipo stringa
    console.log("Due (stringa)"); // Viene eseguito
    break;
}
// Output: "Due (stringa)"
```

## Valutazione di Espressioni

Un blocco `switch` è persino idoneo alla valutazione di espressioni di calcolo al posto delle comunissime e più canoniche variabili non composte.

```javascript
let a = 5;
let b = 10;

switch (a + b) {
  case 10:
    console.log("La somma è 10");
    break;
  case 15:
    console.log("La somma è 15"); // Blocco eseguito
    break;
  default:
    console.log("Valore non riscontrato in archivio");
}
```

## Il Caso di Default

La clausola designata con etichetta `default` assume una dimensione protettiva. Viene infatti elaborata unicamente in ultima analisi quando alcun esito combacia. 
Non possedendo alcun obbligo di formattazione la si ritiene un requisito del tutto opzionale; pur ciononostante se ne raccomanda enormemente un uso mirato e massivo per far fronte in maniera robusta ed incensurabile all'emergenza logica derivante dei dati errati. Convenzionalmente sosta come ultima istruzione a base dello `switch`.
