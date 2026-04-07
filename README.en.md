# 2026 French Municipal Elections — Property Prices, Abstention & Political Blocs

Entry for the [data.gouv.fr open data challenge](https://www.data.gouv.fr/posts/ouverture-du-challenge-open-data-resultats-des-elections-municipales).
Deadline: **April 13, 2026** · Keyword: `defi-municipales-2026-résultats`

---

## The question

Do property prices correlate with abstention rate and which political bloc won?

Each commune becomes a dot: x = median price per m² (log scale), y = abstention rate, colour = winning bloc. The y-axis shows the price/abstention relationship; the colour shows which blocs dominate at different price levels.

## Visualisations

1. **Scatter plot** — median price per m² (x, log scale) vs abstention rate (y), one dot per commune, coloured by winning bloc. 838 communes with more than 9,000 inhabitants, 2nd round of 22 March 2026.
2. **Box plot** — distribution of prices per m² by winning political bloc. Do the most expensive communes vote differently?
3. **Paris–Lyon–Marseille choropleth** — arrondissement-level maps combining 2nd-round electoral results (fill colour) and median price per m² (circle size). DVF 2024 transactions.

## Political schema

| Bloc (`bloc`)  | Example nuances                   |
| -------------- | --------------------------------- |
| EXG            | LEXG, LFI                         |
| GAU            | LCOM, LSOC, LVEC, LUG, LDVG       |
| CENT           | LREN, LMDM, LHOR, LUC, LDVC, LUDI |
| DTE            | LLR, LUD, LDVD, LDSV              |
| EXD            | LUDR, LRN, LREC, LUXD, LEXD       |
| DIV            | LDIV, LECO, LREG                  |

> The political nuance codes are the Ministère de l'Intérieur's official system. The `bloc` column in the source data already groups them — no manual remapping.

## Data sources

| Source                   | Description                                                         |
| ------------------------ | ------------------------------------------------------------------- |
| Ministère de l'Intérieur | 2nd-round results, 2026 municipal elections (`commune.parquet`)     |
| Ministère de l'Intérieur | BV-level results for Paris, Lyon, Marseille (`Paris_Lyon_BV.parquet`) |
| DVF 2024 (data.gouv.fr)  | Residential property transactions — median prix/m² per commune     |

## Repo structure

```
/notebooks/          — analysis notebooks (self-contained, outputs cleared)
/data/
    /raw/            — raw files (gitignored)
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

Viz deployed at [shahfazal.com/elections-municipales-2026](https://shahfazal.com/elections-municipales-2026)

Réutilisation submitted on data.gouv.fr

---

_Project by [shahfazal](https://github.com/shahfazal)_
