# **Chapitre 1 : LE MONDE DU LAKEHOUSE APACHE ICEBERG**

## **1.1 L'Architecture de Données en Mutation : Une Dialectique Historique**

L'évolution de l'architecture des données au cours des trois dernières décennies ne doit pas être perçue comme une simple succession linéaire de technologies, mais plutôt comme une dialectique complexe entre deux impératifs contradictoires : la nécessité d'une structure rigoureuse pour garantir la fiabilité, et le besoin vital d'agilité pour gérer l'échelle et la variété. Pour l'architecte informatique senior opérant aujourd'hui dans l'écosystème canadien, comprendre l'émergence du paradigme Lakehouse et d'Apache Iceberg exige d'abord une déconstruction minutieuse des époques qui l'ont précédé. C'est en analysant les échecs et les succès du Data Warehouse monolithique et du Data Lake chaotique que nous pouvons saisir la véritable proposition de valeur du Lakehouse.

### **1.1.1 L'Ère du Data Warehouse (1980-2010) : La Cathédrale de la Vérité Unique**

Durant près de trente ans, le Data Warehouse (EDW \- Enterprise Data Warehouse) a représenté l'apogée de l'architecture décisionnelle. Ancré dans les méthodologies formalisées par des figures tutélaires comme Bill Inmon et Ralph Kimball 1, le Warehouse était conçu pour être la "source unique de vérité" de l'entreprise. Dans ce modèle, la donnée n'était pas simplement stockée ; elle était sculptée.

