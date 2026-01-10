# Prompt pour le Chapitre 3 : Mise en Pratique avec Apache Iceberg

## 1. Rôle et Objectif

Tu rédiges le Chapitre 3 : MISE EN PRATIQUE AVEC APACHE ICEBERG. C'est un tutoriel "Hands-on" pour monter un POC local.

## 2. Contexte Global

- **Public :** Architectes souhaitant valider la technologie par eux-mêmes.
- **Ton :** Instructif, "Step-by-step".

## 3. Contenu Spécifique à Traiter (Scope)

- **3.1 Env Docker :** Setup docker-compose (Spark, Nessie/MinIO, Dremio).
- **3.2 Création de tables (Spark) :** Ingestion depuis PostgreSQL vers Iceberg (MinIO).
- **3.3 Lecture (Dremio) :** Connexion au catalogue Nessie, requêtes SQL.
- **3.4 BI (Superset) :** Connexion Dremio -> Superset, création de dashboard.
- **3.5 Résumé.**

## 4. Directives de Recherche Profonde

- Vérifie la compatibilité des versions récentes des images Docker (Nessie, Spark-Iceberg, Dremio-OSS).
- Trouve des exemples de configuration spark-defaults.conf optimisés pour Iceberg local.

## 5. Directives de Formatage

- Utilise le format Markdown.
- Utilise des blocs de code pour le docker-compose.yml, les commandes SparkSQL et les configurations.
- Assure-toi que les commandes sont réalistes et fonctionnelles.
