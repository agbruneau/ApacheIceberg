# Apache Iceberg pour Architectes
## Guide complet pour concevoir, implémenter et opérer un Data Lakehouse moderne

---

## **PARTIE 1 : LA VALEUR DU LAKEHOUSE APACHE ICEBERG**

### **Chapitre 1 - LE MONDE DU LAKEHOUSE APACHE ICEBERG**

- 1.1 Qu'est-ce qu'un data lakehouse
  - 1.1.1 L'essor des entrepôts de données
  - 1.1.2 Le passage aux entrepôts de données cloud
  - 1.1.3 Le data lake et l'ère Hadoop
  - 1.1.4 Apache Iceberg : La clé du data lakehouse
  - 1.1.5 Le data lakehouse : le meilleur des deux mondes
- 1.2 Qu'est-ce qu'Apache Iceberg ?
  - 1.2.1 Le besoin d'un format de table
  - 1.2.2 Comment Apache Iceberg gère les métadonnées
  - 1.2.3 Caractéristiques clés d'Apache Iceberg
  - 1.2.4 Apache Iceberg en tant que standard open-source
- 1.3 Les avantages d'Apache Iceberg
  - 1.3.1 Transactions ACID
  - 1.3.2 Évolution des tables
  - 1.3.3 Voyage dans le temps et requêtes basées sur les snapshots
  - 1.3.4 Partitionnement masqué pour réduire les scans complets accidentels de table
  - 1.3.5 Efficacité des coûts et performance optimisée des requêtes
- 1.4 Les composants d'un lakehouse Apache Iceberg
  - 1.4.1 La couche de stockage : Les fondations de votre lakehouse
  - 1.4.2 La couche d'ingestion : Alimenter les tables Iceberg en données
  - 1.4.3 La couche de catalogue : Le point d'entrée de votre lakehouse
  - 1.4.4 La couche de fédération : Modélisation et accélération des données
  - 1.4.5 La couche de consommation : Apporter de la valeur à l'entreprise
- 1.5 Résumé

### **Chapitre 2 - ANATOMIE TECHNIQUE D'APACHE ICEBERG**

- 2.1 Hiérarchie des fichiers et gestion des métadonnées
  - 2.1.1 Le fichier de métadonnées (metadata.json) : Le pointeur atomique
  - 2.1.2 La liste des manifestes (Manifest List) : Index grossier pour l'élagage
  - 2.1.3 Les fichiers manifestes (Manifest Files) : Métadonnées granulaires par fichier
  - 2.1.4 Les fichiers de données : Formats Parquet, ORC et Avro
  - 2.1.5 Isolation ACID et concurrence optimiste
- 2.2 Stratégies d'écriture : Copy-on-Write vs Merge-on-Read
  - 2.2.1 Copy-on-Write (CoW) : Optimisé pour les lectures
    - 2.2.1.1 Mécanisme et sémantique d'écriture
    - 2.2.1.2 Avantages et limitations
    - 2.2.1.3 Cas d'usage optimaux (batch, dimensions peu modifiées)
  - 2.2.2 Merge-on-Read (MoR) : Optimisé pour le streaming
    - 2.2.2.1 Séparation des data files et delete files
    - 2.2.2.2 Fusion à la volée à la lecture
    - 2.2.2.3 Avantages pour l'ingestion haute fréquence
    - 2.2.2.4 Nécessité de compaction régulière
  - 2.2.3 Comparaison et choix de stratégie
    - 2.2.3.1 Matrice décisionnelle selon les exigences
    - 2.2.3.2 Impact sur la latence d'écriture et de lecture
    - 2.2.3.3 Considérations de coût et maintenance
- 2.3 Gestion de l'évolution de schéma
  - 2.3.1 Identifiants de colonnes (Column IDs) vs noms
  - 2.3.2 Ajout, suppression et renommage de colonnes
  - 2.3.3 Évolution des types de données
  - 2.3.4 Compatibilité avec les fichiers historiques
- 2.4 Partitionnement masqué (Hidden Partitioning)
  - 2.4.1 Concept et avantages par rapport au partitionnement explicite
  - 2.4.2 Transformations de partition supportées (year, month, day, hour, bucket)
  - 2.4.3 Élagage automatique et optimisation des requêtes
  - 2.4.4 Stratégies de partitionnement pour le streaming
- 2.5 Résumé

### **Chapitre 3 - MISE EN PRATIQUE AVEC APACHE ICEBERG**

- 3.1 Configuration d'un environnement Apache Iceberg
  - 3.1.1 Prérequis : Installer Docker
  - 3.1.2 Création du fichier Docker compose
  - 3.1.3 Exécution de l'environnement
  - 3.1.4 Accès aux services
- 3.2 Création de tables Iceberg dans Spark
  - 3.2.1 Peuplement de la base de données PostgreSQL
  - 3.2.2 Démarrage de l'environnement Apache Spark
  - 3.2.3 Configuration d'Apache Spark pour Iceberg
  - 3.2.4 Chargement des données de PostgreSQL dans Iceberg
  - 3.2.5 Vérification du stockage des données dans MinIO
