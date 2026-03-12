# 📋 Regole di Creazione del Second Brain JavaScript

> Documentazione completa delle regole per la creazione e manutenzione del sistema di gestione della conoscenza.

---

## 🎯 Architettura del Sistema

Questo Second Brain è composto da **due tipologie di contenuti**:

### 1. 📄 Appunti Completi (`appunti-completi.md`)

**Scopo**: Contenere i testi originali di studio rielaborati e sintetizzati senza perdite di profondità tecnica, senza stringenti limiti di lunghezza.

**Caratteristiche**:

- ✅ Contenuto SINTETIZZATO MA COMPLETO tecnicamente
- ✅ NESSUN limite di righe per sezione (espandi quanto serve per chiarezza)
- ✅ Includere esempi a codice laddove il testo lo prevede
- ✅ Nessuna verbosità inutile o traduzioni prolisse dei manuali
- ✅ **NON contiene link** verso i file atomici
- ✅ Serve da fonte di verità (source of truth)
- ✅ È il punto di riferimento completo per ogni argomento

**Struttura**:

```markdown
## X. Categoria Principale

### X.Y Nome Sezione

[Contenuto completo originale senza limiti]

#### Sottosezione

[Tutti i dettagli necessari]
```

**Esempi di lunghezza**:

- Una sezione può essere 30 righe o 300 righe
- Include TUTTI gli esempi di codice originali (generati dall'agente AI siccome durante il passaggio vengono persi)
- Spiega approfonditamente ogni concetto

---

### 2. 🗂️ Note Atomiche (File nelle cartelle `01-fondamenti/`, `02-funzioni/`, etc.)

**Scopo**: Sintesi rapide e consultabili dei concetti, organizzate per argomento.

**Caratteristiche**:

- ✅ Contenuto SINTETIZZATO
- ✅ **40-80 righe** di contenuto effettivo (100-130 righe totali inclusi header/footer)
- ✅ Focus su un singolo concetto (atomicità) - scompattare in più file e includere in cartelle se gli argomenti lo permettono
- ✅ **Contengono SEMPRE link** agli appunti completi
- ✅ Ottimizzate per consultazione rapida
- ✅ Seguono il template standard

**Template**: Vedi [TEMPLATE.md](TEMPLATE.md)

**Limiti di lunghezza**:

- Contenuto: 40-80 righe (codice + testo)
- Totale file: ~100-130 righe (con metadata, header, link)
- Se superi questo limite, il concetto va suddiviso

**Struttura titolo con link**:

```markdown
# [[../../appunti-completi#x-y-nome-sezione|Nome Sezione]]
```

Il titolo stesso è un link cliccabile agli appunti completi.

---

## 🔗 Sistema di Collegamento

### Regola Fondamentale: Direzione dei Link

```
┌─────────────────┐           ┌──────────────────────┐
│  File Atomico   │  ──────>  │  appunti-completi.md │
│  (sintesi)      │  SEMPRE   │  (fonte originale)   │
└─────────────────┘           └──────────────────────┘
```

**✅ CORRETTO**:

- File atomico contiene: `[[../../appunti-completi#29-strict-mode]]`
- File atomico → appunti completi

**❌ SBAGLIATO**:

- appunti-completi.md contiene: `[[01-fondamenti/strict-mode]]`
- appunti completi → file atomico (MAI!)

### Formato dei Link

**Da file atomico a appunti-completi**:

```markdown
[[../../appunti-completi#sezione-in-kebab-case]]
```

**Esempi**:

- `[[../../appunti-completi#29-strict-mode]]`
- `[[../../appunti-completi#311-lidentificatore-this]]`
- `[[../../appunti-completi#39-closure]]`

**Nota**: Gli anchor sono in formato `kebab-case` (tutto minuscolo con trattini).

---

## 📝 Processo di Creazione

### Workflow per Nuovi Contenuti

#### Step 1: Aggiungi agli Appunti Completi

1. Apri `appunti-completi.md`
2. Trova la sezione appropriata (es. `## 3. Tipi e Dati`)
3. Aggiungi il contenuto RIELABORATO SINTETICAMENTE ma completo tecnicamente
4. Elimina verbosità pur mantenendo viva la teoria, aggiungi esempi a codice laddove il testo lo permette
5. NON aggiungere link a file atomici

```markdown
### 3.13 Nuovo Concetto

[Spiegazione completa con tutti i dettagli, esempi, best practices]

#### Sottosezione

[Tutti gli approfondimenti necessari]
```

#### Step 2: Crea la Nota Atomica

1. Copia [TEMPLATE.md](TEMPLATE.md)
2. Salva in cartella appropriata: `01-fondamenti/nuovo-concetto.md`
3. Sostituisci il link e il testo del titolo
4. Sintetizza il contenuto (40-80 righe)
5. Collega ad altre note atomiche correlate

```markdown
# [[../../appunti-completi#313-nuovo-concetto|Nuovo Concetto]]

[Descrizione concisa del concetto]

## 🔗 Collegamenti

**Prerequisiti**:

- [[concetto-base]]

**Correlati**:

- [[concetto-simile]]
```

#### Step 3: Verifica

- [ ] Appunti completi contengono il testo ORIGINALE
- [ ] Note atomiche sono sintetizzate (40-80 righe)
- [ ] Link vanno da atomico → completo
- [ ] NO link da completo → atomico
- [ ] Anchor format corretto (kebab-case)

---

## 📐 Regole di Stile

### Per appunti-completi.md

**Metadata**:

```markdown
### 2.9 Nome Sezione

[Contenuto completo]
```

- ❌ NON usare `**Tipo**: Nuovo Topic`
- ❌ NON usare metadata aggiuntivo
- ✅ Titolo diretto con numerazione

**Link**:

- ❌ `[[01-fondamenti/strict-mode]]` (VIETATO)
- ✅ Nessun link interno a file atomici

### Per Note Atomiche

**Struttura** (da TEMPLATE.md):

```markdown
# [[../../appunti-completi#sezione|Nome Concetto]]

[Descrizione concisa del concetto]
```

**Caratteristiche**:

- Titolo H1 è un link cliccabile agli appunti completi
- Sintassi: `[[link|testo visualizzato]]`
- Descrizione breve direttamente sotto il titolo
- Sezioni organizzate con emoji (🎯, 💻, ⚠️, ✅, 🔗, 📚)

**Percorsi relativi per i link**:

- Da `01-fondamenti/`: usa `../../appunti-completi#sezione`
- Da sottocartelle `01-fondamenti/tipi/`: usa `../../../appunti-completi#sezione`

**Formato link nel titolo**:

```markdown
# [[percorso/appunti-completi#anchor|Testo Visualizzato]]
```

---

## 🗂️ Organizzazione Cartelle

### Struttura Standard

```
second_brain_js/
├── appunti-completi.md         # ← Testi originali completi
├── TEMPLATE.md                  # ← Template per note atomiche
├── REGOLE.md                    # ← Questo file
├── 01-fondamenti/
│   ├── INDEX.md
│   ├── variabili.md            # ← Sintesi 40-80 righe + link
│   ├── tipi/
│   │   ├── string.md
│   │   └── number.md
│   └── ...
├── 02-funzioni/
│   ├── INDEX.md
│   └── arrow-functions.md
└── ...
```

### Naming Convention

**File atomici**:

- `kebab-case.md`
- Descrittivi: `arrow-functions.md` non `af.md`
- Un concetto per file

**Anchor negli appunti completi**:

- `#29-strict-mode`
- `#311-lidentificatore-this`
- Numerazione + kebab-case

---

## ✅ Checklist di Validazione

### Per Appunti Completi

- [ ] Contenuto rielaborato, senza enfasi prolisse
- [ ] Nessun limite di righe applicato
- [ ] Tutti gli esempi inclusi
- [ ] NO link `[[01-fondamenti/...]]`
- [ ] NO metadata `**Tipo**: ...`
- [ ] Titoli con numerazione (### 3.2)

### Per Note Atomiche

- [ ] 40-80 righe di contenuto
- [ ] Totale ~100-130 righe
- [ ] Titolo è link a appunti completi: `# [[../../appunti-completi#...|Nome]]`
- [ ] Link ad altre note correlate nella sezione Collegamenti
- [ ] Seguono TEMPLATE.md
- [ ] Un solo concetto (atomicità)

### Sistema nel Complesso

- [ ] Ogni concetto in appunti-completi ha una nota atomica corrispondente
- [ ] Tutti i link vanno da atomico → completo
- [ ] Anchor format corretto (kebab-case, lowercase)
- [ ] Percorsi relativi corretti (`../../` o `../`)

---

## 🔄 Manutenzione e Aggiornamenti

### Quando Aggiornare Appunti Completi

✅ Quando:

- Studi nuovi argomenti
- Scopri dettagli importanti
- Trovi esempi migliori
- Correggi errori concettuali

❌ MAI:

- Sintetizzare per abbreviare
- Rimuovere esempi "per spazio"
- Aggiungere link a file atomici

### Quando Aggiornare Note Atomiche

✅ Quando:

- Serve migliore sintesi
- Link interrotti
- Miglior organizzazione
- Nuovi collegamenti

❌ MAI:

- Espandere oltre 80 righe (crea nuova nota)
- Rimuovere link agli appunti completi

---

## 📚 Riferimenti

- [TEMPLATE.md](TEMPLATE.md) - Template per note atomiche
- [QUICK-START.md](QUICK-START.md) - Guida rapida
- [README.md](README.md) - Panoramica del progetto

---

## ❓ FAQ

**Q: Quanto devono essere lunghe le sezioni in appunti-completi.md?**  
A: Non c'è limite. Possono essere 30 righe o 300 righe. L'importante è che contengano TUTTO il materiale originale.

**Q: Posso mettere link da appunti-completi.md ai file atomici?**  
A: NO. I link vanno SOLO da atomico → completo, mai il contrario.

**Q: Come so se una nota atomica è troppo lunga?**  
A: Se supera 80 righe di contenuto (esclusi header), va divisa in più note atomiche.

**Q: Posso avere esempi più lunghi negli appunti completi?**  
A: SÌ. Gli appunti completi devono avere TUTTI gli esempi originali (se forniti, altrimenti vanno creati), senza limiti.

**Q: Le note atomiche devono coprire tutto ciò che è negli appunti completi?**  
A: NO. Sono SINTESI. Coprono i concetti chiave e rimandano agli appunti completi per i dettagli.

---

**Ultima revisione**: 18 Febbraio 2026
