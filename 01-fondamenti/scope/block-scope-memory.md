# [[../../appunti-completi#blocchi-come-scope-blocks-as-scopes|Block Scope e Garbage Collection]]

## 🎯 Concetto

Lo **scope di blocco** con `let` e `const` non è solo una questione di correttezza sintattica, ma ha anche **importanti implicazioni sulla gestione della memoria**. Confinare variabili in blocchi espliciti aiuta il **Garbage Collector** a liberare memoria non più necessaria, specialmente in presenza di **closures**.

**Beneficio chiave**: Il motore JavaScript può identificare con certezza quando una variabile non è più utilizzabile e liberare la memoria associata.

## 💻 Il Problema: Closures e Memory Leaks

### Closure Mantiene Tutto lo Scope

```javascript
function process(data) {
  // Struttura dati MOLTO grande
  var someReallyBigData = {
    /* ... milioni di record, 50MB ... */
  };

  // Calcolo che usa i dati
  var result = doSomething(someReallyBigData);

  // Click handler che NON usa someReallyBigData
  $("#button").click(function click() {
    console.log("Button clicked!");
  });

  return result;
}

// ⚠️ Problema: someReallyBigData rimane in memoria INDEFINITAMENTE!
```

**Perché?** La funzione `click` crea una **closure sull'intero scope di `process`**. Anche se `click` non usa mai `someReallyBigData`, il motore JavaScript non può sapere con certezza se potrebbe accedervi in futuro, quindi mantiene TUTTO lo scope in memoria.

### Esempio Reale: API Response Grande

```javascript
function loadUserProfile(userId) {
  // Risposta API con migliaia di record (20MB)
  var fullAPIResponse = fetchAllUserData(userId);

  // Estraiamo solo nome e email (pochi byte)
  var profile = {
    name: fullAPIResponse.user.name,
    email: fullAPIResponse.user.email,
  };

  // Event listener per bottone
  $("#saveProfile").click(function () {
    saveProfile(profile); // Usa SOLO profile
  });

  return profile;
}

// ⚠️ fullAPIResponse (20MB) rimane in memoria
// anche se serve solo profile (pochi byte)!
```

### Quando è un Problema

```javascript
// Scenario critico: Molte closure create in loop
var users = getUsersFromAPI(); // 1000 utenti

users.forEach(function (user) {
  var largeUserData = fetchDetailedProfile(user.id); // 5MB per utente

  var summary = extractSummary(largeUserData); // 50 bytes

  $("#user-" + user.id).click(function () {
    displaySummary(summary); // Usa solo summary
  });
});

// ⚠️ 1000 closures × 5MB = 5GB di memoria occupata inutilmente!
```

## 🗑️ Soluzione: Block Scope per Liberare Memoria

### Confinare Dati Temporanei in Blocchi

```javascript
function process(data) {
  var result;

  {
    // Blocco esplicito per i dati temporanei
    let someReallyBigData = {
      /* ... milioni di record, 50MB ... */
    };
    result = doSomething(someReallyBigData);
  }

  // ✅ Qui someReallyBigData può essere garbage-collected!
  // Il motore SA che non serve più (fuori dallo scope)

  $("#button").click(function click() {
    console.log("Button clicked!");
    // Questa closure NON include someReallyBigData
  });

  return result;
}
```

Una volta terminata l'esecuzione del blocco `{ ... }`, la variabile `someReallyBigData` dichiarata con `let` va **fuori scope**. Il motore JavaScript sa con certezza che non può più essere accessibile e può **liberar la memoria** immediatamente, anche se la funzione `click` continua a esistere.

### Esempio Reale Fixed

```javascript
function loadUserProfile(userId) {
  var profile;

  {
    // Cache temporanea per elaborazione
    let fullAPIResponse = fetchAllUserData(userId); // 20MB
    profile = {
      name: fullAPIResponse.user.name,
      email: fullAPIResponse.user.email,
    }; // pochi byte
  }

  // ✅ fullAPIResponse (20MB) liberata dal GC qui!

  $("#saveProfile").click(function () {
    saveProfile(profile); // Closure mantiene SOLO profile
  });

  return profile;
}
```

### Loop con Grandi Dati Fixed

```javascript
var users = getUsersFromAPI(); // 1000 utenti

users.forEach(function (user) {
  var summary;

  {
    // Blocco per dati temporanei
    let largeUserData = fetchDetailedProfile(user.id); // 5MB
    summary = extractSummary(largeUserData); // 50 bytes
  }

  // ✅ largeUserData (5MB) liberato dopo ogni iterazione

  $("#user-" + user.id).click(function () {
    displaySummary(summary); // Closure mantiene SOLO summary
  });
});

// ✅ Totale in memoria: 1000 × 50 bytes = ~50KB (invece di 5GB!)
```

## 📊 Esempio Pratico: Cache Temporanea

### Processing Pipeline con Cache

```javascript
function processLargeDataset(datasetId) {
  let results = [];

  {
    // Stage 1: Fetch e parsing (usa molta memoria)
    let rawData = fetchRawData(datasetId); // 100MB
    let parsed = parseData(rawData); // 80MB
    results.push(...parsed.summaries); // 1MB
  }

  // ✅ rawData (100MB) + parsed (80MB) = 180MB liberati!

  {
    // Stage 2: Enrichment (usa altra memoria)
    let enrichmentCache = loadEnrichmentData(); // 50MB
    results = results.map((r) => enrich(r, enrichmentCache));
  }

  // ✅ enrichmentCache (50MB) liberata!

  return results; // Solo 2MB in memoria
}
```

