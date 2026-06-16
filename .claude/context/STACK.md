---
generated-from-commit: PENDING-FIRST-COMMIT
generated-from-branch: main
generated-date: 2026-06-16
covers-paths:
  - _notes/manuali-e-specifiche/**
  - _notes/settings/**
last-verified-commit: PENDING-FIRST-COMMIT
---

# Stack tecnico

> Documento di recupero importante: tracciato, perché chiunque cloni deve vedere hardware,
> software e standard adottati. Popolare leggendo i manuali in _notes/ e il .docx principale,
> non inventare. Affinare covers-paths man mano.

## Hardware

<dispositivi di cattura, VCR, adattatori, cavi e loro ruolo nella catena del segnale>

Hardware noto dal documento principale:
- Capture device: StarTech SVID2USB232 (S-Video + Composite → USB)
- VCR: DAEWOO ST220 (PAL-B/G, 200V-240V)
- Catena segnale: SCART maschio-maschio → adattatore SCART → RCA → StarTech
- Interfaccia audio esterna: Focusrite (monitoring audio)

## Software

<applicazioni, versioni, ruolo>

Software noto:
- Cattura: OBS Studio (versione da rilevare)
- Post-processing AI: Topaz Video AI Pro 7.1
- Driver capture card: EM2860 (da installarsi manualmente su Windows 11)

## Standard di codifica del master digitale

<codec, container, risoluzione, framerate, audio>

Standard adottati (PAL):
- Codec video: MJPEG (intra-frame, ~30 Mbps)
- Container: AVI
- Risoluzione: 720×576
- Framerate: 25 fps
- Audio: PCM, 48 kHz, 16-bit, stereo
- Dimensione attesa: ~3.95 MB/s (~28-30 GB per 2 ore)

## Alternative deliberatamente escluse

<tecnologie valutate e scartate, con il motivo>

- DIGITNOW USB dongle (~$10): scarta entrambi i campi dell'immagine, produce output degradato
- Elgato: non gestisce correttamente i due campi dell'interlacciamento
- MP4 come container master: non adatto per archivio; si usa AVI con MJPEG

## Riferimenti a documentazione

<puntatori a file di _notes/ rilevanti>

- _notes/manuali-e-specifiche/StarTech svid2usb23 composite to usb capture cable/
- _notes/settings/obs-settings-base/ (screenshot configurazione OBS)
- _notes/upscaling-topaz-AI/upscaling-topaz-AI.md