- 3.3 Lecture des tables Iceberg dans Dremio
  - 3.3.1 Démarrage de Dremio
  - 3.3.2 Connexion de Dremio au catalogue Nessie
  - 3.3.3 Interrogation des tables Iceberg dans Dremio
- 3.4 Création d'un tableau de bord BI à partir de vos tables Iceberg
  - 3.4.1 Démarrage d'Apache Superset
  - 3.4.2 Connexion de Superset à Dremio
  - 3.4.3 Création d'un jeu de données à partir des tables Iceberg
  - 3.4.4 Construction de graphiques et tableaux de bord
- 3.5 Résumé

---

## **PARTIE 2 : CONCEVOIR VOTRE ARCHITECTURE ICEBERG**

### **Chapitre 4 - PRÉPARER VOTRE PASSAGE À APACHE ICEBERG**

- 4.1 Réalisation de l'audit de votre plateforme de données
  - 4.1.1 Qui sont les parties prenantes ?
  - 4.1.2 Que devez-vous demander aux parties prenantes ?
  - 4.1.3 Réalisation d'un audit technologique
  - 4.1.4 Évaluation de l'existant pour le streaming et temps réel
- 4.2 L'audit de la Banque Hamerliwa en action
  - 4.2.1 La Banque Hamerliwa interviewe ses parties prenantes
  - 4.2.2 La Banque Hamerliwa audite sa technologie
  - 4.2.3 La Banque Hamerliwa résume les résultats de son audit
- 4.3 De l'audit aux exigences : Poser les fondations de la conception
  - 4.3.1 Définition des exigences de stockage
  - 4.3.2 Définition des exigences d'ingestion
    - 4.3.2.1 Exigences pour ingestion batch
    - 4.3.2.2 Exigences pour ingestion streaming et temps réel
  - 4.3.3 Définition des exigences de catalogue
  - 4.3.4 Définition des exigences de fédération
  - 4.3.5 Définition des exigences de consommation
  - 4.3.6 La Banque Hamerliwa établit ses exigences
- 4.4 Plan architectural et présentation itinérante
  - 4.4.1 La Banque Hamerliwa crée son plan architectural
  - 4.4.2 La Banque Hamerliwa effectue une présentation itinérante
- 4.5 Résumé

### **Chapitre 5 - SÉLECTION DE LA COUCHE DE STOCKAGE**

- 5.1 Exigences de stockage
  - 5.1.1 Exigences de performance de récupération de fichiers
  - 5.1.2 Exigences de sécurité
  - 5.1.3 Exigences d'intégrité
  - 5.1.4 Exigences de coût et de surcharge opérationnelle
- 5.2 Stockage par blocs vs objet
  - 5.2.1 Stockage par blocs
  - 5.2.2 Stockage objet
- 5.3 Les standards dans la couche de stockage
  - 5.3.1 Apache Parquet
  - 5.3.2 L'API S3
- 5.4 Solutions de stockage
  - 5.4.1 Résumé de comparaison des fournisseurs
  - 5.4.2 Hadoop (HDFS)
  - 5.4.3 Amazon S3
  - 5.4.4 Google Cloud Storage
  - 5.4.5 Azure Blob Storage et ADLS
  - 5.4.6 MinIO
  - 5.4.7 Ceph
  - 5.4.8 NetApp StorageGRID
  - 5.4.9 Pure Storage
  - 5.4.10 Dell ECS
  - 5.4.11 Wasabi
- 5.5 Sélection basée sur les exigences
  - 5.5.1 Exigences de performance
  - 5.5.2 Exigences de sécurité
  - 5.5.3 Exigences d'intégrité
  - 5.5.4 Exigences de coût et opérationnelles
- 5.6 Résumé

### **Chapitre 6 - ARCHITECTURE DE LA COUCHE D'INGESTION**

- 6.1 Exigences d'ingestion
  - 6.1.1 Débit d'ingestion et latence
  - 6.1.2 Fiabilité et tolérance aux pannes
  - 6.1.3 Gestion et évolution du schéma
  - 6.1.4 Complexité opérationnelle et maintenabilité
  - 6.1.5 Exactly-once semantics et garanties de traitement
- 6.2 Modèles et architectures d'ingestion
  - 6.2.1 Ingestion par lots
  - 6.2.2 Ingestion micro-batch et incrémentale
  - 6.2.3 Ingestion en streaming
- 6.3 Comment Iceberg gère les écritures
  - 6.3.1 Sémantique d'écriture dans Iceberg
  - 6.3.2 Protocoles de commit et gestion des conflits
  - 6.3.3 Gestion des transactions et isolation
