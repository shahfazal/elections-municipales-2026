# Élections municipales 2026 : Prix immobiliers, abstention et blocs politiques

Analyse open data — [challenge data.gouv.fr](https://www.data.gouv.fr/posts/ouverture-du-challenge-open-data-resultats-des-elections-municipales).

**Date limite** : 13 avril 2026 · **Mot-clé** : `defi-municipales-2026-résultats`

## La question

Les prix immobiliers influencent-ils le taux d'abstention et le bloc politique gagnant ?

Chaque commune devient un point : axe x = prix médian au m² (échelle log), axe y = taux d'abstention, couleur = bloc gagnant. L'axe y montre la relation prix/abstention, la couleur révèle quels blocs dominent selon le niveau de prix.

## Visualisations

1. **Nuage de points** — prix médian au m² (x, échelle log) vs taux d'abstention (y), un point par commune, coloré par bloc gagnant. 838 communes de plus de 9 000 habitants, 2ème tour du 22 mars 2026.
2. **Boîtes à moustaches** — distribution des prix au m² par bloc politique vainqueur. Les communes les plus chères votent-elles différemment ?
3. **Carte Paris–Lyon–Marseille** — cartes par arrondissement croisant résultats du 2ème tour (couleur de fond) et prix médian au m² (taille des cercles). Données DVF 2024 et 2025, avec bascule entre les deux années.

## Schéma politique

| Bloc (`bloc`) | Exemples de nuances               |
| ------------- | --------------------------------- |
| EXG           | LEXG, LFI                         |
| GAU           | LCOM, LSOC, LVEC, LUG, LDVG       |
| CENT          | LREN, LMDM, LHOR, LUC, LDVC, LUDI |
| DTE           | LLR, LUD, LDVD, LDSV              |
| EXD           | LUDR, LRN, LREC, LUXD, LEXD       |
| DIV           | LDIV, LECO, LREG                  |

> Les codes de nuance politique sont ceux du Ministère de l'Intérieur. La colonne `bloc` dans les données officielles regroupe déjà ces codes — pas de remapping manuel.

## Données

| Source                         | Description                                                                    |
| ------------------------------ | ------------------------------------------------------------------------------ |
| Ministère de l'Intérieur       | Résultats du 2ème tour 2026 (`commune.parquet`)                                |
| Ministère de l'Intérieur       | Résultats BV pour Paris, Lyon, Marseille (`Paris_Lyon_BV.parquet`)             |
| DVF 2024 + 2025 (data.gouv.fr) | Transactions résidentielles — un JSON par année, bascule dans la visualisation |

## Sources de données

Pour reproduire cette analyse, téléchargez les données suivantes :

### Résultats électoraux

- **Source** : Ministère de l'Intérieur
- **Élections** : Municipales 2026, 2ème tour (22 mars 2026)
- **Lien** : [data.gouv.fr — Résultats des élections municipales 2026](https://www.data.gouv.fr/datasets/elections-municipales-2026-resultats-du-second-tour)

### Prix immobiliers (DVF)

- **Source** : Direction générale des Finances publiques (DGFiP)
- **Période** : 2024 et 2025
- **Lien** : [data.gouv.fr — Demandes de valeurs foncières (DVF)](https://www.data.gouv.fr/fr/datasets/demandes-de-valeurs-foncieres/)
- **Fichiers utilisés** : `valeursfoncieres-2024.txt` et `valeursfoncieres-2025.txt`

## Structure du dépôt

```
/notebooks/          — notebooks d'analyse (self-contained, sorties vidées)
/data/
    /raw/            — fichiers bruts (gitignorés)
    /processed/      — JSON propres pour la viz (versionnés, un par année)
/viz/                — HTML + JS + CSS
```

## Lancer l'analyse

```bash
# avec uv (recommandé)
uv sync
uv run jupyter notebook notebooks/

# ou pip
pip install pandas plotly jupyter pyarrow
jupyter notebook notebooks/
```

## Résultats

Viz déployée sur [shahfazal.com/elections-municipales-2026](https://shahfazal.com/elections-municipales-2026)

Réutilisation soumise sur data.gouv.fr

---

_Projet de [shahfazal](https://github.com/shahfazal)_