Le paradigme dominant de cette ère était le **Schema-on-Write** (schéma à l'écriture). Avant qu'une seule ligne de données ne soit ingérée dans le système, elle devait subir un processus rigoureux de modélisation, de nettoyage et de transformation pour se conformer à un schéma relationnel prédéfini, souvent en troisième forme normale (3NF) ou en schéma en étoile dimensionnel.2 Cette contrainte garantissait une intégrité référentielle absolue et une qualité de données irréprochable, permettant aux décideurs de s'appuyer sur des rapports BI (Business Intelligence) d'une précision chirurgicale.

Cependant, cette architecture monolithique portait en elle les germes de sa propre obsolescence face à la montée du Big Data.  
Premièrement, le couplage fort entre le stockage et le calcul (Compute-Storage Coupling) imposait des contraintes économiques sévères. Pour stocker plus de données dans une appliance Teradata, Oracle Exadata ou Netezza, il fallait acheter des nœuds de calcul supplémentaires, même si la puissance de traitement n'était pas requise. Ce modèle linéaire de mise à l'échelle (Scale-up) est devenu financièrement insoutenable avec l'explosion volumétrique des années 2000.3  
Deuxièmement, la rigidité du *Schema-on-Write* créait un goulot d'étranglement opérationnel critique. L'intégration d'une nouvelle source de données nécessitait des semaines, voire des mois, de modélisation et de développement ETL (Extract, Transform, Load).5 Dans un marché numérique en accélération, où des entreprises comme Netflix ou les banques canadiennes cherchaient à réagir en temps réel aux comportements des utilisateurs, cette latence était inacceptable. Le Warehouse, conçu pour répondre à des questions connues sur des données structurées, s'est révélé incapable de gérer l'imprévu et la variété des données non structurées (logs, JSON, images, IoT).1

### **1.1.2 La Révolution du Data Lake (2010-2020) : Le Far West du Hadoop et l'Avènement du Cloud**

En réaction à la rigidité et au coût prohibitif des Warehouses, la décennie 2010 a vu l'émergence brutale du Data Lake, propulsée initialement par l'écosystème Apache Hadoop (HDFS) puis par le stockage objet infonuagique (Amazon S3, Azure Data Lake Storage, Google Cloud Storage).3

Le Data Lake a inversé le paradigme fondamental pour adopter le **Schema-on-Read** (schéma à la lecture). La priorité absolue était désormais la capture de la donnée brute, dans son format natif, à un coût marginal proche de zéro. On stocke d'abord, on structure plus tard. Cette approche a libéré les organisations des carcans de la modélisation a priori, permettant aux Data Scientists d'explorer des pétaoctets de données hétérogènes pour entraîner des modèles de Machine Learning, une tâche impossible dans un Warehouse SQL strict.2

L'architecture s'est alors transformée : le stockage a été découplé du calcul. On pouvait désormais stocker des exaoctets de données sur S3 pour un coût dérisoire, et lancer des clusters éphémères de calcul (Spark, Presto) uniquement lorsque nécessaire. Des formats de fichiers ouverts et colonnaires comme **Apache Parquet**, **Avro** et **ORC** sont devenus les standards de facto, remplaçant les formats propriétaires des bases de données traditionnelles.4

Pourtant, cette liberté architecturale a eu un prix élevé : la perte des garanties transactionnelles. Le Data Lake, dans sa version naïve basée sur HDFS ou S3 et orchestrée par Apache Hive, souffrait de limitations critiques qui l'ont souvent transformé en "Data Swamp" (marécage de données) :

1. **L'Absence d'ACID (Atomicity, Consistency, Isolation, Durability) :** Les opérations sur un Data Lake n'étaient pas atomiques. Si un job Spark écrivant 1000 fichiers plantait au 999ème, le lac restait dans un état corrompu, avec des données partielles visibles par les utilisateurs. Il n'y avait pas de mécanisme de rollback simple.2  
2. **L'Incohérence et l'Isolation Manquante :** Un analyste exécutant une requête de lecture pendant qu'un pipeline d'ingestion mettait à jour les données risquait de lire un mélange incohérent de nouvelles et d'anciennes données ("Dirty Reads").  
3. **Le Problème de Performance du Listage S3 :** C'est ici que résidait le problème technique le plus pernicieux. Le standard de gestion de table de l'époque, le **Hive Table Format**, suivait les données par répertoires. Pour savoir quels fichiers appartenaient à une table partitionnée, le moteur devait lister récursivement le contenu des répertoires sur le système de fichiers. Sur HDFS, c'était gérable. Mais sur un stockage objet comme S3, l'opération listObjects est lente et, jusqu'à récemment, souffrait de problèmes de cohérence éventuelle (Eventual Consistency). Pour des tables massives contenant des millions de fichiers, la simple planification d'une requête pouvait prendre des dizaines de minutes, uniquement pour lister les fichiers avant même de lire un seul octet de donnée.10

Des géants technologiques comme Netflix, qui géraient des exaoctets de données, se sont retrouvés dans une impasse. Ils avaient réussi à scaler le stockage et le calcul, mais la couche de gestion des métadonnées — le lien entre les deux — était brisée.13

### **1.1.3 La Synthèse Hégélienne : Le Data Lakehouse**

Le Data Lakehouse émerge au début de la décennie 2020 comme la synthèse nécessaire de ces deux mondes. Il ne s'agit pas d'un simple compromis, mais d'une nouvelle architecture unifiée qui vise à combiner **la fiabilité, la gouvernance et la performance ACID du Data Warehouse** avec **l'ouverture, la flexibilité et le faible coût du Data Lake**.3

Au cœur de cette architecture se trouve une innovation technologique majeure : le **Format de Table Ouvert** (Open Table Format). Contrairement au Warehouse qui enferme les données et les métadonnées dans une boîte noire propriétaire, le Lakehouse utilise des formats de fichiers ouverts (Parquet) stockés sur un stockage objet standard (S3/ADLS), mais y ajoute une couche de métadonnées intelligente et standardisée pour gérer les transactions et l'état de la table.

Le Lakehouse permet ainsi de servir tous les types de charges de travail (Workloads) sur une copie unique de la donnée :

* **Business Intelligence (BI) :** Requêtes SQL haute performance et tableaux de bord, domaine traditionnel du Warehouse.  
* **Data Science & ML :** Accès direct aux fichiers pour l'entraînement de modèles, domaine traditionnel du Lake.  
* **Streaming :** Ingestion et analyse en temps réel.

#### **Diagramme 1.1 : L'Évolution Architecturale (Warehouse \-\> Lake \-\> Lakehouse)**

Extrait de code

graph TD  
    subgraph Warehouse  
        A \--\>|ETL Rigide & Lent| B(Data Warehouse Monolithique)  
        B \--\>|SQL Standard| C  
        style B fill:\#e1f5fe,stroke:\#01579b,stroke-width:2px,color:\#000  
        desc1  
    end

    subgraph Lake  
        D \--\>|Ingestion Brute| E(Data Lake \- HDFS/S3)  
        E \--\>|Spark/Python| F  
        E \--\>|ETL Complexe| G  
        G \--\>|SQL| H  
        style E fill:\#fff3e0,stroke:\#e65100,stroke-width:2px,color:\#000  
        desc2  
    end

    subgraph Lakehouse \["L'Ère Lakehouse (2020+)"\]  
        I \--\>|Ingestion Unifiée| J(Lakehouse \- Apache Iceberg)  
        J \--\>|Moteur SQL| K  
        J \--\>|Moteur ML| L  
        J \--\>|Moteur Stream| M  
        style J fill:\#e8f5e9,stroke:\#1b5e20,stroke-width:2px,color:\#000  
        desc3  
    end

    Warehouse \--\> Lake  
    Lake \--\> Lakehouse

#### **Tableau 1.1 : Comparatif Détaillé \- Data Warehouse vs Data Lake vs Data Lakehouse**

Le tableau ci-dessous résume les différences fondamentales entre les trois architectures, mettant en lumière pourquoi le Lakehouse représente le point de convergence actuel pour les architectes de données.

| Dimension Architecturale | Data Warehouse (Legacy & Cloud 1.0) | Data Lake (Hadoop & Cloud 1.0) | Data Lakehouse (Apache Iceberg) |
| :---- | :---- | :---- | :---- |
| **Philosophie de Données** | *Schema-on-Write* (Rigide) | *Schema-on-Read* (Flexible) | *Schema-Enforced* & Flexible (Hybride) |
| **Format de Stockage** | Propriétaire, Fermé, Optimisé | Fichiers Ouverts (CSV, JSON, Parquet) | Fichiers Ouverts (Parquet/ORC) \+ Métadonnées |
| **Gestion des Transactions** | **ACID Complet** (Fiabilité maximale) | Aucune ou Limitée (Éventuellement cohérent) | **ACID Complet** (via Concurrence Optimiste) |
| **Couplage Compute/Storage** | Fortement Couplé (Coûteux à scaler) | Découplé (Scalabilité indépendante) | **Totalement Découplé** (Économique & Flexible) |
| **Gouvernance & Qualité** | Forte, Centralisée | Faible, "Data Swamp" fréquent | Forte, Unifiée, Supporte l'évolution de schéma |
| **Support Workloads** | BI, Reporting SQL | ML, IA, Exploration | **Unifié :** BI, SQL, ML, IA, Streaming |
| **Performance** | Très élevée pour le structuré | Variable, lente pour le listage de fichiers | Élevée (Pruning intelligent, Vectorisation) |
| **Ouverture** | Verrouillage Vendeur (Vendor Lock-in) | Standard Ouvert | **Standard Ouvert & Portable** (Multi-Moteurs) |

Sources : Synthèse des analyses comparatives de l'industrie.3

## ---

**1.2 Qu'est-ce qu'Apache Iceberg? Le Standard du Lakehouse Ouvert**

Pour l'architecte, il est crucial de définir ce qu'Apache Iceberg *est* et ce qu'il *n'est pas*. Iceberg n'est pas un moteur de stockage (comme S3 ou HDFS), ni un moteur d'exécution (comme Spark, Trino ou Flink). C'est une **spécification de format de table ouverte** (Open Table Format) accompagnée d'un ensemble de bibliothèques logicielles qui permettent aux moteurs de calcul d'interagir avec des tables stockées dans un Data Lake comme s'il s'agissait de tables SQL dans une base de données traditionnelle.19

### **1.2.1 La Genèse : Netflix et le Problème de l'Échelle**

Pour comprendre l'élégance de l'architecture Iceberg, il faut revenir au problème spécifique qui a motivé sa création chez Netflix vers 2017\. À cette époque, Netflix gérait un Data Lake massif sur Amazon S3, utilisant le format de table Hive standard. Ils se heurtaient à un mur de performance et de fiabilité lié à la nature même de Hive : le suivi des données par répertoires.13

Dans le modèle Hive, une table est un répertoire, et une partition est un sous-répertoire. Pour répondre à la question "Quelles données sont dans cette table?", le système devait lister le contenu de tous les répertoires correspondants. Sur un système de fichiers local ou HDFS, c'est une opération rapide. Sur un stockage objet distribué comme S3 :

1. Le listage est lent (latence réseau, pagination des résultats).  
2. Le listage n'est pas atomique (on peut voir une partie des fichiers pendant une écriture).  
3. Il n'y a pas de garantie immédiate que le fichier qu'on vient d'écrire apparaisse dans la liste (problème de cohérence éventuelle, bien que S3 ait amélioré ce point, le problème de performance O(N) demeure pour les grandes tables).

Ryan Blue et Dan Weeks, ingénieurs chez Netflix, ont réalisé que la solution n'était pas d'optimiser le listage S3, mais de **ne plus lister du tout**. Ils ont conçu Iceberg pour suivre les fichiers individuellement via une couche de métadonnées persistante. Si un fichier n'est pas explicitement listé dans les métadonnées d'Iceberg, il n'existe pas pour la table, même s'il est présent sur le disque. Cela a transformé la complexité de planification des requêtes de O(N) (nombre de fichiers) à O(1) (lecture du fichier de métadonnées).21

### **1.2.2 L'Adoption par Apple et la Standardisation Industrielle**

Bien que né chez Netflix, le projet a pris une dimension industrielle critique avec l'implication d'Apple. Confronté à des échelles de données titanesques pour ses services (iCloud, Siri, Apple Music), Apple avait besoin d'une solution capable de gérer des tables de plusieurs pétaoctets avec une fiabilité absolue. Apple a massivement contribué au projet, notamment en développant des outils de migration "Zero-Copy", permettant de convertir des tables Hive existantes en Iceberg sans réécrire les données, un levier d'adoption majeur pour les entreprises ayant déjà des Data Lakes matures.19

Aujourd'hui, Iceberg est un projet Top-Level de la Fondation Apache, soutenu par un consensus industriel rare incluant AWS, Google, Snowflake, Cloudera, et Databricks (via le support récent d'UniForm). Il est devenu le standard *de facto* pour l'interopérabilité dans le Lakehouse.20

