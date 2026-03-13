# [[../../../appunti-completi#311-lidentificatore-this|Default Binding (Gotchas e Prassi Comuni)]]

Nel tracciamento della default binding di `this` è imperativo prestare attenzione ad alcune anomalie di sintassi, così come favorire l'impiego di accorgimenti protettivi in fase di stipulazione dei costrutti e della logica globale del programma JavaScript.

## Confusione tra const, let e var

Nelle versioni pregresse di JS, la keyword `var` deteneva il monopolio sulle dichiarazioni nello scope globale, causando la consequenziale materializzazione delle relative variabili quali attributi del _global object_ adiacente (es. `window`). Sebbene codesta associazione simbiotica permanga vera ancora oggi per la keyword `var`, un comportamento divergente avviene in relazione alle odierne istruzioni `let` e `const`.

L'utilizzo di `let` e `const` nello scope globale **non porta alla genesi di una corrispettiva proprietà del global object**.

```javascript
let a = 2; // let NON crea proprietà sul global object.

function foo() {
  console.log(this.a); // Sarà undefined, e non 2!
}

foo();
```

Pertanto l'invocazione di `foo()`, la quale fa parimenti affidamento sulla default binding verso `global object`, fallirà nell'acquisizione del valore `2`, proprio per la mancata afferenza di `let a` all'agglomerato delle proprietà globali.

## IIFE e Default Binding

Come ogni "plain function call", anche una IIFE (Immediately Invoked Function Expression) obbedisce integralmente al meccanismo di default binding. Non essendo presente alcun binding implicito od esplicito applicato in adiacenza all'espressione sintattica di invocazione della funzione anonima, il `this` propenderà inequivocabilmente verso un fallback predefinito, obbedendo, allorquando non sussistano prescrizioni per la strict mode, al global object.

```javascript
var a = "global";

(function () {
  console.log(this.a); // Stampa "global" in deferenza alla default binding.
})();

(function () {
  "use strict";
  console.log(this); // Stampa undefined al subentrare delle regole di strict mode.
})();
```

## Best Practices Assodate

Il ricorso consapevole ai precetti protocollati permette di minimizzare le devianze applicative di the default binding:

1. **Predilezione per la strict mode**: Garantisce l'inibizione dell'assegnazione accidentale del global object, tutelando altresì l'applicazione da interazioni collaterali inattese tra scope indipendenti.
2. **Astensione da una esplicita dipendenza dalla default binding**: Evitando l'uso congiunto e reiterato di funzioni slegate per la mutazione diretta del global object risulta più ostica l'insorgenza di imprevisti o side effects spuri.
3. **Esplicitazione del contesto**: Nel caso d'uso ove sia comprovato ed eludibile il bisogno del riferimento al global object, diviene preferibile disporne sotto forma di parametro in ingresso alla procedura interessata in sostituzione della cieca e non deterministica acquisizione di un globale ambientale.

---

**Tags**: `#javascript` `#this` `#default-binding` `#best-practices`
