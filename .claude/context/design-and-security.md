---
generated-from-commit: dc872289dadc6935754f704a70a382411d072fc4
generated-from-branch: main
generated-date: 2026-06-16
covers-paths:
  - .claude/context/**
last-verified-commit: dc872289dadc6935754f704a70a382411d072fc4
---

# Workflow di conversione e qualità del segnale

> Tracciato. Documenta il workflow dalla cassetta al master digitale, la fisica del segnale
> PAL composito e i criteri di qualità adottati. Fonte primaria: documento principale .docx.

## Il concetto critico: frames vs. fields

Un frame analogico PAL non è una singola immagine ma contiene due semiquadri catturati
in momenti distinti: le linee pari formano un campo (campo pari) e le linee dispari formano
l'altro (campo dispari). I due campi sono interlacciati in un unico frame. Separare i due
campi consente di ottenere 50 immagini distinte al secondo invece di 25, producendo un output
che riproduce fedelmente il movimento come visto su un monitor CRT.

Il criterio di selezione hardware è quindi uno solo: qualunque dispositivo di cattura deve
passare entrambi i campi senza scartarne uno. La maggior parte dei dongles economici da 10 EUR
usa driver che acquisiscono un solo campo, dimezzando irrecuperabilmente la qualità temporale.

## Fisica del segnale PAL composito in ingresso allo StarTech

Il segnale che entra nello StarTech è CVBS PAL analogico interlacciato (Composite Video
Baseband Signal). Le sue caratteristiche fisiche e temporali sono le seguenti.

Struttura spaziale: 625 linee totali, 576 linee attive, 49 linee VBI (blanking, teletext,
sync). Ogni campo contiene 312,5 linee totali, 288 linee attive.

Struttura temporale: scansione interlacciata 2:1 (576i), 50 campi/sec, 25 frame/sec. Ogni
frame è composto da un campo pari e un campo dispari catturati a 20 ms di distanza temporale.
Risoluzione nominale 720×576.

Composizione del segnale: luminanza Y (banda utile ~3 MHz), crominanza C modulata su una
sottocarrier a 4,43361875 MHz (PAL), encoding PAL (Phase Alternating Line, correzione
automatica errori di fase). Y e C si sovrappongono spettralmente, causando cross-color (dot
crawl) e cross-luma intrinseche al formato, non eliminabili via software senza perdita.

Livelli elettrici: ampiezza totale 1 Vpp. Sincronismi a -0,3V. Livello di nero a 0V. Livello
di bianco a +0,7V.

La risoluzione cromatica orizzontale reale delle VHS è ~30-40 linee TV, inferiore al nominale
4:2:2 digitale. Nessun codec può "perdere" crominanza che non esiste nella sorgente.

## Catena di qualità del segnale

La qualità del segnale è determinata dalla sorgente (VCR e nastro) e non dalla catena di
adattatori passivi. Gli adattatori SCART → RCA non introducono perdita perché non convertono
nulla: instradano i pin analogici fisicamente. La qualità è fissata nel momento in cui il
VCR somma Y e C per l'uscita SCART.

Il DAEWOO ST220 espone solo Composite (CVBS) sulla SCART: Y e C sono già sommati internamente,
il pin 15 (C) non è cablato. L'adattatore CABLEPELADO estrae giustamente solo Composite e
Audio dall'uscita SCART; la presa S-Video sull'adattatore rimane muta.

L'adattatore CABLEPELADO deve avere il micro-switch impostato fisicamente su OUT (uscita dal
VCR verso la capture card), non su IN. Con switch su OUT la catena è corretta.

Il passaggio successivo sensato per migliorare la qualità segnale, se il DAEWOO ST220 non
espone S-Video, è un VCR diverso che nativamente generi Y/C dalla SCART o un VCR S-VHS/Hi-Fi.
Nessun adattatore passivo può separare Y e C dopo che il VCR li ha già sommati.

## Workflow di cattura — fasi operative

1. Connessione hardware: VCR → SCART → adattatore (switch su OUT) → 3 RCA → StarTech USB.
2. Avvio OBS Studio: verificare che USB 2828x Device (video) e Linea USB 2828x Audio Device
   (audio) siano visibili come sorgenti selezionabili.
3. Configurazione profilo OBS: canvas 1440×1080 (4:3), nuovo profilo e nuova Scene Collection.
4. Impostare output master: AVI, MJPEG, 25-35 Mbps, 720×576, 25 fps, PCM 48kHz 16-bit.
5. Inserire la cassetta nel VCR, premere Play, verificare segnale in OBS (anteprima e Stats).
6. Avviare la registrazione. Monitorare frame dropped (Stats), livelli audio, stabilità segnale.
7. A fine cassetta, fermare la registrazione. Verificare il file AVI risultante.
8. Backup del master su secondo disco prima di qualsiasi post-processing.

## Criteri di qualità accettata allo stato dell'arte attuale

Questo progetto adotta il workflow standard della comunità DataHoarder per VHS su hardware
a basso costo. Le scelte tecniche riflettono i limiti intrinseci del formato VHS e dell'hardware:

Composite PAL è la qualità massima ottenibile dal DAEWOO ST220 senza sostituire il VCR.
MJPEG/AVI a ~30 Mbps è lo standard pratico per master VHS: preserva tutti i campi, non
introduce perdite temporali, compatibile ovunque. Il risultato è una fedele digitalizzazione
del segnale composito PAL interlacciato senza upscaling nel master.

L'upscaling (Topaz Video AI Pro 7.1) è un passo successivo separato sul master, non parte
del workflow di cattura.

## Gestione nastri degradati

Nastri con muffa: possibile se conservati in ambienti umidi. Richiede trattamento prima della
riproduzione (v. link nel documento principale).

Dirty heads: causano dropping e timing issues. Soluzione primaria: cleaning tape. Soluzione
avanzata: pulizia manuale smontando il VCR.

Nastri con segnale instabile: richiedono un Time Base Corrector (TBC). Il TBC interno
(line-TBC) è preferibile; il TBC esterno è costoso e difficile da reperire. L'approccio RF
decode (vhs-decode GitHub) offre TBC software di qualità superiore ai TBC hardware da 1000 EUR,
ma con complessità molto elevata (v. roadmap.md).

Nastri SLP (6-hour speed): qualità inferiore, più soggetti a dropping.

## Note sulla qualità dei connettori

La perdita di qualità su questa catena di adattatori passivi è nulla, confermato: gli
adattatori instradano i pin senza nessuna elaborazione. La qualità del connettore fisico
(resistenza di contatto, ossidazione dei pin) può invece influenzare il segnale su connettori
molto usurati, ma non è un problema per hardware nuovo.
