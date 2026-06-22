---
generated-from-commit: dc872289dadc6935754f704a70a382411d072fc4
generated-from-branch: main
generated-date: 2026-06-16
covers-paths:
  - .claude/**
last-verified-commit: dc872289dadc6935754f704a70a382411d072fc4
stato: in pianificazione
---

# Lavoro in corso

> La fonte di verità su cosa è fatto resta memory/index.md e il work-log, non le spunte di
> questo file. Ogni attività si descrive con lo schema fisso sotto.

## Attività: Strutturazione della documentazione in file .md tracciati

Cosa fa: convertire il contenuto del .docx principale e dei file _notes/ in documenti .md
versionati e collegati all'anatomia .claude/context/.

File da creare:

```
.claude/context/STACK.md            già creato con struttura (da popolare)
.claude/context/design-and-security.md  già creato con struttura (da popolare)
.claude/context/deployment.md       già creato con struttura (da popolare)
.claude/context/dev-testing.md      già creato con struttura (da popolare)
.claude/context/roadmap.md          già creato con struttura (da popolare)
```

Definition of done:

- [x] Schede context/ popolate con il contenuto estratto dal .docx principale
- [x] README.md pubblico creato e pronto per il secondo commit
- [x] dev-testing.md espansa con nota driver BDA vs Twain
- [x] _notes/ ripulita (mmsp2_lab6 eliminato, settings archiviati in old/)
- [ ] _notes/upscaling-topaz-AI/upscaling-topaz-AI.md collegata alla scheda STACK.md
- [ ] Workflow cliente definito e documentato in deployment.md
- [x] Primo commit effettuato (dc87228) e hash ancorato via sync-context
- [ ] Secondo commit (README.md + dev-testing.md) — in attesa manuale

Domande aperte:

- Il workflow cliente (prezzi, formati, consegna) è già definito o ancora in elaborazione?
- _notes/upscaling-topaz-AI/ va collegata esplicitamente a STACK.md o è sufficiente il riferimento implicito?

## Riconciliazione

Ultima verifica: 2026-06-16 al commit dc872289dadc6935754f704a70a382411d072fc4.
