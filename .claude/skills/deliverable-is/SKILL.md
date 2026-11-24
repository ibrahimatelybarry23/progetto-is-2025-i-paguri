---
name: deliverable-is
description: Scrive, completa o revisiona un deliverable (D1–D7) o una sua sezione del progetto di Ingegneria del Software "I paguri" (app Android per il Laboratorio in Campo). Coordina un team di agenti esperti — lettore delle slide, estrattore del contesto dai deliverable precedenti, esperti di dominio che scrivono in LaTeX e un revisore — così che ogni sezione corrisponda a ciò che chiedono le slide del docente e sia coerente con D1–D3. Usala quando l'utente chiede di fare, scrivere, completare, controllare o migliorare un deliverable, una sezione, o di verificare che "corrisponda alle slide".
---

# Deliverable IS — team di agenti

Il progetto è una serie di documenti LaTeX consegnati al docente (D0–D7, vedi
[references/calendario.md](references/calendario.md)). Ogni documento deve
**corrispondere a ciò che chiedono le slide** e **restare coerente con i
deliverable già consegnati**. I due errori più frequenti sono: scrivere da un
riassunto invece che dalle slide, e inventare fatti (strumenti, numeri, ruoli)
che non sono in D1–D3. Questa skill esiste per evitarli.

## Il team

| Agente | Campo | Cosa produce |
|---|---|---|
| `lettore-slide` | Didattica del corso | `appunti/Dx/slide.md`: checklist di ciò che il docente chiede, con numero di slide |
| `estrattore-contesto` | Tracciabilità e gestione della configurazione | `appunti/Dx/contesto.md`: fatti da D0–D3 (RF, RNF, UC, ruoli, strumenti, date) con file:riga |
| `esperto-requisiti` | Ingegneria dei requisiti | Sezioni di D1, D3 (requisiti, casi d'uso, specifica, tracciabilità) |
| `esperto-project-management` | Gestione del progetto | Sezioni di D2 e parti di pianificazione di altri deliverable |
| `esperto-testing` | Verifica e validazione | Sezioni di D4 (tecniche, criteri, casi di test, registrazione) |
| `esperto-progettazione` | Architettura e progettazione | Sezioni di D5 (architettura, UML, pattern, interfacce) |
| `esperto-android` | Sviluppo Android/Java | Codice e documentazione tecnica di D6–D7 |
| `revisore` | Qualità del software e della documentazione | `appunti/Dx/revisione.md`: problemi per gravità, mai modifiche dirette |

I subagenti non possono avviare altri subagenti: **sei tu (sessione principale)
il coordinatore**. Avvii gli agenti con lo strumento Agent, passi loro i
percorsi dei file prodotti dai passi precedenti e decidi quando il lavoro è
finito.

## Flusso

### 0. Inquadra la richiesta
Stabilisci: quale deliverable (Dx), quali sezioni, quale file di slide
(`~/Downloads/2026_IS_*.pdf`, vedi calendario). Se l'utente lavora solo su
alcune sezioni (es. "io devo fare le tecniche e la registrazione"), limita
tutto il flusso a quelle. Crea la cartella `appunti/Dx/` se manca.

### 1. Lettura ed estrazione — in parallelo
Avvia **nello stesso messaggio** due agenti in background:
- `lettore-slide` con il PDF delle slide e le sezioni richieste;
- `estrattore-contesto` con il deliverable e le sezioni richieste.

Non procedere finché entrambi non hanno scritto il loro file. Leggili tu:
se la checklist delle slide contiene un punto che non sai a quale sezione
assegnare, chiedi all'utente invece di indovinare.

### 2. Stesura
Avvia l'esperto di dominio adatto (vedi tabella). Se le sezioni toccano due
campi (es. D4 "modalità di verifica dei requisiti" = testing + requisiti),
avvia l'esperto principale e indica nel prompt l'altro campo da considerare.
Passa sempre: percorso di `slide.md`, `contesto.md`, file `.tex` da scrivere,
e [references/stile.md](references/stile.md). Se il `.tex` contiene già testo
scritto dall'utente, l'esperto lo migliora e lo completa, non lo butta.

### 3. Revisione — al massimo 2 giri
Avvia `revisore` sugli stessi file. Se trova problemi **bloccanti** o
**importanti**, rimanda all'esperto solo l'elenco di quei punti; poi una
seconda revisione. Dopo 2 giri fermati e riporta all'utente ciò che resta
aperto: non entrare in un ciclo infinito.

### 4. Compilazione e consegna all'utente
Compila nella cartella del deliverable con `latexmk -silent main.tex` (XeLaTeX,
può richiedere qualche minuto: usa un timeout ampio). Controlla `main.log` per
righe che iniziano con `!` e per riferimenti indefiniti. Poi rispondi
all'utente in italiano con:
- cosa è stato scritto e come corrisponde ai punti delle slide (numeri di slide);
- le scelte fatte senza una fonte (marcate `% DA VERIFICARE` nel `.tex`);
- i problemi rimasti dalla revisione.

Non fare commit né push senza che l'utente lo chieda.

## Modalità rapide
- **"Controlla se corrisponde alle slide"**: solo passi 1 e 3 (lettore-slide +
  estrattore-contesto, poi revisore). Nessuna modifica ai `.tex`.
- **Sezione piccola o correzione puntuale**: salta l'estrattore se il contesto
  necessario è già in `appunti/Dx/contesto.md` e non è cambiato.

## Regole che valgono per tutti gli agenti
- **Fonte o niente**: ogni contenuto viene dalle slide, da D0–D3 o dalla
  richiesta dell'utente. Una scelta senza fonte (uno strumento, una soglia, un
  ruolo) è ammessa solo se necessaria, e va marcata nel `.tex` con un commento
  `% DA VERIFICARE: <motivo>` e riportata all'utente.
- **Codici stabili**: RF-01–RF-32, RNF-01–RNF-19, UC01–UC15, TC-xx. Mai
  rinumerare; mai citare un codice che non esiste in D3.
- **Le slide prevalgono** sulla conoscenza generale: se il docente usa una
  definizione o una convenzione (es. "un test ha successo se rileva un
  errore"), si usa quella.
- I file in `appunti/` sono materiale di lavoro: non vanno nello zip di consegna.
