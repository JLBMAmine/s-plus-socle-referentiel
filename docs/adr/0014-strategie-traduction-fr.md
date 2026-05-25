# ADR-0014 : Stratégie de traductions françaises du référentiel S+

## Statut
Accepté — 25 mai 2026

## Contexte
L'utilisateur final du référentiel S+ est un consultant ou comptable québécois travaillant en français. Les libellés des postes doivent donc être disponibles en français de qualité professionnelle, alignés sur la pratique terrain et idéalement traçables à une source normative.

Investigation des sources françaises disponibles :
- **Taxonomie XBRL IFRS-PME en français** — n'existe pas (confirmé par l'IFRS Foundation : seules les versions japonaise, coréenne, espagnole et ukrainienne sont publiées)
- **Norme IFRS for SMEs 3e édition 2025 en français** — non publiée à ce jour, statut futur incertain
- **Norme IFRS for SMEs édition 2009 en français** — publiée par l'IASB en novembre 2010, accessible via compte IFRS Foundation, datée mais utile pour la terminologie de référence
- **Caseware (codes de liaison)** — libellés français québécois déjà adaptés au terrain
- **États financiers modèle CPA Québec NCCF** — vocabulaire NCCF québécois professionnel
- **Référentiel CPA Québec NCCF** — vocabulaire NCCF québécois professionnel

## Décision
Stratégie de traduction française **progressive en deux temps**, alignée sur le découplage défini en ADR-0012 :

**Temps 1 — Démarrage (construction initiale du référentiel)**
- Libellés français provisoires extraits directement de **Caseware** pour les postes qui y figurent
- Pour les postes IFRS-PME absents de Caseware, traduction de travail rédigée pendant la construction itérative, validée avec le porteur du projet
- Aucun investissement de traduction massif a priori
- La démo S+ peut tourner en français dès le jour 1

**Temps 2 — Sprint « Polish libellés FR » (après démo fonctionnelle)**
- Revue systématique des libellés provisoires contre la norme IFRS for SMEs 2009 FR (si récupérée) et contre les sources NCCF québécoises (États financiers modèle, Référentiel CPA Québec)
- Validation par un comptable professionnel du cabinet
- Estimation : 3 à 5 jours-personne pour ~150-200 postes
- Production finale d'un jeu de libellés stable pour mise en production

Aucun mapping FR exhaustif a priori de la taxonomie IFRS-PME complète (~250 concepts) ne sera produit — seuls les postes retenus dans le référentiel S+ sont traduits.

## Alternatives envisagées
- **Traduction automatique massive de la taxonomie IFRS-PME EN, puis validation humaine** — rejetée car risque de terminologie hors-pratique québécoise, et travail à perte sur les concepts non retenus dans S+
- **Production d'un fichier de mapping FR complet en amont avant la construction du référentiel** — rejetée car investissement de traduction sur des concepts qui pourraient ne pas être retenus
- **Attente d'une éventuelle traduction officielle FR de la 3e édition par l'IFRS Foundation** — rejetée car calendrier incertain (probablement plusieurs années), bloque le projet S+

## Conséquences

### Positives
- Démarrage rapide sans dépendance à une traduction préalable
- Investissement de traduction limité aux postes effectivement utilisés
- Libellés finaux alignés sur la pratique terrain (Caseware) ET sur la norme NCCF (États financiers modèle CPA Québec)
- Architecture découplée (ADR-0012) permet le raffinement sans toucher au code

### Négatives
- Libellés provisoires pendant la phase de développement
- Sprint « polish » à planifier explicitement avant mise en production
- Pas de mapping FR officiel IFRS-PME, donc traçabilité normative limitée pour le français

### À surveiller
- Si l'IFRS Foundation publie une traduction FR officielle de la 3e édition, l'intégrer comme source de référence
- Si une étude révèle des écarts terminologiques significatifs entre Caseware FR et NCCF québécois, arbitrer au cas par cas
- Si une extension multi-langue (anglais) devient prioritaire, le découplage ADR-0012 permet d'ajouter EN sans toucher au code