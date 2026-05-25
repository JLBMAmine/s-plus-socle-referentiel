# ADR-0010 : Granularité fine du référentiel canonique S+

## Statut
Accepté — 25 mai 2026

## Contexte
La mission initiale du sous-projet « Construction du référentiel comptable canonique S+ » proposait une cible de 40 à 60 postes pour le référentiel, dans un objectif d'agrégation utilisateur. Le référentiel S+ doit servir de langage métier sur lequel les visualisations et KPIs financiers de l'application s'appuient.

Une analyse des sources disponibles (Caseware, IFRS-PME, IGRF, Stat Can 2006) a révélé que les référentiels professionnels existants sont nettement plus fins :
- Caseware (codes de liaison) : ~233 postes hiérarchisés
- IGRF (ARC) : 765 codes
- IFRS-PME (taxonomie XBRL) : ~250 concepts

Une granularité agrégée (40-60 postes) imposerait au modèle de données du référentiel des choix d'agrégation arbitraires en amont, alors que la sélection contextuelle des postes pertinents revient naturellement au consultant pendant le mandat, selon les KPIs et analyses mobilisés pour la PME concernée.

## Décision
Le référentiel canonique S+ adopte une **granularité fine de 150 à 200 postes**, cohérente avec les référentiels professionnels existants (notamment Caseware) et alignée sur la couverture de la taxonomie IFRS for SMEs.

L'agrégation pour l'affichage utilisateur sera traitée comme une **couche de présentation séparée** (groupements affichables, vues consolidées), pas comme une contrainte du modèle de données.

## Alternatives envisagées
- **Granularité agrégée (40-60 postes)** — rejetée car force des choix d'agrégation prématurés et perd la finesse nécessaire au calcul de certains KPIs (ex : ratio de liquidité immédiate qui distingue Encaisse / Placements court terme).
- **Deux niveaux (canonique fin + vue pilotage agrégée)** — rejetée pour cette phase car ajoute une complexité d'architecture (mappings entre niveaux) avant qu'on en démontre le besoin. Pourra être ajoutée plus tard si nécessaire.

## Conséquences

### Positives
- Couverture exhaustive permettant tous les KPIs prévus dans la bibliothèque S+
- Cohérence avec les pratiques cabinet (vocabulaire et finesse Caseware)
- Évolutivité : le référentiel peut servir plusieurs cas d'usage sans refonte

### Négatives
- Travail de construction plus volumineux (150-200 postes vs 40-60)
- L'interface utilisateur devra implémenter une couche d'agrégation pour ne pas submerger les consultants

### À surveiller
- Si certains postes s'avèrent inutilisés après plusieurs mandats, envisager une révision (marquage `optionnel` ou `déprécié`)