### Web Worker con Block Scope

```javascript
function processInWorker(workerData) {
  var processedResults;

  {
    // Blocco per elaborazione intensiva
    let tempBuffer = new ArrayBuffer(1024 * 1024 * 100); // 100MB
    let view = new Uint8Array(tempBuffer);

    // Elaborazione pesante
    for (let i = 0; i < view.length; i++) {
      view[i] = computeValue(workerData[i]);
    }

    processedResults = extractResults(view); // 5MB
  }

  // ✅ tempBuffer (100MB) liberato!

  postMessage(processedResults); // Invia solo 5MB
}
```

## 🔬 Come il Motore Decide

### Cosa il GC Può Determinare

```javascript
function example() {
  var outer = "mantieni questo";

  {
    // Blocco con let
    let temp = createLargeObject(); // 50MB
    outer += process(temp);
  }

  // GC può liberare 'temp' perché:
  // 1. È dichiarata con 'let' in un blocco
  // 2. Il blocco è terminato
  // 3. Nessuna closure può accedervi (fuori scope)

  return outer;
}
```

### Cosa il GC NON Può Determinare (con var)

```javascript
function example() {
  var outer = "mantieni questo";

  {
    // Blocco con var
    var temp = createLargeObject(); // 50MB
    outer += process(temp);
  }

  // ⚠️ GC NON può liberare 'temp' perché:
  // 1. var ha function scope (ancora nello scope)
  // 2. Potrebbe essere usata dopo il blocco
  // 3. GC deve essere conservativo

  return outer;
}
```

## ⚠️ Attenzione: Non Sempre Necessario

### Quando è Utile

```javascript
// ✅ UTILE: Dati temporanei MOLTO grandi
function processImages(images) {
  let results = [];

  images.forEach((img) => {
    {
      // Blocco per buffer temporaneo
      let decodedBuffer = decodeImage(img); // 10MB per immagine
      let thumbnail = createThumbnail(decodedBuffer); // 100KB
      results.push(thumbnail);
    }
    // ✅ decodedBuffer (10MB) liberato dopo ogni immagine
  });

  return results;
}
```

### Quando NON Serve

```javascript
// ❌ OVERKILL: Variabili piccole
function calculate(a, b) {
  {
    // ❌ Inutile per variabili piccole
    let temp = a + b; // pochi bytes
    return temp * 2;
  }
}

// ✅ Meglio semplice
function calculate(a, b) {
  let temp = a + b;
  return temp * 2;
}
```

### Regola Generale

Usa blocchi espliciti per ottimizzare memoria quando:

- ✅ Dati temporanei > 1MB
- ✅ Ci sono closures che vivono a lungo
- ✅ Molte iterazioni (loop) con dati grandi
- ✅ Processing pipelines con cache intermedie

NON serve per:

- ❌ Variabili primitive piccole (numeri, stringhe corte)
- ❌ Oggetti piccoli (< 1KB)
- ❌ Funzioni che terminano subito (no closures)

## 📦 Pattern Avanzati

### Pipeline con Stages

```javascript
function dataPipeline(input) {
  let stage1Result;
  {
    let rawData = fetchData(input); // 100MB
    stage1Result = stage1Process(rawData); // 20MB
  } // -100MB

  let stage2Result;
  {
    let enrichedData = enrichData(stage1Result); // 50MB
    stage2Result = stage2Process(enrichedData); // 10MB
  } // -50MB

  let finalResult;
  {
    let transformedData = transform(stage2Result); // 30MB
    finalResult = finalize(transformedData); // 2MB
  } // -30MB

  return finalResult; // Solo 2MB in memoria
}
```

### Async/Await con Block Scope

```javascript
async function loadAndProcess() {
  let summary;

  {
    // Blocco per dati temporanei asincroni
    let data = await fetchBigData(); // 100MB
    let processed = await processData(data); // 50MB
    summary = extractSummary(processed); // 1MB
  }

  // ✅ data + processed = 150MB liberati

  return summary;
}
```

### Event Handlers con Dati Grandi

```javascript
function setupHandlers(largeDataset) {
  let essentials = extractEssentials(largeDataset); // 100KB from 50MB

  {
    // largeDataset usato solo per setup
    let tempIndex = buildIndex(largeDataset); // 20MB
    let config = deriveConfig(largeDataset, tempIndex); // 5MB
    essentials.config = config;
  }

  // ✅ largeDataset + tempIndex liberati (70MB)

  $("#btn").click(() => {
    processWithEssentials(essentials); // Closure su 100KB, non 70MB
  });
}
```

## ✅ Best Practices

1. **Usa blocchi espliciti per dati temporanei grandi (>1MB)**
2. **Confina cache e buffer in blocchi dedicati** prima di creare closures
3. **Libera memoria in loop** se ogni iterazione usa dati grandi
4. **Separa processing stages** con blocchi distinti
5. **Non esagerare** - usa solo per veri problemi di memoria

## 🔗 Concetti Correlati

- [[let-const-block-scope|let e const]] - Come funziona block scope
- [[closures|Closures]] - Come le closure catturano lo scope
- [[nested-scope|Scope Annidato]] - Scope chain e lookup
- [[../../appunti-completi#blocchi-come-scope-blocks-as-scopes|Blocchi come Scope Completo]]

## 📚 Risorse

- MDN: Memory Management
- Chrome DevTools: Memory Profiler
- "You Don't Know JS" - Scope & Closures

## 📌 Tag

#javascript #scope #block-scope #garbage-collection #memory #performance #closures #optimization #let #memory-leaks
