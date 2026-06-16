---
generated-from-commit: PENDING-FIRST-COMMIT
generated-from-branch: main
generated-date: 2026-06-16
covers-paths:
  - _notes/settings/**
last-verified-commit: PENDING-FIRST-COMMIT
---

# Test e validazione della cattura

> Procedure di verifica della qualità della cattura. Non ci sono test software automatici:
> qui si documentano i controlli manuali da eseguire durante e dopo ogni sessione di cattura.
> La checklist operativa locale vive in _notes/TEST-CHECKLIST.md, ignorata da git.

## Configurazione di test in OBS Studio

<configurazione scene, device, risoluzione, framerate, audio per un test di cattura>

Screenshot di riferimento: _notes/settings/obs-settings-base/

## Checklist di verifica pre-cattura

<passi da completare prima di avviare una cattura lunga>

## Indicatori di qualità durante la cattura

<frame drop, livelli audio, stabilità del segnale: come leggerli in OBS>

## Verifica del file masterizzato

<come controllare il file AVI risultante: integrità, durata, qualità visiva, sync>

## Troubleshooting noto

<problemi comuni e soluzioni documentate nel .docx principale>

- Frame dropping: ridurre risoluzione preview o abbassare carico CPU
- Timing issues: testine VCR sporche, nastro consumato
- Audio drift: impostazioni mono/stereo, latenza interfaccia audio
- Video jitter: impostazioni di deinterlacciamento in OBS
