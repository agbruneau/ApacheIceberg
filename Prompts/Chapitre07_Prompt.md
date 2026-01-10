# Prompt pour le Chapitre 7 : Implémentation de la Couche de Catalogue

## 1. Rôle et Objectif

Tu rédiges le Chapitre 7 : IMPLÉMENTATION DE LA COUCHE DE CATALOGUE. Focus sur le rôle central du catalogue et la spec REST.

## 2. Contexte Global

- **Contexte technologique :** Importance du standard "Iceberg REST Catalog".

## 3. Contenu Spécifique à Traiter (Scope)

- **7.1 Rôle :** Responsabilités, interactions moteurs.
- **7.2 Exigences :** Performance, Gouvernance, Sécurité, Fédération.
- **7.3 Spec REST Catalog :** Standardisation, interopérabilité (avant/après).
- **7.4 Options (Comparatif) :** Hadoop, Hive, JDBC, Polaris (Apache), Nessie, Gravitino, AWS Glue, Dremio, Snowflake Open Catalog, Databricks Unity.
- **7.5 Scénarios de choix :** 8 scénarios détaillés (Migration Hive, Startup, Entr. Finance, SaaS, Multi-cloud, etc.).
- **7.6 Résumé.**

## 4. Directives de Recherche Profonde

- Analyse les différences entre Project Nessie et Apache Polaris (architecture, git-like semantics vs RBAC).
- Vérifie le support de la spécification REST par les grands vendeurs (Snowflake, Databricks, AWS) en 2024-2025.

## 5. Directives de Formatage

- Utilise le format Markdown.
- Tableau comparatif des catalogues (Support REST, Git-semantics, Licence, Hébergé/Self-managed).
- Diagramme de séquence illustrant l'interaction Client -> REST Catalog -> Stockage S3.
