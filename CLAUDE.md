# elections-municipales-2026

*Analyse open data — challenge data.gouv.fr · Date limite : 13 avril 2026 · Mot-clé : `defi-municipales-2026-résultats`*

---

## The angle — v0.1

Two questions, same data:
1. Does public transport access correlate with **abstention rate**?
2. Does public transport access correlate with **which political bloc won**?

Both answered in one scatter plot: transport score (x), abstention rate (y), colour = winning bloc per commune. The colour answers question 2; the y-axis answers question 1.

## Political nuance schema

Sourced from the `bloc` column in `nuances.csv` (Ministère de l'Intérieur official coding). No manual remapping — use the `bloc` field directly from the nuances join.

| Bloc (`bloc`)  | Example nuances             |
| -------------- | --------------------------- |
| EXG            | LEXG, LFI                   |
| GAU            | LCOM, LSOC, LVEC, LUG, LDVG |
| CENT           | LREN, LMDM, LHOR, LUC, LDVC |
| DTE            | LLR, LUD, LDVD, LDSV        |
| EXD            | LUDR, LRN, LREC, LUXD, LEXD |
| DIV            | LDIV, LECO, LREG             |
| Abstention     | derived from participation data |

## Analysis level

Commune-level (not bureau de vote) — clean join with BPE transport data.

## Datasets to use

- `Données des élections agrégées` — general-results.csv + candidats-results.csv
- `Elections municipales 2026 - Résultats du second tour` (Ministère de l'Intérieur)
- `Base permanente des équipements (BPE)` — filter for transport equipment codes (**TBD — see BPE documentation for relevant TYPEQU codes, e.g. transport stops, stations**)
- `Population (3 tranches d'âge)` — INSEE commune-level demographics (control variable)

## Data pipeline

pandas notebook → aggregate bureau de vote → commune → join BPE transport → clean JSON → Plotly.js viz on shahfazal.com

## Primary visualisations (both)

1. **Choropleth map** — communes coloured by abstention rate or transport score. Geographic story. datagouv explicitly encourages maps.
2. **Scatter plot** — transport score (x) vs abstention rate (y), one dot per commune, coloured by winning bloc. Shows both correlations at once: transport → abstention (y-axis), transport → political colour (dot colour).

Map tells the story. Scatter proves the point.

## Output

- Jupyter notebook in /notebooks/ (self-contained, all code inline)
- Clean JSON in /data/processed/ → committed to repo
- Raw CSVs in /data/raw/ → gitignored
- Viz as static HTML+JS → deployed to shahfazal.com/elections-2026
  - These are the same thing: `static/elections-2026/` in shahfazal/shahfazal.github.io is served by Hugo at `shahfazal.com/elections-2026`. Do NOT create a Hugo content page AND a static folder — static folder only.
- Réutilisation submitted on data.gouv.fr (in French)

## Repo structure

```
/notebooks/     — analysis notebook(s)
/data/
    /raw/       — gitignored, downloaded CSVs
    /processed/ — committed, clean JSON for viz
/viz/           — static HTML + Plotly.js
```

## Stack

- Python, pandas, plotly (Python for exploration)
- Plotly.js for the web viz
- No ML — pure data analysis and visualization
- All viz labels, titles, tooltips in French

## Website integration

Viz output goes to shahfazal/shahfazal.github.io repo under static/elections-2026/
Project page at shahfazal.com/projects/elections-2026 to be created (English first, French version later when Hugo multilingual is set up).

## Prior project context

- shahfazal's third project after TinyNet (23-param MLP) and NYC EV charger LSTM
- Active in French OpenData/AI space, contributes to MCP in front of data.gouv APIs
- GitHub: shahfazal, HuggingFace: shahfazal, Medium: @shahfazal
- Personal site: shahfazal.com (Hugo + PaperMod + GitHub Pages, just launched)
