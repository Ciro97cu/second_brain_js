# Dove Inserire il Codice JavaScript in HTML

**Tipo**: Nuovo Topic  
**Data**: 13 Febbraio 2026  
**Appunti Completi**: [[../appunti-completi#13-dove-inserire-il-codice-javascript-in-html]]

---

## Descrizione

Per far interagire JavaScript con una pagina web, è necessario includere il codice nel documento HTML. Questo si fa tramite il tag `<script>`, che può essere posizionato in punti diversi del file. La posizione e gli attributi usati (async, defer) hanno un impatto significativo sul caricamento della pagina e sulle performance.

Il modo più comune è collegare un file .js esterno usando l'attributo src.

```html
<script src="script.js"></script>
```

## Nel `<head>` (Senza Attributi)

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Esempio</title>
    <script src="script.js"></script>
  </head>
  <body>
    <h1>Contenuto della pagina</h1>
  </body>
</html>
```

**Comportamento** → Il browser interrompe l'analisi (parsing) del file HTML, scarica ed esegue immediatamente lo script. Solo dopo riprende a costruire la pagina.

**Impatto** → È un metodo bloccante (blocking). Rallenta la visualizzazione iniziale della pagina, perché l'utente non vedrà alcun contenuto finché lo script non avrà finito. Oggi è una pratica generalmente sconsigliata.

## Alla Fine del `<body>`

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Esempio</title>
  </head>
  <body>
    <h1>Contenuto della pagina</h1>
    <p>Tutto il contenuto HTML viene caricato prima dello script</p>

    <script src="script.js"></script>
  </body>
</html>
```

**Comportamento** → Il browser analizza e visualizza tutto il contenuto HTML della pagina. Solo alla fine, scarica ed esegue lo script.

**Impatto** → La pagina appare velocemente all'utente. Quando lo script viene eseguito, ha già accesso a tutti gli elementi del DOM. È stata la tecnica più raccomandata per anni.

## Nel `<head>` con Attributo defer

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Esempio</title>
    <script src="script.js" defer></script>
    <script src="altro-script.js" defer></script>
  </head>
  <body>
    <h1>Contenuto della pagina</h1>
  </body>
</html>
```

**Comportamento** → Il browser scarica lo script in parallelo, senza interrompere l'analisi dell'HTML. Lo script viene eseguito solo quando l'intero documento HTML è stato analizzato, ma prima che venga lanciato l'evento DOMContentLoaded. Se ci sono più script con defer, vengono eseguiti nell'ordine in cui appaiono nel documento.

**Impatto** → Non blocca la visualizzazione della pagina e garantisce l'ordine di esecuzione. È spesso la scelta migliore e più moderna.

## Nel `<head>` con Attributo async

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Esempio</title>
    <script src="analytics.js" async></script>
  </head>
  <body>
    <h1>Contenuto della pagina</h1>
  </body>
</html>
```

**Comportamento** → Il browser scarica lo script in parallelo, ma lo esegue non appena il download è completato, interrompendo momentaneamente l'analisi dell'HTML se non è ancora finita. L'ordine di esecuzione non è garantito se ci sono più script async.

**Impatto** → Utile per script indipendenti che non devono interagire con il DOM e non dipendono da altri script (es. script di analytics, pubblicità). Non è adatto per script che manipolano la pagina o che hanno dipendenze.

## Esempio

```html
<!-- 1. Nel <head> SENZA attributi - SCONSIGLIATO (blocca il rendering) -->
<head>
  <script src="script.js"></script>
</head>

<!-- 2. A fine <body> - Tecnica classica (DOM già caricato) -->
<body>
  <h1>Contenuto</h1>
  <script src="script.js"></script>
</body>

<!-- 3. Nel <head> con DEFER - RACCOMANDATO (parallelo + ordine garantito) -->
<head>
  <script src="script.js" defer></script>
</head>

<!-- 4. Nel <head> con ASYNC - Per script indipendenti (analytics) -->
<head>
  <script src="analytics.js" async></script>
</head>
```

## Collegamenti

- [[programma]] - Il programma JavaScript viene inserito nell'HTML
- [[esecuzione]] - Come il browser esegue il codice JavaScript

## Riferimenti

- [MDN - The Script element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script)
- [MDN - async and defer attributes](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/What_is_JavaScript#script_loading_strategies)
