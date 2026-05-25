# ADR-0012 : Découplage poste canonique vs libellés de présentation

## Statut
Accepté — 25 mai 2026

## Contexte
Le référentiel canonique S+ doit être manipulable par le code applicatif (loaders, calculateurs de KPIs, agents de mapping) tout en présentant aux utilisateurs (consultants, comptables) des libellés en français adaptés à leur pratique.

Plusieurs contraintes coexistent :
- Les libellés français peuvent évoluer (raffinement avec la norme officielle, retours terrain)
- Une extension multi-langue ultérieure est plausible (clients anglophones, dirigeants internationaux)
- Le code S+ doit pouvoir référencer un poste sans dépendre de son libellé d'affichage
- Les KPIs et calculs ne doivent pas casser si un libellé change

## Décision
Le modèle de données du référentiel S+ sépare deux niveaux distincts :

**Niveau canonique (langue-neutre, stable)**
- Identifiant interne S+ (ex. `SP_BIL_AC_001`)
- Référence au concept XBRL IFRS-PME (ex. `ifrs-smes:Cash`)
- Code IGRF de mapping fiscal (ex. `1001`)
- Type (actif courant, passif non courant, produit, etc.)
- Type de solde (débit/crédit)
- Hiérarchie et ordre d'affichage

**Niveau présentation (par langue, modifiable indépendamment)**
- Identifiant du poste S+ (référence vers le niveau canonique)
- Code langue (ex. `fr-CA`, `en`, etc.)
- Libellé court
- Libellé long
- Définition / texte d'aide

Le code applicatif référence **toujours l'identifiant canonique**, jamais le libellé. Les libellés sont injectés au moment de l'affichage selon la langue de l'utilisateur.

## Alternatives envisagées
- **Modèle plat avec libellés directement attachés au poste** — rejeté car couplage fort entre données et présentation, refactoring coûteux pour ajouter une langue ou raffiner un libellé
- **Libellés stockés dans un système d'i18n applicatif standard (ex. fichiers `.po`, `.json` i18next)** — option compatible avec la décision actuelle, à privilégier au moment de l'implémentation côté code S+ (décision technique à prendre dans le repo applicatif)

## Conséquences

### Positives
- Démo S+ possible immédiatement avec libellés Caseware FR sans investissement de traduction dédié
- Sprint « polish libellés FR » peut intervenir tardivement sans toucher au code (voir ADR-0014)
- Extension multi-langue future ne nécessite qu'un nouveau jeu de libellés
- Les changements de libellés sont des changements de données, pas de code

### Négatives
- Modèle de données légèrement plus complexe (deux tables ou deux fichiers au lieu d'un)
- Nécessite que le code S+ implémente proprement la couche d'injection des libellés

### À surveiller
- Lors de l'implémentation, vérifier qu'aucun libellé n'est codé en dur dans la couche applicative
- S'assurer que les changements de libellés n'invalident pas les références dans les configurations utilisateur (mandats, vues sauvegardées, etc.)