### **1.2.3 Architecture Technique Profonde : Comment Iceberg Fonctionne?**

L'intelligence d'Iceberg réside dans sa structure hiérarchique de métadonnées, qui découple complètement l'état logique de la table de son stockage physique.

#### **1\. Le Fichier de Métadonnées (Metadata File \- metadata.json)**

C'est la racine de la table. Chaque modification de la table (commit) crée un *nouveau* fichier de métadonnées (versionné v1, v2, v3...). Ce fichier contient :

* Le schéma actuel de la table.  
* L'information de partitionnement.  
* La liste des **Snapshots** (instantanés) historiques.  
* Le pointeur vers le "Snapshot Courant".22

#### **2\. La Liste de Manifestes (Manifest List)**

Un Snapshot pointe vers une Liste de Manifestes. Ce fichier (généralement au format Avro) liste tous les fichiers manifestes qui composent l'image de la table à cet instant précis. Il contient aussi des statistiques agrégées (ex: les bornes min/max des valeurs de partition pour chaque manifeste), ce qui permet au moteur de requête d'ignorer des groupes entiers de fichiers sans même les ouvrir (Manifest Pruning).25

#### **3\. Les Fichiers Manifestes (Manifest Files)**

C'est le niveau le plus granulaire des métadonnées. Un fichier manifeste (Avro) contient la liste exacte des fichiers de données (Parquet/ORC) qui appartiennent à la table. Plus important encore, il stocke des statistiques **par fichier de données** :

* Compte de valeurs nulles.  
* Valeurs minimales et maximales pour chaque colonne (Lower/Upper bounds).  
  C'est cette richesse de métadonnées qui permet le "Data Skipping" extrême : si une requête cherche WHERE id \= 500 et que le manifeste indique que le fichier A contient des ID de 1 à 100, le moteur sait qu'il peut ignorer le fichier A sans jamais toucher à S3.21

#### **4\. Les Fichiers de Données (Data Files)**

À la base de la pyramide se trouvent les fichiers de données réels, stockés en formats standards ouverts comme Apache Parquet, ORC ou Avro. Iceberg est agnostique quant au format, mais Parquet est le plus courant pour l'analytique.8

## ---

**1.3 Les Avantages Architecturaux d'Apache Iceberg**

Pourquoi un architecte d'une grande organisation canadienne, comme la Banque Nationale ou Bell, devrait-il recommander une migration vers Iceberg? Au-delà de la performance, Iceberg apporte des capacités fonctionnelles qui résolvent des problèmes d'affaires critiques.

### **1.3.1 Transactions ACID et Isolation des Snapshots : La Fin des "Dirty Reads"**

Dans un environnement transactionnel, l'intégrité est primordiale. Iceberg introduit les garanties ACID dans le Data Lake grâce à un mécanisme de **Concurrence Optimiste** (Optimistic Concurrency Control \- OCC).

* **Le Mécanisme :** Lorsqu'un moteur (ex: Spark) veut écrire dans une table, il lit d'abord le fichier de métadonnées courant (ex: v1.json). Il prépare ses nouveaux fichiers de données et crée un nouveau fichier de métadonnées (v2.json). Au moment du commit, il tente de faire basculer atomiquement le pointeur de la table de v1 à v2. Si un autre processus a commité v1.1 entre-temps, le premier processus détecte le conflit, rebase ses changements sur v1.1 et réessaie.27  
* **L'Isolation (Snapshot Isolation) :** Les lecteurs voient toujours une version cohérente de la table. Si un rapport financier complexe prend 30 minutes à s'exécuter, il verra exactement les données telles qu'elles étaient au début de la requête, même si des milliers de nouvelles transactions sont insérées pendant ce temps. Cela élimine totalement les lectures incohérentes qui polluaient les Data Lakes de première génération.29

### **1.3.2 L'Évolution de Schéma (Schema Evolution) : Agilité Maximale**

