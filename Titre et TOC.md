# Architecting an Apache Iceberg Lakehouse

**Contexte d'exploitation : Confluent Cloud Kafka**

---

## **PARTIE 1 : FONDATIONS & INTERNALS**

### **Chapitre 1 : Le concept de Streaming Lakehouse**

**Adaptations Confluent Cloud:**

- Introduction au concept de lakehouse streaming avec Kafka
- Architecture data streaming vs. architecture batch traditionnelle
- Positionnement d'Apache Iceberg comme destination analytique pour Kafka
- **Cas d'usage**: Unified streaming lakehouse avec Confluent Cloud
- Avantages de l'intégration Kafka-Iceberg pour analytics temps réel[^1][^2]

### **Chapitre 2 : Anatomie Technique d'Apache Iceberg**

**Focus Architecte [NOUVEAU]:**

- **Structure des fichiers** : Metadata (`.json`), Manifest Lists (`.avro`), Manifests (`.avro`), Data Files (`.parquet`).
- **Le cycle de vie d'un commit** : Isolation ACID et _Optimistic Concurrency_.
- **Row-Level Ops** : Copy-on-Write (CoW) vs Merge-on-Read (MoR) - Trade-offs pour le streaming[^3].
- **Le rôle critique du Catalogue** : Mécanisme de verrouillage et gestion de l'état.

---

## **PARTIE 2 : DESIGN & STRATÉGIE**

### **Chapitre 3 : Modélisation de Données pour le Lakehouse**

**Focus Design:**

- Audit des topics Kafka existants et mapping de schémas (Avro/Protobuf vers Iceberg).
- **Stratégies de Partitionnement** : Identity, Transform, et le pouvoir du _Hidden Partitioning_[^4].
- **Gestion de la cardinalité** : Prévention de l'explosion des partitions (ex: `bucket(user_id)`).
- Évolution de Schéma vs Évolution de Partition (Support Tableflow vs Natif).
- Planification de la transition : Streaming vs Batch.

### **Chapitre 4 : Architecture de Stockage & Catalogues**

**Focus Infrastructure:**

- **Stockage** : Amazon S3 (Tiered Storage) vs Confluent Managed Storage.
  - Considérations de coûts et performance.
- **Comparatif Catalogues** :
  - AWS Glue (Intégration native Tableflow).
  - Iceberg REST (Confluent Built-in).
  - Snowflake Open Catalog.
  - Project Nessie (Git-like semantics pour DataOps).
- Impact du choix du catalogue sur la portabilité et le verrouillage architectural.

---

## **PARTIE 3 : PATTERNS D'INGESTION**

### **Chapitre 5 : Ingestion via Confluent Tableflow**

**Focus Simplicité & Limitations:**

- Configuration "Zero-code" : Topic → Iceberg (Hands-on).
- Évolution automatique de schéma avec Schema Registry.
- Maintenance automatique gérée par Confluent (Compaction, Optimisation).
- Limitations à connaître : Latence de propagation, support des suppressions, coûts.

### **Chapitre 6 : Ingestion Avancée via Flink SQL**

**Focus Transformations Complexes & CDC:**

- Pattern : Kafka → Flink SQL (Deduplication/Enrichissement) → Iceberg.
- **Gestion des Upserts et Deletes** en streaming (CDC).
- Utilisation de Flink pour des jointures _stream-stream_ avant persistance.
- **Alternative Self-Managed** : Kafka Connect Iceberg Sink.
  - Contrôle granulaire des commits et multi-table fan-out.

---

## **PARTIE 4 : OPÉRATIONS & OPTIMISATIONS**

### **Chapitre 7 : Maintenance et Performance**

**Techniques Avancées:**

- **Problème des "Small Files"** : Impact en streaming et stratégies de compaction (Bin-packing).
- **Optimisation des Lectures** :
  - Techniques de layout : `SORT`, `Z-ORDER` (Clustering multidimensionnel).
  - Filtres probabilistes : Bloom Filters pour le pruning efficace.
