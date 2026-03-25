# [[../../appunti-completi#87-cos-e-in-un-nome-l-eredita-prototipale-e-la-delega|Ereditarietà Prototipale e Delega]]

In JavaScript non si producono copie delle proprietà da un oggetto (come fosse una "classe") a un altro (una "istanza"). Tramite il meccanismo del `[[Prototype]]`, vengono creati semplicemente dei **collegamenti** tra gli oggetti.

Chiamare questo meccanismo **Ereditarietà Prototipale** crea molta confusione. La parola "ereditarietà" implica un'operazione di copia. Aggiungere il termine "prototipale" per indicare un comportamento che è quasi l'esatto opposto nel mondo JavaScript, è come chiamare una mela "arancia rossa".

Poiché JavaScript non copia nulla nativamente ma crea collegamenti che permettono a un oggetto di appoggiarsi a un altro per l'accesso a determinate proprietà o funzioni, il termine molto più accurato è **Delega** (Delegation).

![Pattern Delegation](../../../assets/whats_in_a_name.png)

Un altro termine spesso usato è **Ereditarietà Differenziale**, cioè l'idea di descrivere un oggetto solo in base alle differenze rispetto a un modello base predefinito, unendoli concettualmente in un unico blocco.

Tuttavia, anche questo modello mentale sbaglia: in JavaScript non avviene alcun appiattimento in stile copia. Un oggetto viene creato con le sue specifiche caratteristiche affiancate a dei veri e propri "buchi" (parti non definite). Sono esattamente questi spazi vuoti che la Delega riempie "al volo", andando a rintracciare e fornire quel comportamento richiesto tramite l'oggetto collegato. La **Delega** descrive perfettamente la realtà fisica di ciò che fa il linguaggio, senza appoggiarsi a modelli mentali fittizi.

## 🔗 Collegamenti

**Prerequisiti**:

- [[illusione-classi|L'Illusione delle Classi e le Funzioni Costruttrici]]
