# analog-to-digital-VHS-converter

> Istruzioni di team, versionate. Questo file è l'indice del progetto: indicizza i soli file
> satellite tracciati e descrive la procedura di ripresa. Le preferenze personali vivono in
> `CLAUDE.local.md`, ignorato da git, non qui.

## Cos'è questo progetto

Workflow e documentazione tecnica per la conversione di cassette VHS in formato digitale:
procedura di cattura analogica con OBS Studio, standard del master digitale (PAL 720×576,
MJPEG/AVI, PCM 48kHz), post-processing con Topaz Video AI Pro 7.1 e specifiche hardware
(StarTech SVID2USB232, VCR DAEWOO ST220). Non è un progetto di sviluppo software: è un
sistema di documentazione operativa e workflow di servizio per clienti privati.

## Procedura di ripresa in una sessione nuova

Lo stato del progetto è interamente recuperabile su disco. All'inizio di una sessione si segue
questo percorso fisso. Si legge per primo `.claude/memory/index.md`, che dà branch, commit di
riferimento, stato di verifica di ogni scheda e punto di ripresa. Si legge poi
`.claude/context/current-work.md` se c'è una feature attiva, per sapere cosa è in lavorazione e
quali sono i TODO e i limiti d'ambiente. Si invoca la skill `sync-context` per verificare il
drift tra schede e codice, e si leggono solo le schede pertinenti al task, mai tutte insieme. Il
work-log `.claude/memory/progress.md` e il registro `.claude/memory/decisions.md` forniscono la
storia e le decisioni quando servono. Il materiale grezzo sotto `_notes/` si apre solo per
verificare un requisito originale. Per una ripresa rapida esiste, quando presente,
`_notes/RESUME-PROMPT.md`, privato e ignorato: riporta lo stato raggiunto e un prompt pronto da
incollare. Va aggiornato alla fine di ogni sessione con il punto in cui si è arrivati, mentre lo
stato canonico resta `.claude/memory/index.md`.

## Indice dei file satellite tracciati

Memoria e meta-stato, sotto `.claude/memory/`, letti sempre a inizio sessione.

```
.claude/memory/index.md       snapshot e tabella di sincronizzazione, da leggere per primo
.claude/memory/progress.md    work-log append-only di passi e riconciliazioni
.claude/memory/decisions.md   registro ADR-lite delle decisioni architetturali
```

Schede tecniche, sotto `.claude/context/`, con frontmatter di riconciliazione.

```
.claude/context/STACK.md                hardware, software, standard di codifica
.claude/context/design-and-security.md  workflow di conversione e catena di qualità del segnale
.claude/context/deployment.md           distribuzione ai clienti, formati di consegna
.claude/context/dev-testing.md          procedure di test della cattura e checklist di verifica
.claude/context/current-work.md         attività in corso, definition of done, domande aperte
.claude/context/roadmap.md              direzione e priorità del progetto
```

Regole modulari caricate su necessità, sotto `.claude/rules/`, e skill richiamabili, sotto
`.claude/skills/`. Lo standard di sistema completo è in `.claude/PROJECT-SYSTEM.md`.

## Vincoli di team

Le operazioni di `git add`, commit e push restano sempre manuali dell'utente: l'agente prepara i
file, non committa. L'identità git è impostata a livello locale del repo secondo
`.claude/rules/git-identity-and-repo.md`. Lo stile di documentazione e di interazione è quello di
`.claude/rules/interaction-style.md`. Claude non scrive autonomamente nei file di memoria e di
contesto: li aggiorna solo su richiesta esplicita, così il versionamento resta sotto controllo
umano.

## MCP

Nessun server MCP configurato per questo progetto. Può essere aggiunto in seguito creando
`.mcp.json` in radice e la cartella `mcp/`, istanziando il template opzionale in
`.claude/templates/mcp.json`.
