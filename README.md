# Élections municipales 2026 : L’accès aux transports influence-t-il l’abstention ?

Analyse du open data croisant résultats électoraux et équipements de transport — Soumis au [défi data.gouv.fr](https://www.data.gouv.fr/posts/ouverture-du-challenge-open-data-resultats-des-elections-municipales).

**Date limite** : 13 avril 2026 · **Mot-clé** : `defi-municipales-2026-résultats`

## La question

Deux questions, mêmes données :

1. L'accès aux transports influence-t-il le **taux d'abstention** ?
2. L'accès aux transports influence-t-il le **bloc politique gagnant** ?

Chaque commune devient un point : axe x = score transport, axe y = taux d'abstention, couleur = bloc gagnant. L'axe y répond à la première question, la couleur à la seconde.

## Visualisations

1. **Carte choroplèthe** — communes colorées par taux d'abstention ou score transport. La carte raconte l'histoire géographique.
2. **Nuage de points** — score transport (x) vs taux d'abstention (y), un point par commune, coloré par bloc gagnant. Trois dimensions, un seul graphique : transport → abstention (axe y) et transport → couleur politique (couleur du point).

> **v1** — score transport vs taux d'abstention vs bloc politique gagnant, soumis au challenge.
> D'autres visualisations sont prévues : profil urbain/rural, démographie vs abstention.

## Schéma politique simplifié

| Bloc (`bloc`)  | Exemples de nuances                 |
| -------------- | ----------------------------------- |
| Extrême gauche | LEXG, LFI                           |
| Gauche         | LCOM, LSOC, LVEC, LUG, LDVG         |
| Centre         | LREN, LMDM, LHOR, LUC, LDVC, LUDI   |
| Droite         | LLR, LUD, LDVD, LDSV                |
| Extrême droite | LUDR, LRN, LREC, LUXD, LEXD         |
| Divers / local | LDIV, LECO, LREG                    |
| Abstention     | dérivé des données de participation |

> Les codes de nuance politique sont ceux du Ministère de l'Intérieur. La colonne `bloc` dans les données officielles regroupe déjà ces codes — ce schéma l'utilise directement, sans remapping manuel.

## Données

| Source                   | Description                                                   |
| ------------------------ | ------------------------------------------------------------- |
| Ministère de l'Intérieur | Résultats agrégés + candidats, élections municipales 2026     |
| INSEE — BPE              | Base permanente des équipements, codes transport              |
| INSEE — Population       | Répartition par tranche d'âge, commune (variable de contrôle) |

## Structure du dépôt

```
/notebooks/          — notebook d'analyse (self-contained)
/data/
    /raw/            — CSVs bruts (gitignorés)
    /processed/      — JSON propre pour la viz (versionné)
/viz/                — HTML statique + Plotly.js
```

## Lancer l'analyse

```bash
# with uv (recommandé)
uv sync
uv run jupyter notebook notebooks/

# ou pip
pip install pandas plotly jupyter pyarrow
jupyter notebook notebooks/
```

## Résultats

Viz sera déployée sur [shahfazal.com/elections-municipale-2026](https://shahfazal.com/elections-municipale-2026)

Réutilisation soumise sur data.gouv.fr

---

_Projet de [shahfazal](https://github.com/shahfazal)_
