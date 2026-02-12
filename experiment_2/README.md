# Quantification de l'impact des verrous inutiles

Ce dossier contient les résultats de l'Expérience 2, visant à quantifier l'impact de performance des verrous inutiles.

## Structure du dossier

- `images/` : Graphiques générés à partir des tests CloudLab.
- `runner.py` : Script d'exécution automatisée des benchmarks.
- `analyze.py` : Script de génération des graphiques.
- `results.csv` : Données brutes de l'expérience.

## Comment exécuter

1. Installer les dépendances : `pip install pandas matplotlib`
2. Lancer les mesures : `python runner.py`
3. Générer les plots : `python analyze.py`
