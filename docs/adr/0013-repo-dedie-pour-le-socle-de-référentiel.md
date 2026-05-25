# ADR-0013 : Dépôt Git dédié pour le socle de référentiel

## Statut
Accepté — 25 mai 2026

## Contexte
Le sous-projet « Construction du référentiel canonique S+ » nécessite de rassembler de nombreuses sources externes volumineuses :
- Taxonomies IFRS XBRL (~50 Mo, plusieurs milliers de fichiers .xsd et .xml)
- IFRS Taxonomy Illustrated (PDF et Excel)
- Spécifications XBRL 2.1 et Dimensions
- Norme IFRS for SMEs 3e édition (PDF)
- Codes de liaison Caseware (Excel)
- Index IGRF de l'ARC (Excel, PDF, HTML)
- Documents de versioning et de référence

Volume total : ~65 Mo, ~4670 fichiers.

Ce contenu est :
- Statique (sources figées, pas de code applicatif)
- Référentiel partagé (utilisé par les humains et par Claude Code)
- Sensible aux licences (IFRS Foundation, XBRL International, ARC)

## Décision
Création d'un **dépôt Git dédié et public** nommé `s-plus-socle-referentiel`, séparé du dépôt applicatif S+ principal.

Caractéristiques :
- Dépôt **public** sur GitHub (`github.com/JLBMAmine/s-plus-socle-referentiel`)
- Fichiers `NOTICE.md` et `README.md` à la racine, documentant l'attribution et les conditions de licence de chaque source
- Structure par dossier : un dossier par grande source (`ifrs-smes-norme-2025/`, `ifrs-taxonomy-2024/`, `caseware/`, `igrf/`, etc.)
- Aucun code applicatif, aucune donnée client

Le dépôt applicatif S+ principal référence ce dépôt comme **source de vérité externe** pour le socle de référentiel, mais ne l'embarque pas comme submodule Git pour l'instant.

## Alternatives envisagées
- **Sous-dossier dans le repo S+ applicatif principal** — rejeté car alourdit le repo applicatif de 65 Mo de sources statiques sans valeur pour le développement courant du code
- **Repo privé** — rejeté car les sources contenues sont déjà publiques (IFRS, XBRL, ARC), aucun secret n'est exposé, et un repo public permet un accès direct par Claude Code et par toute personne du cabinet sans authentification
- **Submodule Git rattaché au repo S+ principal** — option ouverte pour plus tard si l'usage le justifie, mais non nécessaire actuellement

## Conséquences

### Positives
- Repo applicatif S+ reste léger et focalisé sur le code
- Repo socle référentiel peut évoluer à son propre rythme (mise à jour annuelle des taxonomies IFRS, etc.)
- Versioning Git permet de tracer les évolutions des sources externes
- Accessible publiquement par Claude Code, par toute personne du cabinet, par les futurs collaborateurs

### Négatives
- Deux repos à maintenir (mineur — le socle évoluera peu)
- Conformité de licence à respecter en permanence (fichier NOTICE.md à jour)

### À surveiller
- Si une source change de conditions de licence et exige un usage privé, basculer le repo en privé
- Si la nouvelle taxonomie IFRS-PME standalone est publiée (2026-2027), ajouter et versionner proprement
- Si le dépôt dépasse 1 Go (peu probable), envisager Git LFS pour les binaires