- Maintenance Hygiène : Expiration des snapshots (retention policy) et suppression des fichiers orphelins.

### **Chapitre 8 : Gouvernance et Consommation**

**Vision Unifiée:**

**A. Gouvernance et Sécurité**

- Intégration Schema Registry pour la gouvernance des données.
- Lineage de bout en bout et Audit trails.
- Gestion GDPR : "Right to be forgotten" via Iceberg Deletes.
- Sécurité : IAM, RBAC au niveau Catalogue.

**B. Couche de Consommation & Fédération**

- **Outils BI** : Snowflake, Amazon Athena, Power BI.
- **Moteurs de Fédération** : Trino, Dremio, Starburst (Requêtes sur données chaudes).
- **Notebooks** : Jupyter, Spark pour l'exploration data science.
- Architecture hybride : Requêtes sur données Kafka (Temps réel) + Iceberg (Historique).

### **Chapitre 9 : Synergie Confluent Cloud, Apache Iceberg et Microsoft Fabric**

**Adaptations Confluent Cloud & Microsoft Fabric:**

- **Architecture de l'intégration Tripartite**

  - Pipeline unifié : Confluent Cloud (Streams) → Iceberg (Storage) → Microsoft Fabric (Analytics)
  - Rôle des **Shortcuts OneLake** pour la virtualisation sans copie des tables Iceberg
  - Configuration du stockage ADLS Gen2 comme destination pour Confluent Tableflow

- **Mise en œuvre technique**

  - Provisioning des topics Kafka et schémas dans Confluent Cloud
  - Configuration de Tableflow pour matérialiser en Iceberg sur ADLS Gen2
  - Création de Shortcuts dans un Lakehouse Fabric pointant vers les buckets Iceberg
  - Compatibilité des métadonnées et gestion du catalogue

- **Exploitation Analytique dans Fabric**

  - **Power BI Direct Lake** : Visualisation haute performance directe sur Iceberg
  - **T-SQL & Spark** : Interrogation transparente des données streaming via les moteurs Fabric
  - Enrichissement : Croisement des données chaudes (Iceberg) avec le data warehouse d'entreprise (OneLake)

- **Gouvernance et Sécurité étendu**
  - Sécurité Entra ID (Azure AD) unifiée sur la couche de stockage
  - Lineage de bout en bout : du Producer Kafka au Dashboard Power BI
  - Gestion du cycle de vie des données et conformité (Purview + Stream Governance)

---

## **ANNEXES ADAPTÉES CONFLUENT CLOUD**

### **Annexe A : Les tables de métadonnées Iceberg dans un contexte streaming**

- Structure métadonnées pour tables haute vélocité
- Snapshots et commits fréquents
- Impact du streaming sur la croissance des métadonnées
- Best practices: Rétention snapshots pour données streaming

### **Annexe B : Scripts et outils pour Confluent + Iceberg**

- **Python**: Scripting pour configuration Tableflow
- **Confluent CLI**: Automation déploiement pipelines
- **SQL**: Exemples Flink SQL pour transformations streaming[^6][^19]
- **Kafka Connect REST API**: Configuration programmatique Iceberg Sink[^23]

### **Annexe C : Spécifications et intégrations**

- **Spécification Apache Iceberg** pour streaming use cases
- **Confluent Tableflow API**: Documentation intégration
- **Schema Registry**: Format Avro, JSON Schema, Protobuf
- **Iceberg REST Catalog Specification**: Intégration avec Confluent
- **AWS Glue Data Catalog**: Configuration pour Tableflow[^7][^4]

---

## **RESSOURCES COMPLÉMENTAIRES CONFLUENT**

### **Guides de démarrage rapide**

- Quickstart: Kafka → Iceberg → Snowflake avec Tableflow[^3][^4]
- Streaming ETL avec Flink SQL et Tableflow[^6]
- Data exploration avec Tableflow, Iceberg et Trino[^16]

### **Patterns d'architecture recommandés**

