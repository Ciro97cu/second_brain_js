# 🚀 Quick Start Guide

## Come iniziare con il tuo Second Brain JavaScript

### 1️⃣ Primo Setup

```bash
# Clona o naviga nella directory del progetto
cd second_brain_js

# Inizializza git (se non già fatto)
git init
git add .
git commit -m "Initial commit: JavaScript Second Brain structure"
```

### 2️⃣ Come aggiungere una nuova nota

#### Passo 1: Scegli la categoria

Apri [INDICE-COMPLETO.md](INDICE-COMPLETO.md) e trova l'argomento che vuoi studiare.

#### Passo 2: Copia il template

```bash
# Copia il template nella cartella appropriata
cp TEMPLATE.md 01-fondamenti/var-let-const.md
```

#### Passo 3: Compila la nota

- Cambia il titolo
- Aggiungi la descrizione
- Inserisci esempi di codice
- Collega ad altre note usando `[[nome-nota]]`

#### Passo 4: Aggiorna l'indice

Marca l'argomento come completato nell'INDEX.md della cartella.

### 3️⃣ Workflow consigliato

1. **Studia un concetto** da una risorsa (corso, libro, documentazione)
2. **Prendi appunti grezzi** mentre studi
3. **Sintetizza** usando il template
4. **Crea collegamenti** con concetti correlati
5. **Rivedi** periodicamente le note

### 4️⃣ Best Practices

✅ **Una nota = Un concetto**

- Mantieni le note atomiche e focalizzate

✅ **Usa i tuoi esempi**

- Oltre agli esempi standard, aggiungi casi d'uso personali

✅ **Collega attivamente**

- Ogni nota dovrebbe avere almeno 2-3 collegamenti

✅ **Scrivi con parole tue**

- Non copiare/incollare: rielabora i concetti

✅ **Inserisci errori comuni**

- Documenta gli errori che fai per evitarli in futuro

### 5️⃣ Esempio pratico

Supponiamo tu voglia studiare le **Arrow Functions**:

1. Leggi la documentazione MDN
2. Copia `TEMPLATE.md` in `02-funzioni/arrow-functions.md`
3. Compila con:
   - Descrizione di cosa sono le arrow functions
   - Esempi di sintassi
   - Differenze con function normali
   - Collegamenti a `[[this-keyword]]`, `[[function-expression]]`
4. Aggiorna `02-funzioni/INDEX.md` marcando `[✓]`

### 6️⃣ Simboli utilizzati

- `[ ]` - Da studiare
- `[→]` - In corso
- `[✓]` - Completato
- `[!]` - Da approfondire
- `[[nome]]` - Link ad altra nota

### 7️⃣ Comandi Git utili

```bash
# Salva i progressi
git add .
git commit -m "Add: note su arrow functions"

# Sincronizza con GitHub (dopo aver creato il repo)
git remote add origin <url-repo>
git push -u origin main
```

### 8️⃣ Prossimi passi

1. Inizia dai **fondamenti** (01-fondamenti)
2. Passa ai tuoi appunti e inizia a sintetizzare
3. Crea almeno 2-3 note per categoria
4. Rivedi settimanalmente

---

## 💡 Tips

- **Non aspettare la perfezione**: meglio una nota incompleta che nessuna nota
- **Revisiona regolarmente**: le note migliorano con la rilettura
- **Usa tag**: aggiungi tag per ricerche rapide
- **Esporta esempi**: crea file .js separati per esempi complessi

---

**Buono studio! 🎯**
