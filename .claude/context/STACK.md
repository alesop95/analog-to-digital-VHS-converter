---
generated-from-commit: dc872289dadc6935754f704a70a382411d072fc4
generated-from-branch: main
generated-date: 2026-06-16
covers-paths:
  - _notes/manuali-e-specifiche/**
  - _notes/settings/**
last-verified-commit: dc872289dadc6935754f704a70a382411d072fc4
---

# Stack tecnico

> Tracciato. Documenta hardware, software e standard adottati ricavandoli dal documento
> principale e dai manuali in _notes/. Affinare covers-paths man mano.

## Hardware

La catena hardware finale è la seguente.

VCR DAEWOO ST220 (SCART femmina) → cavo SCART maschio-maschio → adattatore SCART femmina
CABLEPELADO (con selettore ingresso/uscita impostato su OUT) → 3 RCA (giallo + rosso + bianco)
→ StarTech SVID2USB232 (ingresso Composite + Audio).

Il segnale che percorre questa catena è CVBS PAL composito analogico interlacciato (576i,
25 frame/sec, 50 campi/sec). L'adattatore CABLEPELADO è passivo e instrada i pin SCART senza
nessuna conversione: estrae solo Composite e Audio, non S-Video (il pin 15 non è collegato
nel DAEWOO ST220). La qualità è quindi fissata al Composite e non migliorabile via cavi.

### VCR

DAEWOO VIDEO CASSETTE RECORDER MODEL NO. ST220. Sistema PAL-B/G. Alimentazione 200V-240V ~
50/60Hz, 14W. Serial No. GV33A42692. Uscita posteriore: EURO AV SCART femmina. L'uscita
espone solo Composite (CVBS): Y e C sono già sommati internamente prima della SCART, il pin 15
(crominanza S-Video) non è cablato. Ha capacità di riproduzione NTSC commerciale su TV PAL
(funzione COMMERCIAL SKIP NTSC PLAYBACK ON PAL TV).

### Capture card

StarTech SVID2USB232 (USB Video Capture, S-Video or Composite to USB). Chip Empia EM28xx,
USB VID_EB1A&PID_8286. Due interfacce distinte: USB 2828x Device (video) e USB 2828x Audio
Device (audio), che appaiono separate in Gestione dispositivi come comportamento atteso.
Preserva entrambi i campi dell'interlacciamento: campo pari e campo dispari arrivano
all'ADC senza essere scartati.

Driver installato: BDA051321.2 v5.2021.0513.2 (da startech.com/SVID2USB232, NON il CD incluso
che è obsoleto su Windows 11). Installer: Setup_5.2021.080.3.exe. Il CD incluso usa driver
legacy non compatibili con Windows 10/11 perché nessun file .inf nel CD dichiara compatibilità
con VID_EB1A&PID_8286.

### Audio monitoring

Focusrite Scarlett 2i4 2nd Gen. Driver scaricati il 30/11/2025 da downloads.focusrite.com.
Usata come dispositivo di output in Windows 11 per il monitoring durante la cattura: OBS
invia il flusso audio alla Focusrite tramite le impostazioni di monitoraggio audio avanzate.

## Software

OBS Studio (Open Broadcaster Software) per Windows 11. Download da obsproject.com (installer).
Usato per cattura, processing e encoding in un solo step. Configurazione: nuovo profilo e nuova
Scene Collection 4:3, canvas 1440×1080 (4:3 PAL a qualità superiore).

Topaz Video AI Pro 7.1 (x64) per upscaling e post-processing dei master digitali.
Elaborazione CPU-only (nessuna GPU dedicata). Documentazione tecnica in
_notes/upscaling-topaz-AI/upscaling-topaz-AI.md.

## Standard di codifica — master digitale

Il master VHS va prodotto con un codec intra-frame ad alto bitrate: qualsiasi codec inter-frame
(H.264, H.265, MPEG-2) è sbagliato per l'archivio perché penalizza il rumore analogico
imprevedibile della VHS.

Standard adottato (PAL):
- Container: AVI (accetta qualsiasi codec, PCM nativo, robusto come archivio)
- Encoder video: MJPEG (intra-frame, ogni fotogramma indipendente)
- Qualità/bitrate: 90-95 oppure 25-35 Mbps
- Risoluzione: 720×576
- Frame rate: 25 fps interlacciato (Top Field First — NON deinterlacciare il master)
- Spazio colore: YUV 4:2:2
- Gamma: BT.601 (PAL, assunta automaticamente da OBS per SD)
- Encoder audio: PCM non compresso, 48 kHz, 16-bit, stereo (WAV)
- Peso atteso: ~3.95 MB/s → ~28-30 GB per 2 ore di registrazione

In OBS questa configurazione si ottiene da Impostazioni > Uscita > Registrazione > Qualità della
registrazione: "lossless con dimensioni del file enormi". Il container MP4 è da evitare per il
master perché supporta male PCM non compresso, MJPEG ad alto bitrate e flussi interlacciati non
consumer; è pensato per H.264/H.265 e streaming, non per archivio.

## Impostazioni OBS della prima cattura di test (subottimali)

La prima cattura di verifica è stata eseguita con le seguenti impostazioni (non adatte al master):
- Qualità della registrazione: Alta qualità, dimensioni dei file medie
- Formato: MP4 ibrido [BETA]
- Encoder video: Hardware QSV H.264
- Encoder audio: AAC 160 kbps
- Bitrate totale: 6160 kbps → ~0.77 MB/s → ~5.4 GB per 2 ore

Queste impostazioni sono adatte per output di fruizione quotidiana, non per il master.

## Alternative deliberatamente escluse

DIGITNOW USB dongle (~10 EUR): driver che scarta un campo su due, qualità dimezzata, nessun
workaround software possibile.

Elgato USB Video Capture: costoso, non preserva entrambi i campi, risultati peggiori del
necessario nonostante il brand professionale.

MP4 come container del master: penalizza MJPEG ad alto bitrate, non gestisce PCM nativo
in modo standard, fragile se il moov atom è corrotto, progettato per codec inter-frame.

S-Video dalla SCART del DAEWOO ST220: non disponibile. Il VCR somma Y e C internamente
prima dell'uscita SCART, pin 15 non cablato. Nessun cavo o adattatore può ripristinare Y/C
dopo la somma. L'upgrade richiederebbe un VCR che espone S-Video nativamente.

## Riferimenti a documentazione

_notes/manuali-e-specifiche/StarTech svid2usb23 composite to usb capture cable/ (manuale e driver)
_notes/settings/obs-settings-base/ (screenshot configurazione OBS prima cattura)
_notes/upscaling-topaz-AI/upscaling-topaz-AI.md (guida post-processing Topaz)
