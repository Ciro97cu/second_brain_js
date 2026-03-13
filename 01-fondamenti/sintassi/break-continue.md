# [[../../appunti-completi#28-cicli-loops|Controllo del Flusso: break e continue]]

JavaScript offre due parole chiave fondamentali per avere un maggior controllo sul flusso di esecuzione all'interno dei cicli: `break` e `continue`. Queste istruzioni alterano il comportamento standard predefinito della struttura ciclica.

## Istruzioni di Controllo

Le due istruzioni differiscono per l'entità del salto che impongono all'interprete:

- L'uscita totale dal ciclo corrente. Modifica in modo permanente l'esecuzione del blocco. Per approfondimenti sui casi d'uso e la sintassi, vedi [[break-statement|L'istruzione break]].
- Il salto in avanto di un solo passo. Evita l'esecuzione della singola logica per l'iterazione in corso e passa alla successiva. Per esplorare l'utilità e il funzionamento, vedi [[continue-statement|L'istruzione continue]].

## Confronto Diretto

| Istruzione | Comportamento Reale                                           |
| ---------- | ------------------------------------------------------------- |
| `break`    | Esce definitivamente dal costrutto ciclico                    |
| `continue` | Abbandona il ciclo in corso, riprendendo dal passo successivo |

```javascript
// break interrompe
for (let i = 0; i < 10; i++) {
  if (i % 2 !== 0) break; // Si ferma a 0
  console.log(i);
}

// continue salta
for (let i = 0; i < 10; i++) {
  if (i % 2 !== 0) continue; // Salta i dispari
  console.log(i);
}
```

Queste istruzioni di controllo sono essenziali per scrivere logiche ottimali durante l'interazione con array e l'esecuzione di cicli potenzialmente lunghi.