Dans les systèmes traditionnels (Hive), renommer une colonne était souvent impossible sans réécrire physiquement toute la table, une opération coûteuse et risquée.

Iceberg résout cela en introduisant une couche d'abstraction : il mappe les colonnes par **ID Unique** et non par nom.

* Si vous renommez client\_id (ID: 1\) en customer\_id (ID: 1), Iceberg met simplement à jour le fichier de métadonnées. Les fichiers Parquet existants ne sont pas touchés.  
* Si vous supprimez une colonne, elle est simplement marquée comme inactive dans les métadonnées.  
* Les changements de type (ex: int vers long) sont gérés de manière sécurisée.  
  Cette capacité permet une évolution fluide des modèles de données en production, sans temps d'arrêt, une caractéristique essentielle pour le CI/CD des données (DataOps).31

### **1.3.3 Le Partitionnement Masqué (Hidden Partitioning) : L'Arme Secrète contre l'Erreur Humaine**

Le partitionnement est essentiel pour la performance, mais dans Hive, il était explicite et dangereux. Si une table était partitionnée par jour (dt=2023-01-01), l'analyste *devait* obligatoirement inclure WHERE dt \=... dans sa requête. S'il requêtait sur le timestamp métier created\_at, Hive ignorait le partitionnement et scannait toute la table (Full Table Scan), entraînant des coûts cloud explosifs.

Iceberg introduit le **Partitionnement Masqué**. L'architecte définit une *transformation* de partitionnement (ex: day(created\_at)). Iceberg stocke cette relation.

* L'analyste écrit : SELECT \* FROM logs WHERE created\_at \> '2023-01-01T10:00:00'.  
* Iceberg comprend automatiquement que cela correspond à la partition 2023-01-01 et ne scanne que les fichiers pertinents.  
* L'utilisateur n'a plus besoin de connaître la structure physique de la table. Le partitionnement devient une optimisation transparente, pas une contrainte logique.33

### **1.3.4 Le Voyage dans le Temps (Time Travel) et le Rollback**

Puisque chaque écriture crée un nouveau Snapshot immuable et qu'Iceberg conserve l'historique dans les métadonnées :

1. **Time Travel :** Un Data Scientist peut reproduire exactement l'entraînement d'un modèle fait il y a trois mois en requêtant : SELECT \* FROM table FOR SYSTEM\_TIME AS OF '2023-10-01'. C'est crucial pour l'auditabilité des modèles IA.25  
2. **Rollback :** Si un pipeline ETL corrompu injecte des données erronées à 3h00 du matin, l'équipe d'ingénierie peut instantanément restaurer la table à l'état de 2h59 via une simple commande CALL catalog.system.rollback\_to\_snapshot(...). Le temps moyen de résolution (MTTR) passe d'heures (restauration de backup) à secondes.32

## ---

**1.4 Les Composants d'un Lakehouse Iceberg : Une Architecture Composée**

Une architecture Iceberg n'est pas monolithique ; elle est modulaire et composable. L'architecte doit assembler quatre couches distinctes pour bâtir un Lakehouse fonctionnel.

### **1.4.1 La Couche de Stockage (Storage Layer)**

C'est la fondation physique. Iceberg exige un système de fichiers qui supporte des sémantiques basiques (écriture, lecture, suppression).

