# 2026 French Municipal Elections — Transport & Abstention

Entry for the [data.gouv.fr open data challenge](https://www.data.gouv.fr/posts/ouverture-du-challenge-open-data-resultats-des-elections-municipales).
Deadline: **April 13, 2026** · Keyword: `defi-municipales-2026-résultats`

---

## The question

Does public transport access in a commune influence voter abstention in municipal elections?

We cross-reference electoral results (Ministère de l'Intérieur) with transport equipment density from the BPE (INSEE), at commune level, to test this correlation — and layer in political nuance to deepen the reading.

## Visualisations

1. **Choropleth map** — communes coloured by abstention rate or transport score. The geographic story.
2. **Scatter plot** — transport score (x) vs abstention rate (y), one dot per commune, coloured by political bloc. The correlation, directly.

> **v1** — initial analysis, submitted for the challenge.
> Further visualisations planned: urban/rural profile, demographics vs abstention, transport score vs winning bloc.

## Simplified political schema

| Group          | Nuances included                |
| -------------- | ------------------------------- |
| Gauche (Left)  | UG, DVG, FG, EELV, DVE          |
| Centre         | ENS, LREM, UDI, MoDem, DVC      |
| Droite (Right) | UDR, DVD, LR                    |
| Far right      | RN, UXD, REC                    |
| Divers / local | DIV, LDIV                       |
| Abstention     | derived from participation data |

> The political nuance codes (UG, DVG, RN, etc.) are the official coding system used by the Ministère de l'Intérieur in French electoral data. This schema groups them into 5 blocs + abstention for cleaner visual reading.

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
pip install pandas plotly jupyter
jupyter notebook notebooks/
```

## Output

Viz will be deployed at [shahfazal.com/elections-municipale-2026](https://shahfazal.com/elections-municipale-2026)
Réutilisation submitted on data.gouv.fr

---

_Project by [shahfazal](https://github.com/shahfazal)_
