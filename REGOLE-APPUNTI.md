# Regole per la Scrittura degli Appunti

## Workflow

1. **Fase 1**: L'utente passa il testo in INGLESE dal libro "You Don't Know JS"
2. **Fase 2**: Scrivere appunti in ITALIANO in `appunti-completi.md` seguendo le regole sotto
3. **Fase 3**: L'utente ripassa gli appunti scritti
4. **Fase 4**: Creare/aggiornare i file atomici del second brain

> **IMPORTANTE**: Non creare i file del second brain finché l'utente non ripassa gli appunti della Fase 2. Questo evita operazioni troppo lunghe.

## Regole di Scrittura

### 1. Titolo del Topic

Ogni blocco deve iniziare con un titolo chiaro che identifichi l'argomento.

- Esempio: "Scope Lessicale"

### 2. Terza Persona

Scrivere **rigorosamente in terza persona** in TUTTI i casi, incluse le traduzioni dirette.

- ✅ "Si osserva che..."
- ✅ "L'Engine esegue..."
- ✅ "Questo permette di..."
- ✅ "È possibile utilizzare..."
- ❌ "Osserviamo che..."
- ❌ "Eseguiamo..."
- ❌ "Possiamo utilizzare..."
- ❌ "Puoi usare..." o "You can use..."

**IMPORTANTE**: Non tradurre mai letteralmente la seconda persona dall'inglese. Convertire sempre:

- "you can" → "si può" / "è possibile"
- "we need to" → "è necessario" / "si deve"
- "let's consider" → "si consideri" / "considerando"

### 3. Stile Discorsivo

Prediligere **paragrafi fluidi** e spiegazioni narrative.

- Evitare elenchi puntati eccessivi
- Usare bullet points solo per enumerazioni tecniche necessarie
- Preferire la narrazione continua

### 4. Semplicità

Mantenere il linguaggio **semplice, chiaro e diretto**.

- Evitare complessità non necessarie
- Spiegare i concetti in modo accessibile

### 5. Termini Tecnici

**Mantenere in inglese** i termini chiave dell'ecosistema JavaScript:

- Scope
- Hoisting
- Closure
- Event Loop
- Compiler
- Engine
- Lexical Scope
- Runtime
- Callback
- ecc.

### 6. Commenti nel Codice

Utilizzare **commenti multilinea** `/* ... */` per le spiegazioni estese all'interno degli snippet di codice.

```javascript
/*
 * Spiegazione del concetto
 * su più righe
 */
```

### 7. Esempi di Codice

- L'utente fornirà gli esempi di codice
- Valutare se è necessario ampliarli (generalmente non dovrebbe servire)
- Includere sempre snippet pratici a supporto della teoria quando necessario

### 8. Posizionamento

Prestare **attenzione al corretto posizionamento** degli appunti in `appunti-completi.md`:

- Rispettare la struttura esistente
- Inserire nel capitolo/sezione appropriati
- Mantenere la numerazione coerente

### 9. Traduzione Diretta

Se il concetto è breve e non vale la pena riassumerlo, **tradurlo direttamente** in italiano mantenendo tutti i dettagli. (è sempre preferibile riassumere in termini più semplici il concetto)

- ✅ Tradurre tutto il contenuto originale
- ✅ Mantenere esempi e spiegazioni complete
- ✅ **SEMPRE in terza persona** anche nella traduzione diretta
- ✅ Convertire lo stile: "you can" → "si può", "we need" → "è necessario"
- ❌ NON sintetizzare o tagliare parti
- ❌ NON lasciare contenuti in inglese
- ❌ NON mantenere seconda persona ("puoi", "possiamo")

### 10. Gestione Duplicazioni

Se un concetto è già stato spiegato in una sezione precedente degli appunti, **NON ripeterlo**. Invece:

- ✅ Inserire un link di riferimento alla sezione dove è già spiegato
- ✅ Usare la sintassi Markdown: `[testo descrittivo](#anchor-della-sezione)`
- ✅ Fornire un breve contesto prima del link

**Formato consigliato**:

```markdown
> **Nota**: Per i dettagli su [concetto], si veda [la sezione dedicata](#nome-sezione).
```

o

```markdown
> **Approfondimento**: Il meccanismo di [concetto] è spiegato in dettaglio in [sezione X.Y](#nome-sezione).
```

**Esempio pratico**:

```markdown
> **Nota**: Per i dettagli sul bug di typeof null, si veda [la sezione 3.1 "I Casi Particolari: null e undefined"](#i-casi-particolari-null-e-undefined).
```
