# Registro delle decisioni architetturali

> Convenzione ADR-lite, append-only. Ogni decisione non ovvia entra come voce numerata con
> data, stato, contesto, decisione, motivazione e conseguenze. Una decisione non si cancella
> e non si riscrive: quando viene superata, si aggiunge una nuova voce che dichiara di
> superare la precedente e ne cita il numero. Le inferenze non confermate si marcano come
> da verificare e si promuovono a decisione solo quando una fonte le conferma.

## ADR-001 — Adozione del sistema di progetto portabile

Data: 2026-06-16
Stato: accettata
Contesto: il progetto necessita di uno stato interamente recuperabile da un clone e di
documentazione che resti allineata al materiale senza rilettura integrale a ogni sessione.
Trattandosi di un progetto non-codice (workflow e documentazione tecnica), le schede context/
sono adattate per documentare hardware, software, standard e procedure invece di moduli
software.
Decisione: adottare il sistema descritto in .claude/PROJECT-SYSTEM.md, con motore di
riconciliazione ancorato ai commit e doppio livello documentale tracciato/ignorato.
Motivazione: persistenza strutturale su disco indipendente dalla sessione di chat, e controllo
umano sul versionamento.
Conseguenze: ogni passo significativo aggiorna schede, last-verified-commit, snapshot e
work-log; commit e push restano manuali.

## ADR-002 — Standard master digitale PAL

Data: 2026-06-16
Stato: accettata
Contesto: occorre scegliere codec, container, risoluzione e framerate per il file master
prodotto dalla cattura VHS.
Decisione: MJPEG (~30 Mbps) in container AVI, 720×576, 25 fps, PCM 48 kHz 16-bit stereo.
Motivazione: MJPEG è intra-frame (ogni fotogramma indipendente, ideale per archivio e
post-processing), AVI mantiene entrambi i campi dell'interlacciamento. Standard consolidato
nella comunità DataHoarder per VHS PAL.
Conseguenze: file di grandi dimensioni (~28-30 GB per 2 ore); si comprimono in uscita per il
cliente, il master resta non compresso.

<!-- ADR-003 — <titolo>
Data: <YYYY-MM-DD>
Stato: <proposta / accettata / superata da ADR-NNN>
Contesto: ...
Decisione: ...
Motivazione: ...
Conseguenze: ... -->
