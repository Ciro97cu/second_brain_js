# [[../../appunti-completi#73-i-meccanismi-delle-classi-in-javascript|I Meccanismi delle "Classi" in JS]]

A prescindere dall'apparente architettura di facciata, il nucleo di JavaScript **non implementa** il reale paradigma basato su classe fornito da linguaggi affini (es. Java o C++). Tutta l'impalcatura che avvolge la concezione a classe si presenta unicamente come sintassi cosmetica.

## 🎯 Concetti Chiave

- **Syntactic Sugar**: Keywords come `new` o la successiva adozione di `class` introdotta da ES6 furono inserite in modo esplicito per accontentare un'utenza largamente abituata alla programmazione procedurare rigorosa, mascherando una differente operatività dei componenti sottostanti.
- **Forzatura e Attriti**: Dal momento che adoperare il paradigma a _class pattern_ costituisce una mera scelta di programmazione mascherata all'interno del linguaggio, insistere nella simulazione di un ecosistema puramente OO non affine al _behavior delegation_ di JS può condurre a frizioni architetturali del programma causando bug o codici difficilmente mantenibili.

## ⚠️ Gotcha / Errori Comuni

- ❌ **Equiparazione con linguaggi ad Orientamento Forte**: Scrivere Classi in JS e aspettarsi il comportamento rigoroso, privato e strettamente ereditario visto in altri linguaggi induce fortemente allo scontro con il runtime Javascript. La struttura in superficie che si appresta al design delle classi non corrisponde affatto all'ingranaggio che realmente fa muovere le proprietà degli oggetti (prototipi).

## 🔗 Collegamenti

**Prerequisiti**:

- [[teoria-classi]]

**Concetti Correlati**:

- [[istanziazione]]

---

**Tags**: `#javascript` `#classi` `#OO` `#pattern` `#design`
