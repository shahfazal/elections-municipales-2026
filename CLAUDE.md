# elections-municipales-2026

_Analyse open data : challenge data.gouv.fr · Date limite : 13 avril 2026 · Mot-clé : `defi-municipales-2026-résultats`_

---

## The question

Do property prices correlate with abstention rate and which political bloc won?

Three visualisations built:

1. **Scatter plot:** median prix/m² (x, log scale) vs abstention rate (y), one dot per commune, colour = winning bloc. 838 communes >9,000 inhabitants, 2nd round 22 March 2026.
2. **Box plot:** prix/m² distribution by winning political bloc.
3. **Paris–Lyon–Marseille choropleth:** arrondissement-level Leaflet maps, fill = winning bloc, circle size = median prix/m². DVF 2024 + 2025, one JSON per year, year toggle in viz.

## Political nuance schema

Sourced from the `bloc` column in `nuances.csv` (Ministère de l'Intérieur official coding). No manual remapping, use the `bloc` field directly from the nuances join.

| Bloc (`bloc`) | Example nuances             |
| ------------- | --------------------------- |
| EXG           | LEXG, LFI                   |
| GAU           | LCOM, LSOC, LVEC, LUG, LDVG |
| CENT          | LREN, LMDM, LHOR, LUC, LDVC |
| DTE           | LLR, LUD, LDVD, LDSV        |
| EXD           | LUDR, LRN, LREC, LUXD, LEXD |
| DIV           | LDIV, LECO, LREG            |

## Analysis level

Commune-level for scatter/boxplot. Arrondissement-level for PLM maps.

## Datasets used

- `commune.parquet`: 2nd-round commune-level results (838 communes with >9,000 inhabitants)
- `Paris_Lyon_BV.parquet`: Bureau de Vote-level 2nd-round results for Paris, Lyon, Marseille.
- `ValeursFoncieres-2024.txt` + `ValeursFoncieres-2025.txt`: DVF residential transactions (prix au m², one JSON per year)
- `nuances.csv`: nuance code → political bloc mapping

## Data pipeline

The original angle was transport access (GTFS stop density per commune) vs abstention and winning bloc. It was dropped: unclear whether the angle would produce anything meaningful given the data granularity available, and time constraints made it hard to justify pursuing further. The project pivoted to property prices (DVF) as the primary variable.

- `notebooks/01-data-exploration.ipynb`: initial schema exploration
- `notebooks/02-prix-logement.ipynb`: commune-level prix/m² + election results → `prix-logement-elections-2024.json` + `prix-logement-elections-2025.json`
- `notebooks/03-transport-gtfs.ipynb`: transport angle (dropped, deleted)
- `notebooks/04-plm-data.ipynb`: PLM arrondissement aggregation → `plm-secteurs-2024.json` + `plm-secteurs-2025.json`

## Viz architecture

Modular static files in `viz/`:

- `elections-municipales-2026.html`: shell only (structure, no inline CSS/JS)
- `elections-municipales-2026.css`: all styles
- `elections-municipales-2026.js`: all logic
  - (this could definitely be modeled better with ES modules, but a monolith for now in the interest of time)
- Plotly.js scatter + box plot
- Leaflet.js PLM choropleth (GeoJSON from data.gouv.fr)
- Driver.js help tours (3 tours, one per tab)
- All labels, tooltips, copy in French (informal "tu" tone)
- Jupyter notebooks in /notebooks/ (self-contained, outputs cleared before commit)
- Clean JSON in /data/processed/ → committed to repo
- Raw files in /data/raw/ → gitignored

## Output

- Viz as static HTML → `static/elections-municipales-2026/` in shahfazal/shahfazal.github.io
  - Served by Hugo at `shahfazal.com/elections-municipales-2026`
  - Static folder only: do NOT create a Hugo content page
- Réutilisation submitted on data.gouv.fr (in French)

## Repo structure

```
/notebooks/     - analysis notebooks
/data/
    /raw/       - gitignored
    /processed/ - committed, clean JSON for viz
/viz/           - static HTML + Plotly.js
/notes/         - analysis scratchpad
```

## Stack

- Python, pandas (data pipeline)
- Plotly.js, Leaflet.js, Driver.js (web viz)
- No ML, pure data analysis and visualization
- All viz labels, titles, tooltips in French

## Website integration

Viz output goes to shahfazal/shahfazal.github.io repo under `static/elections-municipales-2026/`

## Prior project context

- shahfazal's fourth project after TinyNet (23-param MLP), NYC EV charger LSTM and Claudio
- Active in French OpenData/AI space, contributes to MCP in front of data.gouv APIs
- GitHub: shahfazal, HuggingFace: shahfazal, Medium: @shahfazal
- Personal site: shahfazal.com (Hugo + PaperMod + GitHub Pages)
