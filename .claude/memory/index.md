# Snapshot di sincronizzazione

> Da leggere per primo a inizio sessione. Fotografa lo stato del progetto al commit di
> riferimento e mappa ogni scheda al suo stato di verifica. È la fonte di verità su cosa è
> fatto, non le spunte del diario.

## Stato

```
Branch attivo:         main
Commit di riferimento: dc872289dadc6935754f704a70a382411d072fc4
Data snapshot:         2026-06-16
```

## Stato di verifica delle schede

| Scheda | last-verified | Stato |
|---|---|---|
| STACK.md | dc872289dadc6935754f704a70a382411d072fc4 | aggiornata |
| design-and-security.md | dc872289dadc6935754f704a70a382411d072fc4 | aggiornata |
| deployment.md | dc872289dadc6935754f704a70a382411d072fc4 | aggiornata |
| dev-testing.md | dc872289dadc6935754f704a70a382411d072fc4 | aggiornata |
| current-work.md | dc872289dadc6935754f704a70a382411d072fc4 | aggiornata |
| roadmap.md | dc872289dadc6935754f704a70a382411d072fc4 | aggiornata |

## Punto di ripresa

Sessione 2026-06-16 chiusa. Schede popolate, README.md creato, dev-testing.md espansa con
distinzione BDA/Twain, _notes/ ripulita. Secondo commit in attesa esecuzione manuale:
`git add README.md .claude/context/dev-testing.md && git commit -m "docs: README pubblico e nota driver Twain"`.

Prossimo passo concreto: ricattura con impostazioni MJPEG/AVI per produrre il primo master
vero. Poi: definire workflow cliente (prezzi, formati, consegna). Vedi roadmap.md.