1. **Zero-ETL analytics**: Kafka topics → Tableflow (zero code)[^24][^8]
2. **Streaming ETL**: Kafka → Flink SQL → Tableflow → Iceberg[^6]
3. **Hybrid real-time/historical**: Données fraîches (Kafka) + historique (Iceberg)[^18]
4. **Multi-cloud**: Confluent Cloud + S3 + Multiple analytics engines[^7]

### **Considérations de coûts**

- **Tableflow**: Coût par GB ingéré + stockage S3[^8]
- **Alternative**: Kafka Connect self-managed (infrastructure + maintenance)
- **Optimisations**: Compaction, partitionnement, rétention Kafka court terme

### **Cas d'usage clients**

- Real-time fraud detection avec Kafka + Iceberg analytics[^8]
- IoT telemetry: Streaming ingestion → Long-term analytics[^25][^20]
- Financial services: Compliance et audit avec Iceberg time-travel[^26][^27]

---

## **POINTS CLÉS POUR CONFLUENT CLOUD**

### **Avantages Tableflow vs. alternatives**

✅ **Zéro code**: Configuration en quelques clics
✅ **Fully-managed**: Maintenance automatique (compaction, optimization)
✅ **Schema evolution**: Automatique via Schema Registry
✅ **Performance**: Optimisé pour Confluent Cloud
✅ **Intégrations**: AWS Glue, Snowflake, Databricks

### **Quand utiliser Kafka Connect Iceberg Sink**

- Besoin de contrôle granulaire sur commit strategy
- Infrastructure self-managed existante
- Transformations custom dans connector
- Multi-table fan-out complexe

### **Quand utiliser Flink SQL + Tableflow**

- Transformations streaming complexes nécessaires
- Enrichissement données avant Iceberg
- Jointures streaming multiples sources
- Agrégations temps réel

---

**Cette table des matières adaptée fournit une roadmap complète pour architecturer un lakehouse Apache Iceberg avec Confluent Cloud Kafka, couvrant tous les aspects de l'ingestion streaming temps réel jusqu'à l'analytics à grande échelle.**
<span style="display:none">[^28][^29][^30][^31][^32][^33][^34][^35][^36][^37][^38][^39][^40][^41][^42][^43][^44][^45][^46][^47][^48][^49][^50][^51][^52][^53][^54][^55][^56][^57][^58][^59][^60][^61]</span>

<div align="center">⁂</div>

