# [[../../appunti-completi#311-lidentificatore-this|Il Concetto di this]]

La keyword `this` è uno dei meccanismi più fraintesi in JavaScript. Si tratta di un identificatore speciale definito automaticamente nello scope di ogni funzione. Il suo valore dipende esclusivamente da **come** la funzione viene chiamata (call-site).

## 🎯 Concetti Chiave

- **Binding dinamico (Runtime)**: È determinato al momento dell'invocazione, non al momento della dichiarazione.
- **Contesto Implicito**: Fornisce un modo elegante per operare su oggetti multipli senza passare esplicitamente il loro riferimento come parametro, favorendo API pulite e il riutilizzo del codice.
- **Quattro Regole**: Il suo valore viene deciso attraverso 4 regole di binding rigorose (Default, Implicit, Explicit, New). 

## 💡 Perché this Esiste

Il meccanismo `this` permette la condivisione di metodi tra oggetti diversi senza dover duplicare la funzione per ciascun oggetto o doverne esplicitare il passaggio come parametro fisso (es: `function(context)` rispetto all'uso dinamico).

## ⚠️ Le Confusioni Comuni (Cosa NON è this)

Prima di studiarne il funzionamento, è vitale rimuovere due assunzioni errate:
1. **NON punta alla funzione stessa**: Approfondisci l'errore in [[this-confusion-itself]]
2. **NON punta al Lexical Scope della funzione**: Non funge in alcun modo da "ponte" per le variabili dello scope di definizione. Approfondisci in [[this-confusion-scope]]

## 🔗 Approfondimenti Correlati

- [[this-call-site]] - Comprendere il punto di chiamata ed il Call-Stack
- [[this-binding-rules]] - Le 4 Regole del Binding di this 
- [[this-arrow-functions]] - L'identificatore this lessicale
- [[this-binding-problems]] - Smarrimento del this e pattern avanzati

---

**Tags**: `#javascript` `#this` `#binding` `#context` `#oggetti`
