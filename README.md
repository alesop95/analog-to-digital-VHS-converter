# analog-to-digital-VHS-converter

Documentazione del workflow e della pipeline hardware/software per la conversione di cassette
VHS in formato digitale. Il progetto copre la selezione e l'installazione dell'hardware di
cattura, la configurazione di OBS Studio per PAL composito interlacciato, gli standard del
master digitale e il post-processing con upscaling AI.

---

## Hardware

| Componente | Modello | Note |
|---|---|---|
| VCR | DAEWOO ST220 | PAL-B/G, uscita SCART composita |
| Capture card | StarTech SVID2USB232 | chip EM28xx, ingresso Composite + S-Video |
| Audio monitoring | Focusrite Scarlett 2i4 2nd Gen | linea-in come sorgente audio OBS |

Catena segnale: SCART femmina VCR - cavo SCART maschio-maschio - adattatore SCART-RCA passivo
(switch su OUT) - 3 RCA - StarTech ingresso Composite.

Il segnale e' CVBS PAL composito analogico interlacciato (576i, 25 frame/sec, 50 campi/sec).
L'adattatore e' passivo e non introduce perdita: la qualita' e' fissata alla sorgente.

---

## Software

| Applicazione | Uso |
|---|---|
| OBS Studio | cattura, encoding, monitoring |
| Topaz Video AI Pro 7.1 | upscaling e post-processing AI (CPU-only) |

OS: Windows 11. Driver capture card: BDA051321.2 v5.2021.0513.2 (da startech.com, non il CD
incluso, che e' obsoleto su Windows 10/11).

---

## Il concetto critico: frames vs. fields

Un frame VHS analogico non e' una singola immagine: contiene due semiquadri (campi pari e
dispari) catturati in momenti distinti e interlacciati. Preservarli entrambi produce 50 immagini
distinte al secondo invece di 25 e riproduce il movimento in modo fedele all'originale.

Il criterio di selezione dell'hardware e' uno solo: il dispositivo di cattura deve passare
entrambi i campi senza scartarne uno. La maggior parte dei dongle da 10 EUR non lo fa: i
driver acquisiscono un solo campo e la perdita e' irrecuperabile via software.

---

## Standard del master digitale (PAL)

| Parametro | Valore |
|---|---|
| Container | AVI |
| Codec video | MJPEG (intra-frame, ~30 Mbps) |
| Risoluzione | 720x576 |
| Frame rate | 25 fps interlacciato - Top Field First, nessun deinterlace sul master |
| Spazio colore | YUV 4:2:2, BT.601 |
| Codec audio | PCM non compresso |
| Frequenza audio | 48 kHz, 16-bit, stereo |
| Peso per 2 ore | ~28-30 GB |

MJPEG e' intra-frame: ogni fotogramma e' indipendente, ideale per il rumore analogico
imprevedibile della VHS. Il container AVI accetta PCM nativo e flussi interlacciati senza
forzare strutture di streaming. MP4 non e' adatto come container per il master.

In OBS: Impostazioni - Uscita - Registrazione - Qualita' della registrazione: "Lossless con
dimensioni del file enormi", formato AVI.

---

## Pipeline di produzione

```
Cassetta VHS
    |
    v
VCR (DAEWOO ST220) -- SCART -- adattatore RCA -- StarTech SVID2USB232
    |
    v
OBS Studio -- master AVI+MJPEG+PCM (~30 GB / 2h)
    |
    v
[opzionale] Topaz Video AI Pro 7.1 -- upscaling AI su CPU
    |
    v
output compresso per la consegna al cliente
```

---

## Segnale PAL composito -- caratteristiche tecniche

Il DAEWOO ST220 espone solo Composite (CVBS) sulla SCART: luminanza Y e crominanza C sono
sommati internamente. Nessun cavo o adattatore puo' separarli di nuovo. Le caratteristiche
fisiche del segnale in ingresso allo StarTech:

- 625 linee totali, 576 attive, 288 attive per campo
- Luma bandwidth ~3 MHz, chroma modulata a 4.43361875 MHz (PAL)
- Livelli elettrici: 1 Vpp totali, bianco a +0.7V, sincronismi a -0.3V
- Dot crawl e cross-color sono intrinseci al CVBS, non eliminabili senza perdita

Un eventuale upgrade del segnale richiede un VCR che esponga S-Video (Y/C) nativamente sulla
SCART -- non e' una questione di cavi, ma di elettronica interna del VCR.

---

## Troubleshooting noto

**Frame dropping con CPU alta:** ridurre la risoluzione del canvas di anteprima a 960x720.

**Frame dropping con CPU bassa:** testine VCR sporche o nastro usurato. Cleaning tape come
primo intervento; TBC hardware come ultima ratio per nastri con segnale instabile.

**Audio solo su un canale:** adattatore mono-to-stereo tra VCR e StarTech, oppure checkbox
MONO nelle proprieta' audio avanzate di OBS.

**Video jittery:** tasto destro sulla sorgente video OBS - Deinterlacing - Top Field First.

---

## Stato

- [x] Catena hardware funzionante e documentata
- [x] Driver StarTech installati su Windows 11 (BDA051321.2)
- [x] OBS Studio configurato e verificato (prima cattura di test completata)
- [x] Standard master MJPEG/AVI definiti e documentati
- [ ] Prima cattura master con impostazioni MJPEG/AVI
- [ ] Workflow post-processing Topaz formalizzato
- [ ] Workflow cliente definito (prezzi, formati, consegna)

---

## Riferimenti

- Capture card: startech.com/SVID2USB232
- OBS Studio: obsproject.com
- Comunita' di riferimento: reddit.com/r/DataHoarder
- RF decode avanzato: github.com/oyvindln/vhs-decode
