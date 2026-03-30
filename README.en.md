# 2026 French Municipal Elections — Transport & Abstention

Entry for the [data.gouv.fr open data challenge](https://www.data.gouv.fr/posts/ouverture-du-challenge-open-data-resultats-des-elections-municipales).
Deadline: **April 13, 2026** · Keyword: `defi-municipales-2026-résultats`

---

## The question

Two questions, same data:

1. Does public transport access correlate with **abstention rate**?
2. Does public transport access correlate with **which political bloc won**?

Each commune becomes a dot: x = transport score, y = abstention rate, colour = winning bloc. The y-axis answers question 1, the colour answers question 2.

## Visualisations

1. **Choropleth map** — communes coloured by abstention rate or transport score. The geographic story.
2. **Scatter plot** — transport score (x) vs abstention rate (y), one dot per commune, coloured by winning bloc. Three dimensions, one chart: transport → abstention (y-axis) and transport → political colour (dot colour).

> **v1** — transport score vs abstention rate vs winning political bloc, submitted for the challenge.
> Further visualisations planned: urban/rural profile, demographics vs abstention.

## Simplified political schema

| Bloc (`bloc`)  | Example nuances                   |
| -------------- | --------------------------------- |
| Extrême gauche | LEXG, LFI                         |
| Gauche         | LCOM, LSOC, LVEC, LUG, LDVG       |
| Centre         | LREN, LMDM, LHOR, LUC, LDVC, LUDI |
| Droite         | LLR, LUD, LDVD, LDSV              |
| Extrême droite | LUDR, LRN, LREC, LUXD, LEXD       |
| Divers / local | LDIV, LECO, LREG                  |
| Abstention     | derived from participation data   |

> The political nuance codes are the Ministère de l'Intérieur's official system. The `bloc` column in the source data already groups them — this schema uses it directly, no manual remapping.

## Data sources

| Source                   | Description                                                |
| ------------------------ | ---------------------------------------------------------- |
| Ministère de l'Intérieur | Aggregated results + candidates, 2026 municipal elections  |
| INSEE — BPE              | Base permanente des équipements, transport equipment codes |
| INSEE — Population       | Age distribution by commune (control variable)             |

## Repo structure

```
/notebooks/          — analysis notebook (self-contained)
/data/
    /raw/            — raw CSVs (gitignored)
    /processed/      — clean JSON for viz (versioned)
/viz/                — static HTML + Plotly.js
```

## Running the analysis

```bash
# with uv (recommended)
uv sync
uv run jupyter notebook notebooks/

# or with pip
pip install pandas plotly jupyter pyarrow
jupyter notebook notebooks/
```

## Output

Viz will be deployed at [shahfazal.com/elections-municipale-2026](https://shahfazal.com/elections-municipale-2026)

Réutilisation submitted on data.gouv.fr

---

_Project by [shahfazal](https://github.com/shahfazal)_
