# Snapshot di sincronizzazione

> Da leggere per primo a inizio sessione. Fotografa lo stato del progetto al commit di
> riferimento e mappa ogni scheda al suo stato di verifica. È la fonte di verità su cosa è
> fatto, non le spunte del diario.

## Stato

```
Branch attivo:         main
Commit di riferimento: PENDING-FIRST-COMMIT
Data snapshot:         2026-06-16
```

## Stato di verifica delle schede

| Scheda | last-verified | Stato |
|---|---|---|
| STACK.md | PENDING-FIRST-COMMIT | init |
| design-and-security.md | PENDING-FIRST-COMMIT | init |
| deployment.md | PENDING-FIRST-COMMIT | init |
| dev-testing.md | PENDING-FIRST-COMMIT | init |
| current-work.md | PENDING-FIRST-COMMIT | init |
| roadmap.md | PENDING-FIRST-COMMIT | init |

## Punto di ripresa

Inizializzazione completata (2026-06-16). Prossimo passo: eseguire il primo commit manuale,
poi invocare la skill `sync-context` per sostituire i `PENDING-FIRST-COMMIT` con l'hash reale
di HEAD. Successivamente: popolare le schede context/ estraendo il contenuto dal .docx
principale.
