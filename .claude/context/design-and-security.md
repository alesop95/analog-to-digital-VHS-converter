---
generated-from-commit: PENDING-FIRST-COMMIT
generated-from-branch: main
generated-date: 2026-06-16
covers-paths:
  - .claude/context/**
last-verified-commit: PENDING-FIRST-COMMIT
---

# Workflow di conversione e qualità del segnale

> Popolare leggendo il documento principale .docx. I criteri di qualità e la catena del segnale
> sono il cuore tecnico del progetto: documentarli qui permette di riprendere il lavoro senza
> rileggere l'intero .docx.

## Workflow di cattura

<fasi del workflow dalla ricezione della cassetta al master digitale>

## Catena di qualità del segnale

<percorso del segnale analogico dalla testina VCR al file digitale; punti critici>

Nota dal documento principale: il concetto critico è la preservazione dei due campi
dell'interlacciamento (even/odd lines). La maggior parte dei dispositivi economici scarta un
campo, dimezzando la qualità temporale. Il workflow adottato preserva entrambi i campi a 59.94
fps (NTSC) o 50 fps (PAL interlacciato).

## Criteri di qualità del master

<parametri da verificare: frame drop, sync audio/video, colore, stabilità del segnale>

## Gestione nastri degradati

<approcci per nastri con muffa, ossidazione, smagnetizzazione o tracce instabili>

- TBC (Time Base Corrector): necessario per nastri con segnale instabile
- RF decode (vhs-decode GitHub): approccio avanzato che cattura il segnale RF grezzo prima
  della demodulazione del VCR; richiede hardware dedicato (da esplorare)

## Note di sicurezza operativa

<rischi per il materiale originale (cassette), procedure di manipolazione>