[^1]: https://blog.twingdata.com/p/apache-iceberg-in-modern-data-architectures
[^2]: https://www.kai-waehner.de/blog/2025/11/19/data-streaming-meets-lakehouse-apache-iceberg-for-unified-real-time-and-batch-analytics/
[^3]: https://www.snowflake.com/en/developers/guides/snowflake-confluent-tableflow-iceberg/
[^4]: https://quickstarts.snowflake.com/guide/snowflake-confluent-tableflow-iceberg/index.html?index=..%2F..index
[^5]: https://rmoff.net/2025/08/18/kafka-to-iceberg-exploring-the-options/
[^6]: https://www.confluent.io/blog/streaming-etl-flink-tableflow/
[^7]: https://www.confluent.io/product/tableflow/
[^8]: https://www.confluent.io/blog/tableflow-ga-kafka-snowflake-iceberg/
[^9]: https://www.decodable.co/blog/kafka-to-iceberg-with-flink
[^10]: https://estuary.dev/blog/kafka-to-apache-iceberg/
[^11]: https://iceberg.apache.org/docs/nightly/kafka-connect/
[^12]: https://www.tinybird.co/blog/optimizing-apache-iceberg-tables-for-real-time-analytics
[^13]: https://iceberg.apache.org/docs/1.7.2/kafka-connect/
[^14]: https://www.dremio.com/blog/using-dremio-with-confluents-tableflow-for-real-time-apache-iceberg-analytics/
[^15]: https://www.confluent.io/blog/integrating-confluent-tableflow-trino-apache-iceberg-jupyter/
[^16]: https://www.confluent.io/blog/building-streaming-data-pipelines-part-1/
[^17]: https://www.starburst.io/blog/tableflow-confluent-starburst/
[^18]: https://blog.streambased.io/p/making-iceberg-real-time
[^19]: https://docs.confluent.io/cloud/current/flink/reference/sql-examples.html
[^20]: https://link.springer.com/10.1007/s10796-023-10409-2
[^21]: https://www.instaclustr.com/blog/streaming-data-apache-kafkaconnect-iceberg-sink-connector-part1/
[^22]: https://www.confluent.io/blog/build-real-time-kafka-dashboards/
[^23]: https://www.youtube.com/watch?v=5ywgsh2Wzm4
[^24]: https://www.youtube.com/watch?v=O2l5SB-camQ
[^25]: https://www.nationaleducationservices.org/a-unified-bigdata-pipeline-for-cloud-and-network-telemetry-design-implementation-and-benchmarking-with-hadoop-and-apache-spark/pid-2232669502
[^26]: https://al-kindipublisher.com/index.php/jcsts/article/view/9727
[^27]: https://www.academicpublishers.org/journals/index.php/ijdsml/article/view/4304/5286
[^28]: https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/images/835935/046bb9e8-0c5c-4513-9b84-d2a24b325977/image.jpg
[^29]: https://peerj.com/articles/cs-2899
[^30]: https://ieeexplore.ieee.org/document/10724413/
[^31]: https://dl.acm.org/doi/10.14778/3611540.3611567
[^32]: https://wjarr.com/node/15962
[^33]: https://lorojournals.com/index.php/emsj/article/view/1454
[^34]: https://journalwjarr.com/node/1103
[^35]: https://linkinghub.elsevier.com/retrieve/pii/S0167739X21002995
[^36]: https://arxiv.org/pdf/2205.09415.pdf
[^37]: http://arxiv.org/pdf/2410.15533.pdf
[^38]: https://arxiv.org/pdf/2504.02364.pdf
[^39]: https://www.mdpi.com/1424-8220/19/1/134/pdf
[^40]: https://arxiv.org/pdf/2401.17747.pdf
[^41]: https://www.epj-conferences.org/articles/epjconf/pdf/2024/05/epjconf_chep2024_01032.pdf
[^42]: https://arxiv.org/abs/2309.04918
[^43]: https://rmoff.net/2025/07/04/writing-to-apache-iceberg-on-s3-using-kafka-connect-with-glue-catalog/
[^44]: https://www.youtube.com/watch?v=uIrM3vXKRrk
[^45]: https://docs.confluent.io/platform/current/connect/kafka_connectors.html
[^46]: https://github.com/apache/iceberg/issues/10745
[^47]: https://docs.streamnative.io/connect/connectors/kafka-connect-iceberg/current/kafka-connect-iceberg-sink
[^48]: https://blog.dataengineerthings.org/stream-kafka-topic-to-the-iceberg-tables-with-zero-etl-7ccf0e586ebc
[^49]: https://www.youtube.com/watch?v=Zatav2MBoSc
[^50]: https://github.com/databricks/iceberg-kafka-connect
[^51]: https://www.onlinescientificresearch.com/articles/universal-data-engineering-frameworks-for-crossplatform-fraud-detection.pdf
[^52]: https://linkinghub.elsevier.com/retrieve/pii/S138376212100151X
[^53]: https://arxiv.org/pdf/1712.04344.pdf
[^54]: http://arxiv.org/pdf/1901.09062.pdf
[^55]: https://arxiv.org/pdf/2006.04105.pdf
[^56]: https://www.automq.com/blog/kafka-to-iceberg-top-9-ways-2026
[^57]: https://www.getorchestra.io/guides/confluent-tableflow-kafka-streaming-iceberg
[^58]: https://iceberg.apache.org/docs/latest/flink-queries/
[^59]: https://www.youtube.com/watch?v=k6mn2Sb1Uh4
[^60]: https://iceberg.apache.org/docs/nightly/flink/
[^61]: https://jack-vanlightly.com/blog/2024/3/19/tableflow-the-stream-table-kafka-iceberg-duality
