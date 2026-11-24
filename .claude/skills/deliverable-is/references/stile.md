# Stile dei deliverable

## LaTeX
- Compilazione: XeLaTeX tramite `latexmk -silent main.tex` dalla cartella del deliverable.
- Una sezione per file in `sezioni/NN_nome.tex`, inclusa da `main.tex` con `\input`.
  Il file inizia con `\section{...}`; sottosezioni con `\subsection`.
- Colori definiti in `preambolo.tex`: `arancio` (intestazioni e bordi tabelle),
  `titolo`, `grigio`, `azzurro`. Non definire colori nuovi nelle sezioni.
- Tabelle con `tabularray`. Modello standard (divisibile tra pagine):

```latex
\begin{longtblr}[label=none, entry=none]{
  width=\linewidth, rowhead=1,
  colspec={X[1,l] X[3,l]},
  cells={font=\small},
  row{1}={bg=arancio, font=\small\bfseries},
  hline{2-Z}={wd=0.5pt, fg=arancio}
}
Colonna & Colonna \\
... \\
\end{longtblr}
```

- Codici in testo normale: RF-01, RNF-03, UC05; negli intervalli
  `\texttt{RF-01}--\texttt{RF-32}`.
- Riferimenti agli altri documenti nella forma "(D3, Sezione~5)".
- Pacchetti già presenti: tabularray, adjustbox, graphicx, needspace, tikz.
  Prima di aggiungerne uno, verificare che non si possa fare con questi.

## Italiano
- Registro: documento tecnico universitario, chiaro, alla terza persona
  ("il team", "il sistema"), frasi brevi, una idea per frase.
- Termini tecnici inglesi in corsivo alla prima occorrenza (\emph{black-box})
  con l'equivalente italiano quando esiste.
- Evitare lo stile da testo generato: niente elenchi di tre aggettivi, niente
  "è fondamentale/cruciale", niente frasi di apertura o chiusura vuote
  ("In conclusione...", "Questa sezione è molto importante"), niente
  grassetto sparso. Ogni frase deve dire qualcosa di verificabile sul progetto.
- Esempi sempre concreti e presi dal progetto (un RF, un UC, un sensore del
  telefono), non esempi generici.
- Accenti corretti (è, perché, più, così).

## Coerenza
- Nomi dei requisiti identici a D3 (Sezione 3 e Sezione 5).
- Soglie degli RNF identiche a D3 (Sezione 4).
- Ruoli del team e strumenti come in D2 (Sezioni 2 e 4).
- Date in formato gg/mm/aaaa; lo storico delle versioni si aggiorna solo alla consegna.