* **Stockage Objet (Cloud) :** Amazon S3, Azure Data Lake Storage Gen2 (ADLS), Google Cloud Storage (GCS). C'est le déploiement le plus courant au Canada.  
* Stockage On-Premise : MinIO, Ceph, ou HDFS (bien que l'usage de HDFS décline au profit du stockage objet S3-compatible).  
  L'atout ici est le coût : on utilise le stockage le moins cher disponible pour conserver des données critiques avec des garanties de base de données.21

### **1.4.2 La Couche de Catalogue (Catalog Layer) \- Le Cerveau**

C'est le composant le plus critique pour la cohérence. Le Catalogue est le système qui détient le pointeur vers le fichier de métadonnées *courant*. C'est l'arbitre de la vérité atomique. Il existe plusieurs implémentations, créant ce qu'on appelle la "Guerre des Catalogues" :

1. **Hive Metastore (HMS) :** L'approche legacy. Compatible avec tout, mais souffre de problèmes de performance et de verrouillage (Locking) à grande échelle.36  
2. **Catalogues Cloud (AWS Glue) :** Très populaire pour les architectures 100% AWS. Simple, serverless, mais crée un verrouillage vendeur (Vendor Lock-in) et ne gère pas toujours bien les commits atomiques multi-tables.36  
3. **Project Nessie ("Git for Data") :** Une approche moderne qui apporte les concepts de Git aux données. On peut créer des branches de données (dev, experiment), faire des commits, et merger en production. Idéal pour le DataOps avancé et le CI/CD des données.37  
4. **REST Catalog :** C'est le **standard émergent**. Iceberg a défini une API REST standard pour parler à n'importe quel catalogue. Cela permet de découpler totalement le moteur de calcul du stockage des métadonnées. Des services comme **Snowflake Polaris**, **Tabular** (acquis par Databricks) ou des implémentations open-source implémentent cette interface. Pour un architecte soucieux de pérennité, c'est souvent le choix recommandé aujourd'hui.37

### **1.4.3 La Couche d'Ingestion (Ingestion Layer)**

Comment les données entrent-elles dans le Lakehouse?

* **Batch :** Apache Spark est le moteur dominant pour les gros traitements batch d'écriture Iceberg.  
* **Streaming :** Apache Flink ou Kafka Connect (avec Iceberg Sink) permettent d'écrire des données en continu dans le lac avec des garanties *exactly-once*, rendant les données disponibles pour l'analyse quelques minutes (ou secondes) après leur génération.13

### **1.4.4 La Couche de Consommation (Consumption Layer)**

L'avantage du format ouvert est que n'importe quel moteur peut lire les données.

* **Analytique Interactive (SQL) :** **Trino** (anciennement PrestoSQL) et **Starburst** sont les champions de la requête SQL rapide sur Iceberg. Ils permettent de fédérer les requêtes.  
* **Data Warehouse Modernes :** Snowflake, BigQuery et Amazon Redshift supportent désormais la lecture native des tables Iceberg externes, permettant d'utiliser leur puissance de calcul sans avoir à déplacer/copier les données dans leur format propriétaire.20

## ---

**1.5 Le Contexte Canadien et Québécois : Pourquoi Iceberg est une Nécessité Stratégique**

L'adoption d'Apache Iceberg au Canada, et particulièrement au Québec, n'est pas seulement motivée par la technologie, mais par un paysage réglementaire et opérationnel unique.

### **1.5.1 La Loi 25 et le Droit à l'Oubli : Un Défi Architectural**

La **Loi 25** (Loi modernisant des dispositions législatives en matière de protection des renseignements personnels) impose aux entreprises québécoises des obligations strictes, comparables au RGPD européen. Deux exigences touchent directement l'architecture de données : le **droit à l'effacement** (droit à l'oubli) et la **portabilité des données**.45

Dans un Data Lake traditionnel (fichiers immuables), supprimer les données d'un individu spécifique (ex: "Supprimer toutes les traces de M. Tremblay") est un cauchemar technique. Il faut identifier tous les fichiers contenant ses données, les lire, filtrer la ligne, et réécrire les fichiers. Sur des pétaoctets de données, c'est prohibitif en termes de coût de calcul (I/O) et de temps.

La Solution Iceberg : Copy-on-Write vs Merge-on-Read  
Iceberg offre une réponse élégante et conforme via deux stratégies de suppression 47 :

1. **Copy-on-Write (COW) :** Lors de la suppression, Iceberg réécrit immédiatement les fichiers de données affectés sans la donnée cible. C'est idéal pour la conformité stricte et la performance de lecture maximale, mais coûteux à l'écriture.  
2. **Merge-on-Read (MOR) :** Iceberg écrit simplement un petit "Delete File" (fichier de suppression) qui indique "L'ID client 123 est supprimé". La suppression est instantanée. Lors de la lecture, le moteur fusionne les données et les suppressions pour ne pas afficher l'enregistrement.  
   * *Stratégie recommandée pour le Québec :* Utiliser le **Merge-on-Read** pour traiter les demandes de droit à l'oubli au quotidien (haute réactivité, faible coût), et exécuter une tâche de maintenance ("Compaction") hebdomadaire pour réécrire physiquement les fichiers (passage en COW) afin de nettoyer définitivement les données et optimiser les lectures. Cela permet une conformité auditable à la Loi 25 tout en maîtrisant les coûts Cloud.

### **1.5.2 Souveraineté des Données et Résidence**

Pour les institutions fédérales ou des entreprises comme **Bell Canada**, la souveraineté des données est critique. Les données sensibles doivent souvent résider physiquement sur le sol canadien pour éviter les implications du CLOUD Act américain.50

L'architecture Lakehouse Iceberg facilite cette conformité par son découplage :

* Les données (fichiers Parquet chiffrés) peuvent être stockées dans des buckets S3 régionaux précis (ca-central-1 à Montréal ou Toronto).  
* Le catalogue et les moteurs de calcul peuvent être configurés pour n'opérer que dans cette juridiction.  
* Contrairement aux solutions SaaS "boîte noire" où l'on ne sait pas toujours où la donnée transite, Iceberg offre une transparence totale sur la localisation physique des fichiers.

### **1.5.3 Cas d'Usage Canadiens Emblématiques**

L'adoption est déjà massive dans l'écosystème local :

* **Shopify :** L'entreprise a migré l'intégralité de ses données analytiques vers Iceberg. Confrontés à des problèmes de cohérence S3 et de performance de métadonnées avec leur legacy Hive, ils ont adopté Iceberg pour garantir la fiabilité de leurs rapports marchands. Ils utilisent massivement **Trino** sur Iceberg pour permettre des requêtes interactives sur des pétaoctets de données.43  
* **Secteur Bancaire (Banque Nationale, Desjardins) :** Ces institutions modernisent leurs plateformes pour briser les silos. Le Lakehouse leur permet de centraliser les données transactionnelles (Core Banking) et les données d'interaction (Logs web, App mobile) dans une structure unifiée et gouvernée, facilitant la détection de fraude en temps réel et la personnalisation client (Customer 360\) tout en respectant les cadres réglementaires stricts.54

## ---

**1.6 Résumé et Perspectives**

Le Data Lakehouse basé sur Apache Iceberg représente bien plus qu'une évolution technique ; c'est une maturation de l'ingénierie des données. En réconciliant la rigueur transactionnelle du Data Warehouse avec l'échelle infinie du Data Lake, Iceberg offre aux architectes une plateforme unifiée capable de soutenir l'avenir de l'entreprise numérique.

**Points Clés à Retenir pour l'Architecte :**

1. **Fiabilité avant tout :** Les transactions ACID et l'isolation des snapshots transforment le Data Lake d'un "marécage" en une plateforme critique fiable.  
2. **Performance à l'échelle :** L'architecture basée sur les fichiers manifestes élimine les goulots d'étranglement du listage S3, permettant des tables de taille illimitée.  
3. **Agilité et Conformité :** L'évolution de schéma, le partitionnement masqué et les suppressions granulaires (Merge-on-Read) sont des atouts indispensables pour naviguer dans l'environnement réglementaire québécois (Loi 25\) et les besoins d'affaires changeants.  
4. **Interopérabilité :** Le standard ouvert et le catalogue REST garantissent que vos données survivront aux outils d'aujourd'hui, vous protégeant contre le verrouillage vendeur.

Dans les chapitres suivants, nous quitterons la théorie pour la pratique : nous explorerons comment concevoir, déployer et optimiser concrètement cette architecture au sein de votre entreprise.

#### **Ouvrages cités**

1. Lakes? Warehouses? Lakehouses? A short history of Data Architecture | by QuantumBlack, AI by McKinsey \- Medium, dernier accès : janvier 10, 2026, [https://medium.com/quantumblack/lakes-warehouses-lakehouses-a-short-history-of-data-architecture-bc942b0ed463](https://medium.com/quantumblack/lakes-warehouses-lakehouses-a-short-history-of-data-architecture-bc942b0ed463)  
2. Understanding Modern Data Architecture: An Evolution from Warehouses to Mesh \- Addepto, dernier accès : janvier 10, 2026, [https://addepto.com/blog/understanding-modern-data-architecture-an-evolution-from-warehouses-to-mesh/](https://addepto.com/blog/understanding-modern-data-architecture-an-evolution-from-warehouses-to-mesh/)  
3. Understanding the evolution of data lakes | by Capital One Tech \- Medium, dernier accès : janvier 10, 2026, [https://medium.com/capital-one-tech/understanding-the-evolution-of-data-lakes-37d13b809be9](https://medium.com/capital-one-tech/understanding-the-evolution-of-data-lakes-37d13b809be9)  
4. The Modern Data Stack: How The Evolution of Data Architecture Led to The Data Intelligence Platform \- Databricks, dernier accès : janvier 10, 2026, [https://www.databricks.com/blog/modern-data-stack-how-evolution-data-architecture-led-data-intelligence-platform](https://www.databricks.com/blog/modern-data-stack-how-evolution-data-architecture-led-data-intelligence-platform)  
5. From Data to Data Platforms: The Story Behind the emergence of Data Warehouses, Lakes, Mesh and…, dernier accès : janvier 10, 2026, [https://medium.com/@saurabh.engg.it/from-data-to-data-platforms-the-story-behind-the-emergence-of-data-warehouses-lakes-mesh-and-3460cc1b1781](https://medium.com/@saurabh.engg.it/from-data-to-data-platforms-the-story-behind-the-emergence-of-data-warehouses-lakes-mesh-and-3460cc1b1781)  
6. Why Lakehouse Matters: A Deep Dive into the Data Architecture Evolution | by Mohan Vamsi | Dec, 2025, dernier accès : janvier 10, 2026, [https://medium.com/@mohanvamsi75/why-lakehouse-matters-a-deep-dive-into-the-data-architecture-evolution-8bf8f6fbe5a5](https://medium.com/@mohanvamsi75/why-lakehouse-matters-a-deep-dive-into-the-data-architecture-evolution-8bf8f6fbe5a5)  
7. Data Warehouses vs. Data Lakes vs. Data Lakehouses \- IBM, dernier accès : janvier 10, 2026, [https://www.ibm.com/think/topics/data-warehouse-vs-data-lake-vs-data-lakehouse](https://www.ibm.com/think/topics/data-warehouse-vs-data-lake-vs-data-lakehouse)  
8. Apache Iceberg Explained: A Complete Guide for Beginners \- DataCamp, dernier accès : janvier 10, 2026, [https://www.datacamp.com/tutorial/apache-iceberg](https://www.datacamp.com/tutorial/apache-iceberg)  
9. From Data Warehouse to Lakehouse: How Architecture Has Evolved \- Binariks, dernier accès : janvier 10, 2026, [https://binariks.com/blog/warehouse-to-lakehouse-architecture/](https://binariks.com/blog/warehouse-to-lakehouse-architecture/)  
10. Committing work to S3 with the S3A Committers \- Apache Hadoop, dernier accès : janvier 10, 2026, [https://hadoop.apache.org/docs/r3.2.1/hadoop-aws/tools/hadoop-aws/committers.html](https://hadoop.apache.org/docs/r3.2.1/hadoop-aws/tools/hadoop-aws/committers.html)  
11. Optimizing S3 Bulk Listings for Performant Hive Queries \- Qubole, dernier accès : janvier 10, 2026, [https://www.qubole.com/blog/optimizing-s3-bulk-listings-for-performant-hive-queries](https://www.qubole.com/blog/optimizing-s3-bulk-listings-for-performant-hive-queries)  
12. S3 Strong Consistency | Hacker News, dernier accès : janvier 10, 2026, [https://news.ycombinator.com/item?id=25271791](https://news.ycombinator.com/item?id=25271791)  
13. How and Why Netflix Built a Real-Time Distributed Graph: Part 1 — Ingesting and Processing Data Streams at Internet Scale, dernier accès : janvier 10, 2026, [https://netflixtechblog.com/how-and-why-netflix-built-a-real-time-distributed-graph-part-1-ingesting-and-processing-data-80113e124acc](https://netflixtechblog.com/how-and-why-netflix-built-a-real-time-distributed-graph-part-1-ingesting-and-processing-data-80113e124acc)  
14. Netflix's Apache Iceberg Data Lake Migration \- AWS, dernier accès : janvier 10, 2026, [https://aws.amazon.com/awstv/watch/3db41488539/](https://aws.amazon.com/awstv/watch/3db41488539/)  
15. The data lakehouse evolution \- DEV Community, dernier accès : janvier 10, 2026, [https://dev.to/apachedoris/the-data-lakehouse-evolution-3a7e](https://dev.to/apachedoris/the-data-lakehouse-evolution-3a7e)  
16. Data Lake vs Data Warehouse vs Data Mart \- Difference Between Cloud Storage Solutions, dernier accès : janvier 10, 2026, [https://aws.amazon.com/compare/the-difference-between-a-data-warehouse-data-lake-and-data-mart/](https://aws.amazon.com/compare/the-difference-between-a-data-warehouse-data-lake-and-data-mart/)  
17. Re: Comparison between data warehouse, data lake and data lakehouse, dernier accès : janvier 10, 2026, [https://community.fabric.microsoft.com/t5/Data-Warehouse/Comparison-between-data-warehouse-data-lake-and-data-lakehouse/m-p/4065820](https://community.fabric.microsoft.com/t5/Data-Warehouse/Comparison-between-data-warehouse-data-lake-and-data-lakehouse/m-p/4065820)  
18. Evolution to the Data Lakehouse | Databricks Blog, dernier accès : janvier 10, 2026, [https://www.databricks.com/blog/2021/05/19/evolution-to-the-data-lakehouse.html](https://www.databricks.com/blog/2021/05/19/evolution-to-the-data-lakehouse.html)  
19. How Iceberg Powers Data and AI Applications at Apple, Netflix, LinkedIn, and Other Leading Companies | Qlik Blog, dernier accès : janvier 10, 2026, [https://www.qlik.com/blog/how-iceberg-powers-data-and-ai-applications-at-apple-netflix-linkedin-and](https://www.qlik.com/blog/how-iceberg-powers-data-and-ai-applications-at-apple-netflix-linkedin-and)  
20. The Iceberg Wave: How an Open Format Became an Enterprise Standard | Blog \- Cloudera, dernier accès : janvier 10, 2026, [https://www.cloudera.com/blog/business/the-iceberg-wave-how-an-open-format-became-an-enterprise-standard.html](https://www.cloudera.com/blog/business/the-iceberg-wave-how-an-open-format-became-an-enterprise-standard.html)  
21. Apache Iceberg Architecture: 3 Core Components to Understand \- Atlan, dernier accès : janvier 10, 2026, [https://atlan.com/know/iceberg/apache-iceberg-architecture/](https://atlan.com/know/iceberg/apache-iceberg-architecture/)  
22. Apache Iceberg Metadata Explained: Snapshots & Manifests | Fastest Open Source Data Replication Tool \- OLake, dernier accès : janvier 10, 2026, [https://olake.io/blog/2025/10/03/iceberg-metadata/](https://olake.io/blog/2025/10/03/iceberg-metadata/)  
23. How Apple Uses Apache Iceberg to Power Its Lakehouse at Scale \- Data Engineer Things, dernier accès : janvier 10, 2026, [https://blog.dataengineerthings.org/how-apple-uses-apache-iceberg-to-power-its-lakehouse-at-scale-f19b27a64c62](https://blog.dataengineerthings.org/how-apple-uses-apache-iceberg-to-power-its-lakehouse-at-scale-f19b27a64c62)  
24. Spec \- Apache Iceberg™, dernier accès : janvier 10, 2026, [https://iceberg.apache.org/spec/](https://iceberg.apache.org/spec/)  
25. Apache Iceberg: Architectural Insights | Dremio, dernier accès : janvier 10, 2026, [https://www.dremio.com/resources/guides/apache-iceberg-an-architectural-look-under-the-covers/](https://www.dremio.com/resources/guides/apache-iceberg-an-architectural-look-under-the-covers/)  
26. Apache Iceberg internal Structure in Details | by Kundan Singh \- Medium, dernier accès : janvier 10, 2026, [https://medium.com/@kundansingh0619/apache-iceberg-internal-structure-in-details-7150a3c736fe](https://medium.com/@kundansingh0619/apache-iceberg-internal-structure-in-details-7150a3c736fe)  
27. Manage concurrent write conflicts in Apache Iceberg on the AWS Glue Data Catalog, dernier accès : janvier 10, 2026, [https://aws.amazon.com/blogs/big-data/manage-concurrent-write-conflicts-in-apache-iceberg-on-the-aws-glue-data-catalog/](https://aws.amazon.com/blogs/big-data/manage-concurrent-write-conflicts-in-apache-iceberg-on-the-aws-glue-data-catalog/)  
28. Reliability \- Apache Iceberg™, dernier accès : janvier 10, 2026, [https://iceberg.apache.org/docs/1.6.0/reliability/](https://iceberg.apache.org/docs/1.6.0/reliability/)  
29. Understanding Apache Iceberg's Consistency Model Part 2 \- Jack Vanlightly, dernier accès : janvier 10, 2026, [https://jack-vanlightly.com/analyses/2024/8/5/apache-icebergs-consistency-model-part-2](https://jack-vanlightly.com/analyses/2024/8/5/apache-icebergs-consistency-model-part-2)  
30. Optimizing Big Data with Apache Iceberg in Databricks: | by Shraddha Shetty | Medium, dernier accès : janvier 10, 2026, [https://medium.com/@dataninsight/optimizing-big-data-with-apache-iceberg-in-databricks-fed1b61c4db2](https://medium.com/@dataninsight/optimizing-big-data-with-apache-iceberg-in-databricks-fed1b61c4db2)  
31. Apache Iceberg \- Apache Iceberg™, dernier accès : janvier 10, 2026, [https://iceberg.apache.org/](https://iceberg.apache.org/)  
32. The why and how of partitioning in Apache Iceberg \- IBM Developer, dernier accès : janvier 10, 2026, [https://developer.ibm.com/articles/the-why-and-how-of-partitioning-in-apache-iceberg/](https://developer.ibm.com/articles/the-why-and-how-of-partitioning-in-apache-iceberg/)  
33. Iceberg Partitioning vs. Hive Partitioning | Fastest Open Source Data Replication Tool \- OLake, dernier accès : janvier 10, 2026, [https://olake.io/iceberg/hive-partitioning-vs-iceberg-partitioning/](https://olake.io/iceberg/hive-partitioning-vs-iceberg-partitioning/)  
34. Partitioning Practices in Apache Hive and Apache Iceberg \- DEV Community, dernier accès : janvier 10, 2026, [https://dev.to/alexmercedcoder/partitioning-practices-in-apache-hive-and-apache-iceberg-46kg](https://dev.to/alexmercedcoder/partitioning-practices-in-apache-hive-and-apache-iceberg-46kg)  
35. Partitioning in Apache Iceberg: Do You Need It? | by Manoj Thammu | Medium, dernier accès : janvier 10, 2026, [https://medium.com/@mthammus/partitioning-in-apache-iceberg-do-you-need-it-4aa8b5798c44](https://medium.com/@mthammus/partitioning-in-apache-iceberg-do-you-need-it-4aa8b5798c44)  
36. Iceberg Operational Toolkit: Advantages & Cataloging \- Nexla, dernier accès : janvier 10, 2026, [https://nexla.com/blog/iceberg-operational-toolkit-advantages-and-cataloging/](https://nexla.com/blog/iceberg-operational-toolkit-advantages-and-cataloging/)  
37. Mastering Apache Iceberg Catalogs: A Comprehensive Guide for Data Engineers | itversity, dernier accès : janvier 10, 2026, [https://medium.com/itversity/iceberg-catalogs-a-guide-for-data-engineers-a6190c7bf381](https://medium.com/itversity/iceberg-catalogs-a-guide-for-data-engineers-a6190c7bf381)  
38. Iceberg Catalog Formats: Which One Is Best \- Orchestra, dernier accès : janvier 10, 2026, [https://www.getorchestra.io/guides/iceberg-catalog-formats-which-one-is-best](https://www.getorchestra.io/guides/iceberg-catalog-formats-which-one-is-best)  
39. Comprehensive Data Catalog Comparison \- Onehouse.ai, dernier accès : janvier 10, 2026, [https://www.onehouse.ai/blog/comprehensive-data-catalog-comparison](https://www.onehouse.ai/blog/comprehensive-data-catalog-comparison)  
40. Announcing full Apache Iceberg™ support in Databricks, dernier accès : janvier 10, 2026, [https://www.databricks.com/blog/announcing-full-apache-iceberg-support-databricks](https://www.databricks.com/blog/announcing-full-apache-iceberg-support-databricks)  
41. Introducing Polaris Catalog: An Open Source Catalog for Apache Iceberg \- Snowflake, dernier accès : janvier 10, 2026, [https://www.snowflake.com/en/blog/introducing-polaris-catalog/](https://www.snowflake.com/en/blog/introducing-polaris-catalog/)  
42. Incremental Processing using Netflix Maestro and Apache Iceberg, dernier accès : janvier 10, 2026, [https://netflixtechblog.com/incremental-processing-using-netflix-maestro-and-apache-iceberg-b8ba072ddeeb](https://netflixtechblog.com/incremental-processing-using-netflix-maestro-and-apache-iceberg-b8ba072ddeeb)  
43. What I Learned from Studying How SaaS Companies Build Open Data Lakehouses | by Harry Tan | Medium, dernier accès : janvier 10, 2026, [https://medium.com/@datasmiles/how-saas-leaders-built-scalable-open-data-lakehouses-5d665254b777](https://medium.com/@datasmiles/how-saas-leaders-built-scalable-open-data-lakehouses-5d665254b777)  
44. Rewriting History \- Migrating petabytes of data to Apache Iceberg using Trino, dernier accès : janvier 10, 2026, [https://trino.io/assets/blog/trino-summit-2022/Shopify@Trino.pdf](https://trino.io/assets/blog/trino-summit-2022/Shopify@Trino.pdf)  
45. Quebec Law 25/ Bill 64 | TrustArc, dernier accès : janvier 10, 2026, [https://trustarc.com/regulations/quebec-law-25/](https://trustarc.com/regulations/quebec-law-25/)  
46. Quebec's Law 25: What Is It and What Do You Need to Know? | Blog \- OneTrust, dernier accès : janvier 10, 2026, [https://www.onetrust.com/blog/quebecs-law-25-what-is-it-and-what-do-you-need-to-know/](https://www.onetrust.com/blog/quebecs-law-25-what-is-it-and-what-do-you-need-to-know/)  
47. Apache Iceberg and the Right to Be Forgotten | Blog Post \- Dremio, dernier accès : janvier 10, 2026, [https://www.dremio.com/blog/apache-iceberg-and-the-right-to-be-forgotten/](https://www.dremio.com/blog/apache-iceberg-and-the-right-to-be-forgotten/)  
48. Data Retention in Apache Iceberg: Implementation Details and Best Practices | Yuval Yogev \- Ryft, dernier accès : janvier 10, 2026, [https://www.ryft.io/blog/data-retention-in-apache-iceberg-implementation-details-and-best-practices](https://www.ryft.io/blog/data-retention-in-apache-iceberg-implementation-details-and-best-practices)  
49. Handling "Right to be Forgotten" in GDPR and CCPA using Delta Live Tables (DLT), dernier accès : janvier 10, 2026, [https://www.databricks.com/blog/handling-right-be-forgotten-gdpr-and-ccpa-using-delta-live-tables-dlt](https://www.databricks.com/blog/handling-right-be-forgotten-gdpr-and-ccpa-using-delta-live-tables-dlt)  
50. Government of Canada White Paper: Data Sovereignty and Public Cloud, dernier accès : janvier 10, 2026, [https://www.canada.ca/en/government/system/digital-government/digital-government-innovations/cloud-services/digital-sovereignty/gc-white-paper-data-sovereignty-public-cloud.html](https://www.canada.ca/en/government/system/digital-government/digital-government-innovations/cloud-services/digital-sovereignty/gc-white-paper-data-sovereignty-public-cloud.html)  
51. CLOUD Act and FISA: Secure Your Data Sovereignty \- ited, dernier accès : janvier 10, 2026, [https://www.it-ed.com/en/data-sovereignty/](https://www.it-ed.com/en/data-sovereignty/)  
52. Canada's AI moment: The criticality of sovereignty for a thriving digital future, dernier accès : janvier 10, 2026, [https://explore.business.bell.ca/blog/canada-ai-moment-criticality-sovereignty-thriving-digital-future](https://explore.business.bell.ca/blog/canada-ai-moment-criticality-sovereignty-thriving-digital-future)  
53. Shopify cuts execution time from hours to seconds with Iceberg and Trino \- Starburst, dernier accès : janvier 10, 2026, [https://www.starburst.io/blog/shopify-cuts-execution-time-from-hours-to-seconds-with-iceberg-and-trino/](https://www.starburst.io/blog/shopify-cuts-execution-time-from-hours-to-seconds-with-iceberg-and-trino/)  
54. Data Lakehouse Architecture for AI: Implementation Guide | Informatica, dernier accès : janvier 10, 2026, [https://www.informatica.com/resources/articles/data-lakehouse-architecture-ai-guide.html](https://www.informatica.com/resources/articles/data-lakehouse-architecture-ai-guide.html)  
55. National Bank of Canada Structures a Cloud Transformation Program \- AWS, dernier accès : janvier 10, 2026, [https://aws.amazon.com/solutions/case-studies/national-bank-canada-case-study/](https://aws.amazon.com/solutions/case-studies/national-bank-canada-case-study/)  
56. Inside Desjardins' Digital Banking Transformation | FinTech Magazine, dernier accès : janvier 10, 2026, [https://fintechmagazine.com/company-reports/inside-desjardins-digital-banking-transformation](https://fintechmagazine.com/company-reports/inside-desjardins-digital-banking-transformation)  
57. Achieving Financial Innovation: Desjardins' Success with nCino, dernier accès : janvier 10, 2026, [https://www.ncino.com/blog/achieving-financial-innovation-desjardins-success-ncino](https://www.ncino.com/blog/achieving-financial-innovation-desjardins-success-ncino)