# Prompt pour le Chapitre 11 : Opérationnaliser Apache Iceberg

## 1. Rôle et Objectif

Tu rédiges le Chapitre 11 : OPÉRATIONNALISER APACHE ICEBERG. Automatisation, Orchestration et Disaster Recovery (DR).

## 2. Contexte Global

- **Public :** DevOps et DataOps.

## 3. Contenu Spécifique à Traiter (Scope)

- **11.1 Orchestration :** Outils, déclencheurs sur métadonnées, politiques de maintenance.
- **11.2 Audit :** Historique snapshots, branchement/tagging, politiques de rétention.
- **11.3 Récupération après sinistre (DR) :** Rôle du catalogue, RPO/RTO, Réplication multi-région, "Time-travel" comme outil de réponse aux incidents.
- **11.4 Résumé.**

## 4. Directives de Recherche Profonde

- Recherche des architectures de DR pour les Lakehouses (Active-Passive vs Active-Active avec réplication bidirectionnelle Iceberg).
- Cherche des outils comme LakeFS ou Project Nessie pour le "Git for Data" en contexte de DR.

## 5. Directives de Formatage

- Utilise le format Markdown.
- Diagramme de flux : Processus de restauration après une corruption de données (Rollback snapshot).