- 6.4 Patterns d'ingestion Kafka vers Iceberg
  - 6.4.1 Pattern 1 : Confluent Tableflow (Approche Zero-ETL)
    - 6.4.1.1 Concept et fonctionnement
    - 6.4.1.2 Avantages : Simplicité opérationnelle et maintenance
    - 6.4.1.3 Limitations et cas d'usage appropriés
    - 6.4.1.4 Gestion automatique des petits fichiers et compaction
  - 6.4.2 Pattern 2 : Ingestion via Apache Flink SQL
    - 6.4.2.1 Configuration des sources Kafka
    - 6.4.2.2 Transformations complexes en temps réel (ETL)
    - 6.4.2.3 Enrichissement et masquage de données sensibles (PII)
    - 6.4.2.4 Gestion des CDC (Change Data Capture) avec Upserts
    - 6.4.2.5 Exemples pratiques de pipelines Flink SQL
  - 6.4.3 Pattern 3 : Kafka Connect Iceberg Sink
    - 6.4.3.1 Configuration du connecteur
    - 6.4.3.2 Exactly-once semantics et coordination
    - 6.4.3.3 Topic de contrôle (iceberg-control) pour la coordination distribuée
    - 6.4.3.4 Configuration critique pour les environnements réglementés
- 6.5 Intégration avec Kafka Schema Registry
  - 6.5.1 Synchronisation des évolutions de schéma
  - 6.5.2 Support des formats Avro, Protobuf et JSON Schema
  - 6.5.3 Gestion des colonnes ajoutées, renommées et supprimées
  - 6.5.4 Typage complexe et structures imbriquées
- 6.6 Outils et frameworks pour l'ingestion
  - 6.6.1 Apache Spark
  - 6.6.2 Apache Flink
  - 6.6.3 Apache NiFi
  - 6.6.4 Fivetran
  - 6.6.5 Qlik
  - 6.6.6 Airbyte
  - 6.6.7 Confluent et Kafka
  - 6.6.8 Redpanda
  - 6.6.9 Services d'ingestion cloud-native
  - 6.6.10 Considérations de sélection d'outils
