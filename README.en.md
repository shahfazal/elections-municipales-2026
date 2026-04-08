# 2026 French Municipal Elections: Property Prices, Abstention & Political Blocs

Entry for the [data.gouv.fr open data challenge](https://www.data.gouv.fr/posts/ouverture-du-challenge-open-data-resultats-des-elections-municipales).
Deadline: **April 13, 2026** · Keyword: `defi-municipales-2026-résultats`

---

## The question

Do property prices correlate with abstention rate and which political bloc won?

Each commune becomes a dot: x = median price per m² (log scale), y = abstention rate, colour = winning bloc. The y-axis shows the price/abstention relationship; the colour shows which blocs dominate at different price levels.

## Visualisations

1. **Scatter plot**: median price per m² (x, log scale) vs abstention rate (y), one dot per commune, coloured by winning bloc. 838 communes with more than 9,000 inhabitants, 2nd round of 22 March 2026.
2. **Box plot**: distribution of prices per m² by winning political bloc. Do the most expensive communes vote differently?
3. **Paris–Lyon–Marseille choropleth**: arrondissement-level maps combining 2nd-round electoral results (fill colour) and median price per m² (circle size). DVF 2024 and 2025 data, with a year toggle in the viz.

## Political schema

| Bloc (`bloc`) | Example nuances                   |
| ------------- | --------------------------------- |
| EXG           | LEXG, LFI                         |
| GAU           | LCOM, LSOC, LVEC, LUG, LDVG       |
| CENT          | LREN, LMDM, LHOR, LUC, LDVC, LUDI |
| DTE           | LLR, LUD, LDVD, LDSV              |
| EXD           | LUDR, LRN, LREC, LUXD, LEXD       |
| DIV           | LDIV, LECO, LREG                  |

> The political nuance codes are the Ministère de l'Intérieur's official system. The `bloc` column in the source data already groups them: no manual remapping.

## Data sources

| Source                         | Description                                                                       |
| ------------------------------ | --------------------------------------------------------------------------------- |
| Ministère de l'Intérieur       | 2nd-round results, 2026 municipal elections (`commune.parquet`)                   |
| Ministère de l'Intérieur       | Bureau de Vote level results for Paris, Lyon, Marseille (`Paris_Lyon_BV.parquet`) |
| DVF 2024 + 2025 (data.gouv.fr) | Residential property transactions: one JSON per year, year toggle in viz          |

### Downloading the data

- **Electoral results**: [data.gouv.fr: Résultats des élections municipales 2026](https://www.data.gouv.fr/datasets/elections-municipales-2026-resultats-du-second-tour)
- **Property prices (DVF)**: [data.gouv.fr: Demandes de valeurs foncières](https://www.data.gouv.fr/fr/datasets/demandes-de-valeurs-foncieres/)
  Files used: `valeursfoncieres-2024.txt` and `valeursfoncieres-2025.txt`

## Repo structure

```
/notebooks/          - analysis notebooks (self-contained, outputs cleared)
/data/
    /raw/            - raw files (gitignored)
    /processed/      - clean JSON for viz (versioned, one file per year)
/viz/                - static HTML + JS + CSS
```

## Notebooks

- `01-data-exploration.ipynb`: electoral data exploration, builds the `df_clean` dataset
- `02-prix-logement.ipynb`: DVF pipeline, median price per m² per commune, JSON export (2024 and 2025)
- `03-transport-gtfs.ipynb`: GTFS exploration (stop density per commune, abandoned angle, not used in viz)
- `04-plm-data.ipynb`: DVF and electoral results aggregated by secteur for Paris, Lyon, Marseille

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

Viz deployed at [shahfazal.com/elections-municipales-2026](https://shahfazal.com/elections-municipales-2026)

Réutilisation submitted on data.gouv.fr

---

_Project by [shahfazal](https://github.com/shahfazal)_
