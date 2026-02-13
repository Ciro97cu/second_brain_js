# 🤝 Come Contribuire

## Principi del Second Brain

Questo progetto segue il metodo **Zettelkasten** per la gestione della conoscenza:

1. **Note Atomiche**: Una nota = un concetto
2. **Collegamenti**: Ogni concetto è connesso ad altri
3. **Scrittura personale**: Rielabora con parole tue
4. **Progressive**: Si costruisce incrementalmente

## Workflow per aggiungere note

### 1. Prepara i tuoi appunti

Raccogli gli appunti grezzi che hai preso studiando.

### 2. Identifica i concetti chiave

Suddividi gli appunti in concetti atomici (uno per nota).

### 3. Crea le note

Per ogni concetto:

- Copia `TEMPLATE.md` con il nome appropriato
- Compila tutte le sezioni
- Aggiungi esempi pratici
- Crea collegamenti

### 4. Aggiorna gli indici

- Marca come completato nell'INDEX.md della cartella
- Aggiorna INDICE-COMPLETO.md se necessario

## Struttura di una buona nota

### ✅ Caratteristiche essenziali

- **Titolo chiaro**: Nome del concetto
- **Descrizione concisa**: 2-3 frasi che spiegano l'essenza
- **Esempi concreti**: Codice funzionante e commentato
- **Collegamenti**: Almeno 2-3 note correlate
- **Best practices**: Consigli pratici

### ❌ Da evitare

- Note troppo lunghe (> 200 righe)
- Copia-incolla da documentazione senza rielaborazione
- Note senza collegamenti
- Esempi non funzionanti
- Linguaggio troppo tecnico senza spiegazioni

## Naming Convention

### File

- Usa **kebab-case**: `arrow-functions.md`
- Nomi descrittivi: `promise-all.md` non `pa.md`
- Evita caratteri speciali: usa `-` non `_` o spazi

### Collegamenti

- Formato: `[[nome-file]]` (senza .md)
- Esempio: `[[arrow-functions]]`

## Categorie e Organizzazione

### Dove mettere una nota?

- **01-fondamenti**: Concetti base del linguaggio
- **02-funzioni**: Tutto relativo a funzioni
- **03-oggetti-classi**: OOP e prototipi
- **04-array-iterazione**: Array e loop
- **05-asincrono**: Async, Promises, callbacks
- **06-dom-eventi**: Browser API
- **07-es6-plus**: Feature moderne ES6+
- **08-moduli**: Import/Export
- **09-error-handling**: Gestione errori
- **10-testing**: Test e TDD
- **11-performance**: Ottimizzazione
- **12-design-patterns**: Pattern di programmazione
- **13-tools-ecosystem**: npm, bundler, etc.
- **14-typescript**: TypeScript
- **15-frameworks**: React, Vue, Angular

Se un concetto si trova a cavallo tra due categorie, scegli la più rilevante e aggiungi un collegamento nell'altra.

## Processo di revisione

### Auto-revisione

Prima di committare, chiediti:

1. ✓ La nota è completa?
2. ✓ Gli esempi funzionano?
3. ✓ Ho creato collegamenti?
4. ✓ Ho scritto con parole mie?
5. ✓ Ci sono errori di battitura?

### Revisione periodica

- Rivedi le note ogni 2-4 settimane
- Aggiungi nuovi collegamenti scoperti
- Migliora gli esempi
- Aggiorna con nuove informazioni

## Esempi di contributi

### Aggiungere una nuova nota

```bash
# 1. Crea la nota
cp TEMPLATE.md 02-funzioni/closure.md

# 2. Compila la nota (usa editor)

# 3. Aggiorna indice
# Modifica 02-funzioni/INDEX.md

# 4. Commit
git add .
git commit -m "Add: nota su closure"
```

### Migliorare una nota esistente

```bash
# 1. Modifica la nota

# 2. Commit
git commit -am "Improve: aggiunti esempi a arrow-functions"
```

### Aggiungere collegamenti

```bash
# 1. Identifica note correlate

# 2. Aggiungi link nelle sezioni "Collegamenti"

# 3. Commit
git commit -am "Link: collegate note su scope e closure"
```

## Messaggi di commit

Usa prefissi chiari:

- `Add:` - Nuova nota
- `Update:` - Aggiornamento contenuto
- `Improve:` - Miglioramento nota esistente
- `Fix:` - Correzione errori
- `Link:` - Aggiunta collegamenti
- `Refactor:` - Riorganizzazione struttura

Esempi:

```bash
git commit -m "Add: nota su Promise.all()"
git commit -m "Update: esempi in array-map"
git commit -m "Fix: correzione codice in closure"
git commit -m "Link: collegamento tra async-await e promises"
```

## Risorse utili

- [Metodo Zettelkasten](https://zettelkasten.de/introduction/)
- [How to Take Smart Notes](https://www.goodreads.com/book/show/34507927-how-to-take-smart-notes)
- [Building a Second Brain](https://www.buildingasecondbrain.com/)

---

**Grazie per contribuire alla crescita di questo Second Brain! 🧠**
