---
generated-from-commit: dc872289dadc6935754f704a70a382411d072fc4
generated-from-branch: main
generated-date: 2026-06-16
covers-paths:
  - _notes/annuncio-per-pubblicizzare/**
last-verified-commit: dc872289dadc6935754f704a70a382411d072fc4
---

# Distribuzione ai clienti

> Tracciato. Documenta come il prodotto digitale raggiunge il cliente finale: formati di output,
> supporto fisico, file system e comunicazione del servizio. Non c'è deployment software.

## Formati di output offerti

Il workflow produce due tipi di file distinti che servono scopi diversi.

Il master AVI+MJPEG (~28-30 GB per 2 ore) è il file di archivio: preserva la qualità massima
ottenibile dal segnale PAL composito del VCR. Non viene consegnato al cliente nella forma
grezza per ragioni pratiche di dimensione, ma è la sorgente da cui si generano tutti gli output.

Il file di distribuzione è un derivato compresso del master, adatto alla fruizione su player
moderni e alla condivisione. Il formato e la qualità del derivato sono da definire (MP4/H.264
o MP4/H.265 a bitrate sufficiente per preservare la qualità VHS visiva).

L'upscaling con Topaz Video AI Pro 7.1 può essere applicato al master prima della compressione
finale per offrire ai clienti un output visivamente migliorato senza artefatti di deinterlace.
Dettagli tecnici in _notes/upscaling-topaz-AI/upscaling-topaz-AI.md.

## Supporto fisico di consegna — USB drive

La consegna principale avviene tramite chiavetta USB fornita al cliente. Il file system della
chiavetta è critico perché un master AVI supera facilmente i 4 GB, il limite del file system
FAT32 che le chiavette USB vengono tipicamente formattate in fabbrica.

Le opzioni di file system praticabili su Windows sono due.

exFAT è progettato per supporti rimovibili, compatibile con Windows, macOS e Linux, non impone
il limite dei 4 GB per singolo file, mantiene una struttura semplice. È la scelta corretta se
la chiavetta deve essere letta su sistemi eterogenei (Windows, Mac, Smart TV).

NTFS è il file system nativo di Windows, più complesso, progettato per dischi interni.
Supporta file di grandi dimensioni, gestisce errori in modo più robusto rispetto a exFAT e
permette la cifratura con BitLocker To Go (protezione dei dati del cliente con password).
Non è nativamente scrivibile su macOS senza software aggiuntivo, ma è leggibile.

In un contesto di consegna a clienti privati su Windows con esigenza di protezione dati,
NTFS con BitLocker To Go offre un livello di sicurezza superiore e non presenta svantaggi
se il cliente usa Windows. Se il cliente usa Mac o ha esigenze cross-platform, exFAT è più
adeguato.

### Procedura di formattazione USB su Windows 11

Questo PC → tasto destro sull'unità USB → Formatta → scegliere exFAT o NTFS → Avvia.

Se la chiavetta è acquistata dal cliente e di scarsa qualità, verificare prima che non sia
in write protection software (Windows monta il drive in sola lettura per errori rilevati) o
hardware (interruttore fisico su alcuni modelli). In caso di write protection software:
eseguire un controllo disco o riformattare. Documentazione completa in "formattare USB
(giusto se clienti comprano USB pen di scarsa qualità).docx" (ignorato da git).

## Comunicazione e pubblicità del servizio

Materiali preparati (in _notes/annuncio-per-pubblicizzare/, ignorati da git):
- Annuncio.txt: testo dell'annuncio per piattaforme online
- Volantino VHS converter.pdf: volantino stampabile
- idea_fascia_prezzo.txt: bozza fasce di prezzo
- canva_edit_volantino.url: link all'editor Canva del volantino

Il pricing definitivo non è ancora fissato. La struttura fiscale per la prestazione occasionale
senza partita IVA è documentata nel file .lnk presente nella stessa cartella.

## Da definire

Il workflow cliente end-to-end non è ancora formalizzato. Aperti i seguenti punti: modalità
di ricezione delle cassette (fisica, spedizione), tempi di lavorazione dichiarati, struttura
del prezzo (a cassetta, a ora, a GB), eventuale offerta di livelli di qualità distinti
(composito senza upscaling vs upscaling Topaz), gestione delle cassette di formato diverso
(VHS-C, 8mm). Questi punti appartengono alla roadmap.md.
