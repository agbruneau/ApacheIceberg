# Prompt pour le Chapitre 6 : Architecture de la Couche d'Ingestion

## 1. Rôle et Objectif

Tu rédiges le Chapitre 6 : ARCHITECTURE DE LA COUCHE D'INGESTION. C'est un chapitre critique axé sur Kafka et le streaming.

## 2. Contexte Global

- **Contexte technologique :** Focus MAJEUR sur Kafka, Confluent, Flink.
- **Public :** Architectes confrontés à de forts volumes de données.

## 3. Contenu Spécifique à Traiter (Scope)

- **6.1 Exigences :** Débit, latence, Exactly-once.
- **6.2 Modèles :** Batch, Micro-batch, Streaming.
- **6.3 Écritures Iceberg :** Sémantique, Commit protocols, gestion des conflits.
- **6.4 Patterns Kafka -> Iceberg (CŒUR DU CHAPITRE) :**
  - Pattern 1 : Confluent Tableflow (Zero-ETL).
  - Pattern 2 : Flink SQL (ETL temps réel, CDC, masquage PII).
  - Pattern 3 : Kafka Connect Iceberg Sink (Topic de contrôle, coordination).
- **6.5 Schema Registry :** Synchro des évolutions, Avro/Protobuf.
- **6.6 Outils :** Spark, Flink, NiFi, Fivetran, etc.
- **6.7 Application des exigences.**
- **6.8 Résumé.**

## 4. Directives de Recherche Profonde

- Cherche les détails techniques de "Confluent Tableflow" et ses limitations actuelles.
- Trouve des configurations types pour le "Kafka Connect Iceberg Sink" (paramètres de commit, flush size).
- Recherche des benchmarks Flink vs Spark Streaming pour l'écriture Iceberg.

## 5. Directives de Formatage

- Utilise le format Markdown.
- **Diagrammes Mermaid obligatoires :** Un pour chaque Pattern Kafka (Tableflow, Flink, Connect).
- Snippets de code : Configuration Flink SQL pour une table Iceberg, Configuration Kafka Connect JSON.