- 6.7 Application des exigences d'ingestion en contexte
  - 6.7.1 Prioriser la faible latence (streaming temps réel)
  - 6.7.2 Gérer le haut débit (milliards d'événements par jour)
  - 6.7.3 Prendre en charge les transformations complexes
  - 6.7.4 Gérer l'évolution du schéma
  - 6.7.5 Équilibrer la surcharge opérationnelle
  - 6.7.6 Considérer les environnements cloud existants
- 6.8 Résumé

### **Chapitre 7 - IMPLÉMENTATION DE LA COUCHE DE CATALOGUE**

- 7.1 Le rôle du catalogue dans les lakehouses Apache Iceberg
  - 7.1.1 Responsabilités du catalogue
  - 7.1.2 Interactions du catalogue avec les moteurs de requête et de traitement
- 7.2 Évaluation des exigences du catalogue
  - 7.2.1 Performance, disponibilité et échelle
  - 7.2.2 Gouvernance et traçabilité des métadonnées
  - 7.2.3 Sécurité et conformité
  - 7.2.4 Flexibilité de déploiement et compatibilité avec l'écosystème
  - 7.2.5 Coût et surcharge opérationnelle
  - 7.2.6 Fédération de catalogues et architectures mesh
- 7.3 Spécification Apache Iceberg REST Catalog
  - 7.3.1 Avant la spécification Apache Iceberg REST
  - 7.3.2 La solution : Standardisation et interopérabilité
- 7.4 Options de catalogue : Exploration de l'écosystème
  - 7.4.1 Hadoop Catalog
  - 7.4.2 Hive Catalog
  - 7.4.3 JDBC Catalog
  - 7.4.4 Apache Polaris
  - 7.4.5 Project Nessie
  - 7.4.6 Apache Gravitino
  - 7.4.7 Lakekeeper
  - 7.4.8 AWS Glue Data Catalog
  - 7.4.9 Dremio Catalog
  - 7.4.10 Snowflake Open Catalog
  - 7.4.11 Databricks Unity Catalog
- 7.5 Choisir le bon catalogue : Évaluer les options à travers des scénarios
  - 7.5.1 Scénario : Une équipe de données de taille moyenne migrant depuis Hive
  - 7.5.2 Scénario : Une startup cloud-native en croissance rapide
  - 7.5.3 Scénario : Une entreprise multinationale avec une gouvernance stricte des données
  - 7.5.4 Scénario : Une startup SaaS priorisant la simplicité opérationnelle
  - 7.5.5 Scénario : Une grande entreprise avec des besoins multi-cloud et de gouvernance fédérée
  - 7.5.6 Scénario : Entreprise financière nécessitant un clonage quotidien d'environnement pour les tests de stress
  - 7.5.7 Scénario : Migration Iceberg progressive avec fédération de requêtes à travers les systèmes legacy
  - 7.5.8 Scénario : Adoption légère du lakehouse avec catalogue Hadoop et Python
- 7.6 Résumé

### **Chapitre 8 - CONCEPTION DE LA COUCHE DE FÉDÉRATION**

- 8.1 Ce qu'est la fédération de données et pourquoi elle compte
  - 8.1.1 Cas d'usage et défis courants motivant les besoins de fédération
  - 8.1.2 Comment la fédération s'aligne avec l'agilité et l'accessibilité
- 8.2 Exigences clés pour la fédération
  - 8.2.1 Prendre en charge des sources de données diverses sans duplication
  - 8.2.2 Assurer une sémantique et une logique métier cohérentes
  - 8.2.3 Fournir une connectivité transparente pour les outils d'analyse
  - 8.2.4 Introduction à Dremio et Trino
- 8.3 Dremio
  - 8.3.1 Architecture de Dremio
  - 8.3.2 Écosystème de connecteurs de Dremio et focus centré sur Iceberg
  - 8.3.3 Améliorations de performance de Dremio
- 8.4 Trino
  - 8.4.1 Architecture modulaire pour la prise en charge de nombreuses sources
  - 8.4.2 Flexibilité et configurabilité pour des environnements complexes
  - 8.4.3 Évolution dirigée par la communauté et extensions de fournisseurs
  - 8.4.4 Considérations de couche sémantique dans Trino
- 8.5 Modèles de déploiement
  - 8.5.1 Déploiement avec Dremio
  - 8.5.2 Déploiement avec Trino
- 8.6 Scénarios de décision de plateforme de fédération
  - 8.6.1 Environnement multi-sources fragmenté : Trino pour la largeur des connecteurs
  - 8.6.2 Construction d'un lakehouse Iceberg natif : Dremio pour les fonctionnalités Iceberg natives
  - 8.6.3 Autonomiser les utilisateurs métier avec l'interface utilisateur et les jeux de données gouvernés : Dremio
  - 8.6.4 Interrogation légère des jeux de données Hudi : Trino via AWS Athena
  - 8.6.5 Modernisation Cloudera on-prem : Trino remplaçant Impala pour les performances
  - 8.6.6 Stratégie Iceberg cloud hybride : Dremio reliant on-prem et ADLS
- 8.7 Alternatives de fédération
  - 8.7.1 Virtualisation via les raccourcis dans OneLake
  - 8.7.2 Virtualisation de données native IA avec Spice.ai
  - 8.7.3 Choisir la bonne solution
- 8.8 Résumé

### **Chapitre 9 - COMPRENDRE LA COUCHE DE CONSOMMATION**

- 9.1 Revenir sur les avantages du lakehouse pour la consommation
- 9.2 Connecter le lakehouse aux personnes
- 9.3 Revenir sur les exigences de notre audit
  - 9.3.1 Interprétation des exigences pour la consommation
  - 9.3.2 Exigences pour les outils BI
  - 9.3.3 Exigences pour les environnements de notebooks interactifs
  - 9.3.4 Exigences pour l'IA et les outils spécialisés de consommation de données
- 9.4 Interfaces ouvertes pour une consommation transparente
  - 9.4.1 JDBC et ODBC
  - 9.4.2 Arrow Flight
  - 9.4.3 Model Context Protocol (MCP)
- 9.5 Outils d'intelligence d'affaires dans le lakehouse
  - 9.5.1 Outils BI open source
  - 9.5.2 Outils BI commerciaux
- 9.6 Outils pour les charges de travail d'IA et d'apprentissage automatique
  - 9.6.1 Frameworks ML et intégration avec Iceberg
  - 9.6.2 Feature stores et gestion des caractéristiques
  - 9.6.3 MLOps et pipelines d'entraînement
  - 9.6.4 Inférence en temps réel sur données Lakehouse
- 9.7 Choisir les bons outils de consommation : Dix scénarios illustrés
  - 9.7.1 Startup avec un focus data science
  - 9.7.2 Grande institution financière avec une gouvernance stricte
  - 9.7.3 Plateforme e-commerce de taille moyenne construisant des analyses intégrées
  - 9.7.4 Organisation média décentralisée permettant l'analyse en libre-service
  - 9.7.5 Agence gouvernementale équilibrant la transparence publique et le contrôle interne
  - 9.7.6 Fournisseur de soins de santé avec des contraintes de conformité et de localité des données
  - 9.7.7 Entreprise de logistique unifiant les opérations en temps réel et l'analyse historique
  - 9.7.8 Entreprise SaaS offrant un accès personnalisable aux données aux clients
  - 9.7.9 Organisation à but non lucratif soutenant la recherche collaborative
  - 9.7.10 Entreprise manufacturière permettant la maintenance prédictive
- 9.8 Résumé

---

## **PARTIE 3 : OPÉRER VOTRE LAKEHOUSE APACHE ICEBERG**

### **Chapitre 10 - MAINTENIR UN LAKEHOUSE ICEBERG EN PRODUCTION**

- 10.1 Problème : Fichiers de données sous-optimaux
  - 10.1.1 Petits fichiers
  - 10.1.2 Données mal colocalisées
  - 10.1.3 Prolifération des métadonnées
  - 10.1.4 Impacts de performance Merge-on-read (MOR)
- 10.2 Solution : Compaction
  - 10.2.1 Qu'est-ce que la compaction ?
  - 10.2.2 Stratégies de compaction
    - 10.2.2.1 Bin-Packing : Regroupement des petits fichiers
    - 10.2.2.2 Sort : Tri des données pour optimiser les requêtes
    - 10.2.2.3 Z-Order : Tri multidimensionnel pour requêtes multi-prédicats
  - 10.2.3 Taille de fichier cible et paramètres
  - 10.2.4 Fichiers à inclure et sélection
  - 10.2.5 Utilisation de filtres pour délimiter la compaction
  - 10.2.6 Fréquence recommandée selon les stratégies
- 10.3 Gestion de l'empreinte de stockage et rétention des données
  - 10.3.1 Exécution de l'expiration des snapshots
  - 10.3.2 COW vs MOR : Implications pour la rétention des données
  - 10.3.3 Considérations réglementaires pour la suppression des données
  - 10.3.4 Suppression sécurisée et droit à l'oubli (Loi 25, RGPD)
    - 10.3.4.1 Procédure en trois étapes : Suppression logique, expiration, nettoyage physique
    - 10.3.4.2 Utilisation des procédures expire_snapshots et remove_orphan_files
- 10.4 Exploration des tables de métadonnées d'Apache Iceberg
  - 10.4.1 Tables de métadonnées disponibles
  - 10.4.2 Requêtes d'inspection et de diagnostic
  - 10.4.3 Automatisation du monitoring via les métadonnées
- 10.5 Contrôles d'accès dans un lakehouse Iceberg
  - 10.5.1 Contrôles de la couche de stockage
  - 10.5.2 Contrôles au niveau du catalogue
  - 10.5.3 Contrôles d'accès au niveau du moteur
- 10.6 Résumé

### **Chapitre 11 - OPÉRATIONNALISER APACHE ICEBERG**

- 11.1 Orchestration du lakehouse
  - 11.1.1 Choix des outils et modèles d'orchestration
  - 11.1.2 Déclencheurs basés sur les métadonnées pour une maintenance proactive
  - 11.1.3 Politiques de maintenance par table
  - 11.1.4 Intégration de la surveillance et des alertes
  - 11.1.5 Mise en pratique de l'orchestration
- 11.2 Audit du lakehouse
  - 11.2.1 Tirer parti de l'historique des snapshots pour le suivi des changements
  - 11.2.2 Utilisation du branchement et du marquage pour la gouvernance
  - 11.2.3 Implémentation des politiques de rétention des fichiers et snapshots
  - 11.2.4 Orchestration pratique des politiques de rétention
  - 11.2.5 Suppression sécurisée des données
  - 11.2.6 Audit d'accès et gouvernance
  - 11.2.7 Audit pratique avec Iceberg : Exemples de flux de travail
- 11.3 Récupération après sinistre dans le lakehouse
  - 11.3.1 Le rôle du catalogue de métadonnées dans la récupération après sinistre
  - 11.3.2 Protection contre la perte et la corruption des données
  - 11.3.3 Récupération multi-région et multi-environnement
  - 11.3.4 Retour en arrière et voyage dans le temps dans la réponse aux incidents
  - 11.3.5 Automatisation des procédures de récupération après sinistre
  - 11.3.6 Validation de la préparation à la récupération
  - 11.3.7 Récupération après sinistre par automatisation
  - 11.3.8 Exemples pratiques : Automatisation des flux de travail de récupération
- 11.4 Résumé

### **Chapitre 12 - L'ÉVOLUTION VERS LE STREAMING LAKEHOUSE**

- 12.1 De l'Architecture Lambda au Streaming Lakehouse
  - 12.1.1 Les limites de l'Architecture Lambda
    - 12.1.1.1 La couche de vitesse (Speed Layer) : Technologies et limitations
    - 12.1.1.2 La couche de lot (Batch Layer) : Latence et complexité
    - 12.1.1.3 Complexité opérationnelle et divergence des données
    - 12.1.1.4 Le problème de la logique dupliquée et de la maintenance
  - 12.1.2 L'avènement de l'Architecture Kappa
    - 12.1.2.1 Traitement unifié par flux : Concept et avantages
    - 12.1.2.2 Limitations des moteurs de streaming purs pour l'analytique OLAP
  - 12.1.3 Le Streaming Lakehouse : La Synthèse
    - 12.1.3.1 Ingestion en temps réel : Disponibilité immédiate des données
    - 12.1.3.2 Correction transactionnelle avec propriétés ACID
    - 12.1.3.3 Unification du stockage : Un seul référentiel pour temps réel et analytique
- 12.2 Le Rôle de Confluent et Kafka dans l'Écosystème Moderne
  - 12.2.1 Kafka comme système nerveux central
    - 12.2.1.1 Au-delà du simple transport : Plateforme de traitement
    - 12.2.1.2 Découplage et scalabilité horizontale
  - 12.2.2 Plateforme de traitement et de gouvernance des données en mouvement
    - 12.2.2.1 Schema Registry et gouvernance des schémas
    - 12.2.2.2 Kafka Connect et intégration avec l'écosystème
  - 12.2.3 Cas d'usage : Transformation architecturale des institutions financières
    - 12.2.3.1 Banque Royale du Canada (RBC) : Passage du mainframe à l'architecture événementielle
    - 12.2.3.2 Monolith Slicing : Libération des données des systèmes cœurs
    - 12.2.3.3 Réduction de la latence de détection des anomalies (semaines → secondes)
    - 12.2.3.4 Réduction des coûts MIPS et modernisation
  - 12.2.4 Découplage des systèmes producteurs et consommateurs
    - 12.2.4.1 Avantages pour l'agilité et l'innovation
    - 12.2.4.2 Scalabilité indépendante des composants
  - 12.2.5 Exemple Shopify : Traitement de milliards d'événements quotidiens
    - 12.2.5.1 Architecture Kubernetes pour Kafka
    - 12.2.5.2 Intégration avec Iceberg pour l'analytique
- 12.3 Résumé

### **Chapitre 13 - SÉCURITÉ, GOUVERNANCE ET CONFORMITÉ DU LAKEHOUSE**

- 13.1 Fondements de la sécurité dans un Lakehouse Apache Iceberg
  - 13.1.1 Modèles de menaces spécifiques aux architectures Lakehouse
    - 13.1.1.1 Surface d'attaque distribuée (stockage, catalogue, moteurs)
    - 13.1.1.2 Risques liés à l'accès multi-tenant
    - 13.1.1.3 Vulnérabilités des pipelines d'ingestion
  - 13.1.2 Principes de défense en profondeur
    - 13.1.2.1 Segmentation réseau et isolation
    - 13.1.2.2 Principe du moindre privilège
    - 13.1.2.3 Chiffrement au repos et en transit
  - 13.1.3 Architecture Zero Trust pour le Lakehouse
    - 13.1.3.1 Authentification continue et contextuelle
    - 13.1.3.2 Micro-segmentation des accès aux données
    - 13.1.3.3 Validation des identités à chaque couche
- 13.2 Gouvernance des données à l'échelle entreprise
  - 13.2.1 Catalogage et lignage des données
    - 13.2.1.1 Métadonnées techniques vs métadonnées métier
    - 13.2.1.2 Traçabilité end-to-end avec Apache Atlas et alternatives
    - 13.2.1.3 Intégration du lignage dans les pipelines Iceberg
  - 13.2.2 Qualité des données et observabilité
    - 13.2.2.1 Validation de schéma et contrats de données
    - 13.2.2.2 Métriques de qualité automatisées (Great Expectations, Deequ)
    - 13.2.2.3 Alertes et tableaux de bord de santé des données
  - 13.2.3 Gestion du cycle de vie des données
    - 13.2.3.1 Classification automatique des données sensibles
    - 13.2.3.2 Politiques de rétention et archivage
    - 13.2.3.3 Suppression sécurisée et droit à l'oubli
- 13.3 Conformité réglementaire et cadres légaux
  - 13.3.1 Réglementations canadiennes
    - 13.3.1.1 LPRPDE (Loi sur la protection des renseignements personnels)
    - 13.3.1.2 Loi 25 du Québec et implications pour les Lakehouses
    - 13.3.1.3 Projet de loi C-27 et implications fédérales
    - 13.3.1.4 Directives du BSIF pour les institutions financières
    - 13.3.1.5 Exigences de résidence des données au Canada
  - 13.3.2 Réglementations internationales
    - 13.3.2.1 RGPD/GDPR et transferts transfrontaliers
    - 13.3.2.2 SOC 2 Type II et certifications de sécurité
    - 13.3.2.3 PCI-DSS pour les données de paiement
    - 13.3.2.4 HIPAA pour les données de santé
  - 13.3.3 Audit et preuve de conformité
    - 13.3.3.1 Journalisation exhaustive des accès
    - 13.3.3.2 Rapports automatisés pour les auditeurs
    - 13.3.3.3 Démonstration de conformité via time-travel Iceberg
- 13.4 Contrôles d'accès avancés
  - 13.4.1 RBAC, ABAC et contrôles hybrides
    - 13.4.1.1 Modèles basés sur les rôles vs attributs
    - 13.4.1.2 Politiques dynamiques selon le contexte
    - 13.4.1.3 Intégration avec les systèmes d'identité d'entreprise (LDAP, Azure AD)
  - 13.4.2 Sécurité au niveau des lignes et colonnes
    - 13.4.2.1 Row-Level Security (RLS) dans les moteurs de requête
    - 13.4.2.2 Column-Level Security et masquage dynamique
    - 13.4.2.3 Implémentation avec Dremio, Trino et Spark
  - 13.4.3 Tokenisation et anonymisation
    - 13.4.3.1 Pseudonymisation réversible vs irréversible
    - 13.4.3.2 Techniques de k-anonymat et differential privacy
    - 13.4.3.3 Cas d'usage : données de test et environnements non-production
- 13.5 Patterns d'architecture sécurisée
  - 13.5.1 Architecture multi-zone de sécurité
    - 13.5.1.1 Zone raw, curated et consumption
    - 13.5.1.2 Isolation des environnements sensibles
    - 13.5.1.3 Data Clean Rooms pour le partage sécurisé
  - 13.5.2 Gestion des secrets et credentials
    - 13.5.2.1 HashiCorp Vault, AWS Secrets Manager, Azure Key Vault
    - 13.5.2.2 Rotation automatique des clés de chiffrement
    - 13.5.2.3 Injection sécurisée dans les pipelines
  - 13.5.3 Détection et réponse aux incidents
    - 13.5.3.1 SIEM et corrélation d'événements de sécurité
    - 13.5.3.2 Détection d'anomalies d'accès aux données
    - 13.5.3.3 Playbooks de réponse aux incidents data breach
- 13.6 Résumé

### **Chapitre 14 - L'INTÉGRATION AVEC MICROSOFT FABRIC ET POWER BI**

- 14.1 OneLake Shortcuts et Virtualisation
  - 14.1.1 Concept de Shortcuts dans OneLake
    - 14.1.1.1 Montage de tables Iceberg externes sans copie de données
    - 14.1.1.2 Support des sources S3 et ADLS générées par Confluent/Snowflake
  - 14.1.2 Virtualisation Bidirectionnelle
    - 14.1.2.1 Couche de traduction de métadonnées basée sur Apache XTable
    - 14.1.2.2 Mapping dynamique des métadonnées Iceberg vers Delta Lake
    - 14.1.2.3 Accessibilité via moteurs Spark de Fabric et SQL Endpoint
  - 14.1.3 Contraintes et considérations
    - 14.1.3.1 Contrainte de région : alignement géographique requis
    - 14.1.3.2 Impact sur les coûts d'egress et les performances
    - 14.1.3.3 Cas spécifique : banques canadiennes et région Canada Central
- 14.2 Power BI Direct Lake : Latence et Performance
  - 14.2.1 Le mode Direct Lake comme rupture technologique
    - 14.2.1.1 Comparaison avec le mode Import et DirectQuery
    - 14.2.1.2 Lecture directe des fichiers Parquet par le moteur VertiPaq
    - 14.2.1.3 Avantages pour les volumes de données massifs
  - 14.2.2 Impact et capacités
    - 14.2.2.1 Visualisation de volumes massifs (Pétaoctets)
    - 14.2.2.2 Performances interactives proches du mode Import
    - 14.2.2.3 Élimination de la duplication des données
  - 14.2.3 Latence de synchronisation
    - 14.2.3.1 Processus de synchronisation Kafka → Iceberg → OneLake → Power BI
    - 14.2.3.2 Variation de latence selon la configuration de cache
    - 14.2.3.3 Considérations pour tableaux de bord opérationnels temps réel
- 14.3 Résumé

### **Chapitre 15 - CONTEXTE CANADIEN ET ÉTUDES DE CAS**

- 15.1 Introduction au contexte canadien
  - 15.1.1 Souveraineté numérique et modernisation des infrastructures
  - 15.1.2 Influence sur l'adoption des technologies de Streaming Lakehouse
- 15.2 Étude de Cas : Banque Royale du Canada (RBC)
  - 15.2.1 Contexte et défis initiaux
    - 15.2.1.1 Dépendance aux mainframes coûteux (MIPS)
    - 15.2.1.2 Difficulté à innover sur des données cloisonnées
  - 15.2.2 Solution architecturale
    - 15.2.2.1 Utilisation de Kafka pour "découper le monolithe" (Monolith Slicing)
    - 15.2.2.2 Capture en temps réel des transactions
    - 15.2.2.3 Diffusion vers applications aval sans re-solliciter le mainframe
  - 15.2.3 Résultats et bénéfices
    - 15.2.3.1 Réduction drastique des coûts MIPS
    - 15.2.3.2 Accélération de la détection de fraude (de plusieurs semaines à quelques secondes)
    - 15.2.3.3 Historisation avec Iceberg pour l'entraînement de modèles IA
    - 15.2.3.4 Données souveraines hébergées au Canada
- 15.3 Étude de Cas : Bell Canada
  - 15.3.1 Contexte et défis
    - 15.3.1.1 Volumes massifs de logs hétérogènes
    - 15.3.1.2 Sources multiples : routeurs, box, antennes
  - 15.3.2 Solution mise en place
    - 15.3.2.1 Ingestion via Kafka
    - 15.3.2.2 Normalisation des logs
    - 15.3.2.3 Passage à une architecture Lakehouse
  - 15.3.3 Bénéfices opérationnels
    - 15.3.3.1 Conservation à long terme à faible coût (conformité légale)
    - 15.3.3.2 Stockage objet économique
    - 15.3.3.3 Requêtes SQL rapides pour investigation d'incidents de sécurité
    - 15.3.3.4 Support du SOC (Security Operations Center)
- 15.4 Souveraineté des Données et Infrastructure Régionale
  - 15.4.1 Conformité et directives fédérales
    - 15.4.1.1 Stratégie infonuagique du gouvernement du Canada
    - 15.4.1.2 Exigences de résidence des données au pays
  - 15.4.2 Comparaison régionale : AWS Canada vs US East
    - 15.4.2.1 AWS Canada Central (ca-central-1) vs US East (N. Virginia)
    - 15.4.2.2 Coûts et considérations financières (+10-15% pour la région canadienne)
    - 15.4.2.3 Déploiement de services de pointe
    - 15.4.2.4 Mandat pour données PII bancaires et gouvernementales
  - 15.4.3 Analyse de latence
    - 15.4.3.1 Latence réseau pour utilisateurs basés à Toronto/Montréal
    - 15.4.3.2 Comparaison ca-central-1 (<10ms) vs Virginie (~20-30ms)
    - 15.4.3.3 Impact sur applications interactives Power BI Direct Lake
- 15.5 Résumé

### **Chapitre 16 - CONCLUSION FINALE ET PERSPECTIVES 2026-2030**

- 16.1 L'architecture de Streaming Lakehouse comme état de l'art
  - 16.1.1 Unification de Kafka, Iceberg et Fabric
  - 16.1.2 Concilier l'agilité du temps réel avec la rigueur de l'analytique transactionnelle
  - 16.1.3 Positionnement en 2025-2026 dans la gestion de données moderne
  - 16.1.4 Maturité de l'écosystème et adoption enterprise
- 16.2 Perspectives technologiques 2026-2028
  - 16.2.1 L'émergence du "Diskless Kafka"
    - 16.2.1.1 Kafka utilisant Iceberg/S3 comme stockage primaire
    - 16.2.1.2 Élimination de la duplication sur disques locaux
    - 16.2.1.3 Impact sur l'architecture et les performances
  - 16.2.2 Standardisation des catalogues via le protocole REST
    - 16.2.2.1 Avantages de la standardisation
    - 16.2.2.2 Interopérabilité accrue entre systèmes
  - 16.2.3 Convergence des formats de table ouverts
    - 16.2.3.1 Apache XTable et l'interopérabilité Delta/Iceberg/Hudi
    - 16.2.3.2 Vers un standard unifié ?
    - 16.2.3.3 Impact sur les stratégies de migration
- 16.3 Horizons 2028-2030 : L'ère de l'Intelligence Artificielle
  - 16.3.1 Lakehouse et IA générative
    - 16.3.1.1 Feature stores intégrés avec Iceberg
    - 16.3.1.2 RAG (Retrieval-Augmented Generation) sur données Lakehouse
    - 16.3.1.3 Gouvernance des données d'entraînement IA
  - 16.3.2 Automatisation et self-driving Lakehouse
    - 16.3.2.1 Optimisation automatique des tables (auto-compaction, clustering)
    - 16.3.2.2 Recommandations d'indexation basées sur l'IA
    - 16.3.2.3 Détection proactive des anomalies de données
  - 16.3.3 Edge computing et Lakehouse distribué
    - 16.3.3.1 Synchronisation edge-to-cloud
    - 16.3.3.2 Traitement local avec consolidation centralisée
    - 16.3.3.3 Cas d'usage IoT industriel et retail
- 16.4 Implications stratégiques pour les organisations canadiennes
  - 16.4.1 Investissement technologique comme décision stratégique
  - 16.4.2 Bénéfices organisationnels
    - 16.4.2.1 Innovation et compétitivité
    - 16.4.2.2 Conformité réglementaire renforcée
    - 16.4.2.3 Adaptation à une économie numérique accélérée
  - 16.4.3 Développement des compétences et talents
    - 16.4.3.1 Formation des équipes aux technologies Lakehouse
    - 16.4.3.2 Écosystème de partenaires et intégrateurs
    - 16.4.3.3 Communautés open source au Canada
  - 16.4.4 Recommandations pour une adoption réussie
    - 16.4.4.1 Approche incrémentale et proof-of-concept
    - 16.4.4.2 Centre d'excellence Lakehouse
    - 16.4.4.3 Métriques de succès et ROI
- 16.5 Résumé final et appel à l'action

---

## **ANNEXES**

### **Annexe A - LA SPÉCIFICATION APACHE ICEBERG**

- A.1 Comprendre la spécification Iceberg
  - A.1.1 Qu'est-ce qu'une spécification de format de table ?
  - A.1.2 Pourquoi Iceberg formalise le comportement des tables
  - A.1.3 Évolution de la spécification : principes de versionnement et compatibilité
- A.2 Versions du format de table Iceberg
  - A.2.1 Version 1 : Fondation pour les tables analytiques
  - A.2.2 Version 2 : Suppressions au niveau des lignes et écritures plus strictes
  - A.2.3 Version 3 : Types étendus et capacités avancées
  - A.2.4 Version 4 : Performance, portabilité et préparation au temps réel
- A.3 Gestion des snapshots et métadonnées de table
  - A.3.1 Fichiers de métadonnées de table
  - A.3.2 Snapshots et la liste des manifestes
  - A.3.3 Numéros de séquence et concurrence optimiste
- A.4 La spécification REST Catalog
  - A.4.1 Aperçu et objectif
  - A.4.2 Configuration du catalogue et points de terminaison par défaut
  - A.4.3 Espaces de noms, tables et vues
  - A.4.4 Enregistrement des tables, métriques et transactions
  - A.4.5 Prise en charge OAuth2 et considérations de sécurité
  - A.4.6 Le point de terminaison de planification de scan
- A.5 Spécification du format de fichier Puffin
  - A.5.1 Qu'est-ce qu'un fichier Puffin ?
  - A.5.2 Stockage des métriques au niveau des colonnes et index personnalisés
  - A.5.3 Intégration avec les métadonnées de table Iceberg
- A.6 Compatibilité et migration
  - A.6.1 Lecture et écriture à travers les versions de format
  - A.6.2 Mise à niveau des tables vers des versions plus récentes de la spécification
  - A.6.3 Gestion de la compatibilité descendante en pratique

### **Annexe B - GLOSSAIRE**

- B.1 Terminologie Apache Iceberg
- B.2 Terminologie Lakehouse et Data Engineering
- B.3 Terminologie Streaming et Kafka
- B.4 Acronymes et abréviations
