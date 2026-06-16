---
generated-from-commit: dc872289dadc6935754f704a70a382411d072fc4
generated-from-branch: main
generated-date: 2026-06-16
covers-paths:
  - _notes/settings/**
last-verified-commit: dc872289dadc6935754f704a70a382411d072fc4
---

# Test e validazione della cattura

> Tracciato. Documenta le procedure di verifica della qualità della cattura e i problemi noti
> con le relative soluzioni. Non ci sono test software automatici: tutto è manuale.
> La checklist operativa locale vive in _notes/TEST-CHECKLIST.md, ignorata da git.

## Verifica dell'installazione hardware e driver (one-time)

Lo StarTech SVID2USB232 su Windows 10/11 richiede il driver BDA, non il CD incluso nella
confezione. Il CD contiene driver legacy che non dichiarano compatibilità con VID_EB1A&PID_8286
e il relativo Setup.exe fallisce silenziosamente. Il driver corretto si scarica da
startech.com/SVID2USB232: installer Setup_5.2021.080.3.exe, pacchetto BDA051321.2
v5.2021.0513.2, firmato digitalmente, installabile normalmente come amministratore.

Nella stessa cartella del download è presente anche un "Twain Driver": questo driver non è
firmato digitalmente e richiede di disabilitare il Driver Signature Enforcement a ogni riavvio
di Windows (da Opzioni di avvio avanzate, tasto 7 o F7). Non è la via adottata in questo
progetto e non va usato: il BDA driver copre la stessa funzione senza richiedere modifiche al
boot. I file del Twain Driver sono conservati in _notes/manuali-e-specifiche/ come riferimento.

Dopo installazione del BDA driver e riavvio Windows, collegare lo StarTech e verificare
in Gestione dispositivi sotto "Controller audio, video e giochi" la presenza di due voci senza
triangolo giallo: "USB 2828x Audio Device" e "USB 2828x Device". L'assenza di triangoli gialli
e l'assenza di voci sotto "Altri dispositivi" confermano il corretto riconoscimento di entrambe
le interfacce del dispositivo composito USB.

## Configurazione OBS Studio — verifica preliminare

Aprire OBS Studio. In Fonti → + → Dispositivo di cattura video: deve apparire "USB 2828x
Device" nel menu a tendina. In Fonti → + → Cattura l'audio in entrata: deve apparire "Linea
(USB 2828x Audio Device)" nel menu a tendina. Se entrambi compaiono, il driver espone
correttamente il flusso video BDA e l'interfaccia audio PCM.

Screenshot di riferimento della configurazione base: _notes/settings/obs-settings-base/

## Configurazione OBS per il master — impostazioni target

Per produrre il master VHS si imposta OBS con il profilo seguente.

Canvas: 1440×1080 (da Impostazioni → Video; 4:3 PAL). Nuovo profilo dedicato (Profilo → Nuovo)
e nuova Scene Collection (Scene Collection → Nuovo) per non contaminare altri profili.

Output master (Impostazioni → Uscita → Registrazione):
- Qualità della registrazione: "Lossless con dimensioni del file enormi"
- Formato di registrazione: AVI
- Encoder video: MJPEG (Software)
- Qualità encoder: 90-95 oppure bitrate 25-35 Mbps
- Risoluzione output: 720×576
- Frame rate: 25 fps

Output audio:
- Encoder audio: PCM non compresso
- 48 kHz, 16 bit, stereo

Monitoraggio: Docks → Stats abilita la finestra con frame catturati, frame mancati e frame
saltati. È il pannello principale da tenere visibile durante la cattura.

Monitoraggio audio: Focusrite Scarlett 2i4 impostata come dispositivo di output Windows; in
OBS Proprietà audio avanzate → attivare il monitoraggio sul canale audio della capture card.

## Prima cattura di test (eseguita — impostazioni subottimali)

La prima cattura è stata effettuata con le impostazioni default di OBS "Alta qualità,
dimensioni dei file medie", container MP4 ibrido [BETA], encoder H.264 QSV hardware,
audio AAC 160 kbps. Il risultato (~5.4 GB per 2 ore) non è adatto come master ma può
essere usato per verificare la catena hardware senza occupare 30 GB di disco.

## Troubleshooting — problemi noti e soluzioni

### Frame dropping con CPU alto

Sintomo: frame mancati nel pannello Stats di OBS, CPU Usage elevato. Soluzione: ridurre
la risoluzione del canvas di anteprima a 960×720. Questa riduzione non tocca il segnale
registrato se l'output è impostato correttamente a 720×576. Il problema non si presenta su
hardware post-2010 in condizioni normali.

### Frame dropping con CPU basso (timing issues)

Sintomo: frame mancati anche con CPU < 80%. Cause probabili: nastro usurato (velocità SLP,
registrazione di scarsa qualità originale), testine VCR sporche. Soluzione primaria: cleaning
tape. Soluzione avanzata: pulizia manuale delle testine smontando il VCR. Se il problema
persiste dopo la pulizia, è necessario un Time Base Corrector (TBC) hardware, opzione costosa.

### Audio assente dalla capture card

Causa: incompatibilità tra driver, sistema operativo e dispositivo. Soluzione: usare la
Focusrite come sorgente audio alternativa aggiungendo in OBS una sorgente "Cattura audio in
entrata" separata dalla capture card. OBS combinerà le due sorgenti durante la registrazione.
È troubleshooting per tentativi.

### Audio drift / desync

Sintomo: audio fuori sincronismo nel file registrato. Causa principale: troppi frame dropped
(v. sopra). Soluzione alternativa se i frame sono OK: impostare un valore di offset audio
nelle proprietà avanzate della sorgente audio in OBS.

### Audio solo su un canale

Causa A: il VCR ha un solo connettore di uscita audio. Soluzione: adattatore mono-to-stereo
tra il cavo RCA bianco/rosso e lo StarTech, per duplicare il canale su entrambi L e R.
Causa B: la registrazione originale era mono. Soluzione: in OBS → sorgente audio → Proprietà
audio avanzate → selezionare "MONO" per mixare i due canali in mono.

### Video jittery / jumpy (frames fuori ordine)

Sintomo: output video con movimenti a scatti o ordine dei campi invertito. Causa: ordine dei
campi (field order) errato. Soluzione: tasto destro sulla sorgente video in OBS → Deinterlacing
→ Top Field First. Se non risolve, provare Bottom Field First.

### Dispositivi cheap che forzano il deinterlacciamento

Alcuni dispositivi economici forzano il deinterlacciamento a livello driver ma espongono tutti i
campi se impostati ad alta frequenza. In questo caso: in OBS impostare la sorgente con
Resolution/FPS Type Custom, risoluzione 720×576 (PAL) o 720×480 (NTSC), FPS al massimo
disponibile; NON applicare Deinterlacing-Yadif 2x. Lo StarTech SVID2USB232 non rientra in
questa categoria: preserva l'interlacciamento nativamente.

## Verifica del file master prodotto

Dopo ogni cattura verificare: durata corretta rispetto alla cassetta, dimensione coerente
(~3.95 MB/s × durata in secondi = peso atteso), sincronismo audio/video su campioni a inizio
metà e fine file, assenza di artefatti visivi macroscopici (bande nere, desaturazione).
