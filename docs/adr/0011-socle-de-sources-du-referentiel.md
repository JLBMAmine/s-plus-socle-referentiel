# ADR-0011 : Socle de sources du référentiel canonique S+

## Statut
Accepté — 25 mai 2026

## Contexte
Le référentiel canonique S+ doit s'appuyer sur des sources externes pour bénéficier d'une légitimité normative, d'une couverture exhaustive et d'une compatibilité avec les outils en place dans les cabinets PME québécois.

L'investigation des sources disponibles a couvert :
- **Taxonomie XBRL IFRS-PME 2024** — référentiel normatif international, machine-readable, structuré, couvre les trois états financiers
- **Caseware (codes de liaison)** — référentiel terrain utilisé par les cabinets PME québécois, libellés en français déjà adaptés
- **IGRF (ARC)** — index général de l'Agence du revenu du Canada, normatif fiscal pour la déclaration T2, ~765 codes
- **Norme IFRS for SMEs (3e édition 2025)** — texte normatif lisible par humain et par agent
- **Stat Can 2006** — plan comptable statistique, écarté car non orienté pilotage
- **Plan comptable XBRL canadien NCECF** — n'existe pas (vérifié auprès de XBRL Canada et CNC)
- **Taxonomie XBRL IFRS pour PME française** — n'existe pas (confirmé par l'IFRS Foundation)

Trois rôles distincts sont identifiés pour les sources :
1. Source normative principale qui structure le référentiel
2. Source de validation terrain pour s'assurer de la pertinence PME québécoises
3. Source de mapping fiscal pour le pont avec la T2

## Décision
Le référentiel canonique S+ s'appuie sur **trois sources complémentaires** avec des rôles distincts :

1. **IFRS for SMEs (taxonomie XBRL 2024 + norme 3e édition 2025)** — socle normatif principal
   - Fournit la structure (concepts, hiérarchie, type de solde, période)
   - Fournit les identifiants stables machine-readable
   - Fournit la définition normative de chaque concept

2. **Caseware (codes de liaison)** — référence terrain et validation
   - Valide la pertinence PME québécoises de chaque concept retenu
   - Fournit les libellés français provisoires (voir ADR-0014)
   - Fournit la granularité d'usage cabinet éprouvée

3. **IGRF (ARC)** — mapping fiscal annexe
   - Chaque poste S+ peut référencer un ou plusieurs codes IGRF
   - Permet aux consultants et à l'agent S+ de mapping de faire le pont avec la T2
   - Le guide RC4088 sert de référence de définitions pour l'agent de mapping intelligent

## Alternatives envisagées
- **Taxonomie XBRL canadienne NCECF** — n'existe pas, écartée
- **Taxonomie IFRS complète (pas IFRS-PME)** — surdimensionnée (~5000 concepts), vocabulaire grandes entreprises
- **Caseware comme socle normatif principal** — rejetée car référentiel propriétaire non normatif, et l'objectif S+ vise une portée plus large que les pratiques d'un cabinet
- **Stat Can 2006** — écartée car trop sectorielle et trop fine, orientée statistiques pas pilotage

## Conséquences

### Positives
- Référentiel normatif (IFRS-PME) + adapté terrain (Caseware) + connecté fiscalement (IGRF)
- Vocabulaire français immédiatement disponible via Caseware
- Pérennité : la norme IFRS-PME 2025 est en vigueur jusqu'à révision majeure attendue post-2030
- Traçabilité : chaque poste S+ est attribuable à un concept IFRS-PME normatif et à un code IGRF fiscal

### Négatives
- Triple sourcing demande un travail de mapping initial soigneux
- La norme IFRS-PME n'existe pas en français officiel (voir ADR-0014)
- Dépendance à la disponibilité publique des sources IFRS et IGRF

### À surveiller
- Publication attendue de la nouvelle taxonomie IFRS-PME XBRL standalone alignée 3e édition (2026-2027) — prévoir une migration
- Évolutions futures de l'IGRF (mises à jour annuelles de l'ARC)
- Évolutions des codes Caseware