# Élections municipales 2026 : L’accès aux transports influence-t-il l’abstention ?

Analyse du open data croisant résultats électoraux et équipements de transport — Soumis au [défi data.gouv.fr](https://www.data.gouv.fr/posts/ouverture-du-challenge-open-data-resultats-des-elections-municipales).

**Date limite** : 13 avril 2026 · **Mot-clé** : `defi-municipales-2026-résultats`

## La question

L'accès aux transports en commun dans une commune influence-t-il le taux d'abstention aux élections municipales ?

On croise les résultats électoraux (Ministère de l'Intérieur) avec la densité d'équipements de transport de la BPE (INSEE), commune par commune, pour tester cette corrélation — et on ajoute la couleur politique pour affiner la lecture.

## Visualisations

1. **Carte choroplèthe** — communes colorées par taux d'abstention ou score transport. La carte raconte l'histoire géographique.
2. **Nuage de points** — score transport (x) vs taux d'abstention (y), un point par commune, coloré par nuance politique. Le graphique prouve la corrélation.

> **v1** — analyse initiale, soumise au challenge. D'autres visualisations sont prévues : profil urbain/rural, démographie vs abstention, score transport vs bloc gagnant.

## Schéma politique simplifié

| Groupe         | Nuances                             |
| -------------- | ----------------------------------- |
| Gauche         | UG, DVG, FG, EELV, DVE              |
| Centre         | ENS, LREM, UDI, MoDem, DVC          |
| Droite         | UDR, DVD, LR                        |
| Extrême droite | RN, UXD, REC                        |
| Divers / local | DIV, LDIV                           |
| Abstention     | dérivé des données de participation |

> Les codes de nuance politique (UG, DVG, RN, etc.) sont ceux du Ministère de l'Intérieur, utilisés dans les données officielles des élections. Ce schéma regroupe ces codes en 5 blocs + abstention pour faciliter la lecture visuelle.

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
pip install pandas plotly jupyter
jupyter notebook notebooks/
```

## Résultats

Viz sera déployée sur [shahfazal.com/elections-municipale-2026](https://shahfazal.com/elections-municipale-2026)
Réutilisation soumise sur data.gouv.fr

---

_Projet de [shahfazal](https://github.com/shahfazal)_
