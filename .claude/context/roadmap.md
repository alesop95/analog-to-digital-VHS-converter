---
generated-from-commit: PENDING-FIRST-COMMIT
generated-from-branch: main
generated-date: 2026-06-16
covers-paths: []
last-verified-commit: PENDING-FIRST-COMMIT
---

# Roadmap

> Direzione e priorità del progetto. Tracciata. Non è il work-log: qui sta dove si va, non cosa
> è già stato fatto.

## Direzione

Costruire un servizio affidabile e documentato di digitalizzazione VHS per clienti privati,
con workflow ripetibile dalla cattura al master digitale al post-processing AI. La
documentazione tecnica (hardware, software, procedure) è già consolidata nel .docx principale;
il passo successivo è strutturarla in file .md versionati e definire compiutamente il workflow
di servizio verso il cliente.

## Priorità

1. Consolidare la documentazione del workflow di cattura: estrarre dal .docx i contenuti
   definitivi e popolare le schede .claude/context/ con il materiale verificato.
2. Strutturare i contenuti di _notes/ in file .md tracciabili: ogni sottocartella esistente
   (annuncio-per-pubblicizzare, upscaling-topaz-AI, settings) ha contenuto da formalizzare.
3. Definire il workflow cliente: ricezione del materiale, standard di consegna, formati di
   output, procedura USB drive, comunicazione.
4. Formalizzare la procedura di post-processing con Topaz Video AI Pro 7.1: parametri,
   preset, tempi di elaborazione CPU-only.
5. Valutare se creare un README.md pubblico per la repo GitHub, distinto dalla documentazione
   interna.
6. Esplorare l'approccio RF decode (vhs-decode GitHub) per nastri particolarmente degradati:
   requisiti hardware, qualità attesa, confronto con il workflow attuale.

## Idee e ipotesi da verificare

- RF decode via vhs-decode: qualità superiore catturando il segnale RF grezzo prima della
  demodulazione del VCR; richiede hardware dedicato e setup complesso (da verificare).
- TBC (Time Base Corrector) esterno per nastri con segnale instabile: costi e benefici
  rispetto alla gestione via software (da verificare).
- Upscaling 4K con Topaz senza GPU dedicata: documentato in
  _notes/upscaling-topaz-AI/upscaling-topaz-AI.md; fattibilità su CPU overnight (da verificare
  con test reali).
- Workflow PAL vs NTSC: il documento principale tratta principalmente PAL; verificare se il
  workflow si adatta a nastri NTSC (59.94 fps, 720×480).
