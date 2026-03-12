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

### 4. Semplicità Estrema e Praticità

Mantenere il linguaggio **il più semplice, chiaro e colloquiale possibile** (pur restando tecnicamente corretti).
Non stiamo scrivendo un romanzo o una tesi universitaria, ma degli appunti pratici.

> **Eccezione**: Se un termine leggermente più "alto" o specifico risulta essere l'unico modo perfetto e inequivocabile per descrivere un concetto (dove parole troppo comuni creerebbero confusione o farebbero perdere precisione tecnica), è ovviamente consentita l'eccezione lessicale.

- ✅ Usare parole dirette e di uso comune di default ("creare", "bloccare", "nascondere")
- ✅ Spiegare i concetti come se li si stesse raccontando a un collega a voce (mantenendo la 3ª persona)
- ❌ **Evitare** l'abuso di termini barocchi o puramente accademici se esiste un'alternativa semplice altrettanto valida (es. evitare "forgiare" se basta "creare", evitare "inibire" se basta "bloccare")
- ❌ Evitare strutture di frase troppo lunghe, complesse o contorte

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

### 9. Sintesi e Rielaborazione (Priorità Assoluta)

Dare **sempre la precedenza alla sintesi e alla rielaborazione** del testo. Evitare traduzioni letterali prolisse. L'obiettivo è estrarre il nocciolo tecnico del concetto e spiegarlo in termini semplici e diretti.

> **Eccezione (Casi Limite)**: Laddove un concetto è già brevissimo di per sé, e un'ulteriore sintesi rischierebbe solo di perderne il significato o peggiorarne l'efficacia, è consentito effettuare una traduzione diretta (sempre rispettando la regola della terza persona). **Questa deve rimanere una strictly eccezione e mai la prassi di default.**

- ✅ Elaborare il testo originale e concettualizzarlo
- ✅ Mantenere tutti i dettagli tecnici essenziali e gli esempi di codice, ma rimuovere verbosità e aria fritta
- ✅ Trasformare paragrafi discorsivi lunghi in spiegazioni concise ed efficaci
- ✅ Convertire lo stile in forma impersonale ("si può", "è necessario", "si consideri")
- ❌ NON fare traduzioni letterali 1:1 o mantenere l'enfasi narrativa manualistica dell'autore originale (salvo l'eccezione descritta sopra)
- ❌ NON mantenere la prolissità se il concetto è spiegabile in meno parole
- ❌ NON lasciare contenuti in inglese (salvo limitatissimi termini tecnici)

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
