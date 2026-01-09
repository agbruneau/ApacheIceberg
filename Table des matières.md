Apache Iceber pour Architectes

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

### **Chapitre 2 - MISE EN PRATIQUE AVEC APACHE ICEBERG**
- 2.1 Configuration d'un environnement Apache Iceberg
  - 2.1.1 Prérequis : Installer Docker
  - 2.1.2 Création du fichier Docker compose
  - 2.1.3 Exécution de l'environnement
  - 2.1.4 Accès aux services
- 2.2 Création de tables Iceberg dans Spark
  - 2.2.1 Peuplement de la base de données PostgreSQL
  - 2.2.2 Démarrage de l'environnement Apache Spark
  - 2.2.3 Configuration d'Apache Spark pour Iceberg
  - 2.2.4 Chargement des données de PostgreSQL dans Iceberg
  - 2.2.5 Vérification du stockage des données dans MinIO
- 2.3 Lecture des tables Iceberg dans Dremio
  - 2.3.1 Démarrage de Dremio
  - 2.3.2 Connexion de Dremio au catalogue Nessie
  - 2.3.3 Interrogation des tables Iceberg dans Dremio
- 2.4 Création d'un tableau de bord BI à partir de vos tables Iceberg
  - 2.4.1 Démarrage d'Apache Superset
  - 2.4.2 Connexion de Superset à Dremio
  - 2.4.3 Création d'un jeu de données à partir des tables Iceberg
  - 2.4.4 Construction de graphiques et tableaux de bord
- 2.5 Résumé

## **PARTIE 2 : CONCEVOIR VOTRE ARCHITECTURE ICEBERG**

### **Chapitre 3 - PRÉPARER VOTRE PASSAGE À APACHE ICEBERG**
- 3.1 Réalisation de l'audit de votre plateforme de données
  - 3.1.1 Qui sont les parties prenantes ?
  - 3.1.2 Que devez-vous demander aux parties prenantes ?
  - 3.1.3 Réalisation d'un audit technologique
- 3.2 L'audit de la Banque Hamerliwa en action
  - 3.2.1 La Banque Hamerliwa interviewe ses parties prenantes
  - 3.2.2 La Banque Hamerliwa audite sa technologie
  - 3.2.3 La Banque Hamerliwa résume les résultats de son audit
- 3.3 De l'audit aux exigences : Poser les fondations de la conception
  - 3.3.1 Définition des exigences de stockage
  - 3.3.2 Définition des exigences d'ingestion
  - 3.3.3 Définition des exigences de catalogue
  - 3.3.4 Définition des exigences de fédération
  - 3.3.5 Définition des exigences de consommation
  - 3.3.6 La Banque Hamerliwa établit ses exigences
- 3.4 Plan architectural et présentation itinérante
  - 3.4.1 La Banque Hamerliwa crée son plan architectural
  - 3.4.2 La Banque Hamerliwa effectue une présentation itinérante
- 3.5 Résumé

### **Chapitre 4 - SÉLECTION DE LA COUCHE DE STOCKAGE**
- 4.1 Exigences de stockage
  - 4.1.1 Exigences de performance de récupération de fichiers
  - 4.1.2 Exigences de sécurité
  - 4.1.3 Exigences d'intégrité
  - 4.1.4 Exigences de coût et de surcharge opérationnelle
- 4.2 Stockage par blocs vs objet
  - 4.2.1 Stockage par blocs
  - 4.2.2 Stockage objet
- 4.3 Les standards dans la couche de stockage
  - 4.3.1 Apache Parquet
  - 4.3.2 L'API S3
- 4.4 Solutions de stockage
  - 4.4.1 Résumé de comparaison des fournisseurs
  - 4.4.2 Hadoop (HDFS)
  - 4.4.3 Amazon S3
  - 4.4.4 Google Cloud Storage
  - 4.4.5 Azure Blob Storage et ADLS
  - 4.4.6 MiniO
  - 4.4.7 Ceph
  - 4.4.8 NetApp StorageGRID
  - 4.4.9 Pure Storage
  - 4.4.10 Dell ECS
  - 4.4.11 Wasabi
- 4.5 Sélection basée sur les exigences
  - 4.5.1 Exigences de performance
  - 4.5.2 Exigences de sécurité
  - 4.5.3 Exigences d'intégrité
  - 4.5.4 Exigences de coût et opérationnelles
- 4.6 Résumé

### **Chapitre 5 - ARCHITECTURE DE LA COUCHE D'INGESTION**
- 5.1 Exigences d'ingestion
  - 5.1.1 Débit d'ingestion et latence
  - 5.1.2 Fiabilité et tolérance aux pannes
  - 5.1.3 Gestion et évolution du schéma
  - 5.1.4 Complexité opérationnelle et maintenabilité
- 5.2 Modèles et architectures d'ingestion
  - 5.2.1 Ingestion par lots
  - 5.2.2 Ingestion micro-batch et incrémentale
  - 5.2.3 Ingestion en streaming
- 5.3 Comment Iceberg gère les écritures
  - 5.3.1 Sémantique d'écriture dans Iceberg
  - 5.3.2 Protocoles de commit et gestion des conflits
- 5.4 Outils et frameworks pour l'ingestion
  - 5.4.1 Apache Spark
  - 5.4.2 Apache Flink
  - 5.4.3 Apache NiFi
  - 5.4.4 Fivetran
  - 5.4.5 Qlik
  - 5.4.6 Airbyte
  - 5.4.7 Confluent
  - 5.4.8 Redpanda
  - 5.4.9 Services d'ingestion cloud-native
  - 5.4.10 Considérations de sélection d'outils
- 5.5 Application des exigences d'ingestion en contexte
  - 5.5.1 Prioriser la faible latence
  - 5.5.2 Gérer le haut débit
  - 5.5.3 Prendre en charge les transformations complexes
  - 5.5.4 Gérer l'évolution du schéma
  - 5.5.5 Équilibrer la surcharge opérationnelle
  - 5.5.6 Considérer les environnements cloud existants
- 5.6 Résumé

### **Chapitre 6 - IMPLÉMENTATION DE LA COUCHE DE CATALOGUE**
- 6.1 Le rôle du catalogue dans les lakehouses Apache Iceberg
  - 6.1.1 Responsabilités du catalogue
  - 6.1.2 Interactions du catalogue avec les moteurs de requête et de traitement
- 6.2 Évaluation des exigences du catalogue
  - 6.2.1 Performance, disponibilité et échelle
  - 6.2.2 Gouvernance et traçabilité des métadonnées
  - 6.2.3 Sécurité et conformité
  - 6.2.4 Flexibilité de déploiement et compatibilité avec l'écosystème
  - 6.2.5 Coût et surcharge opérationnelle
  - 6.2.6 Fédération de catalogues et architectures mesh
- 6.3 Spécification Apache Iceberg REST Catalog
  - 6.3.1 Avant la spécification Apache Iceberg REST
  - 6.3.2 La solution
- 6.4 Options de catalogue : Exploration de l'écosystème
  - 6.4.1 Hadoop Catalog
  - 6.4.2 Hive Catalog
  - 6.4.3 JDBC Catalog
  - 6.4.4 Apache Polaris
  - 6.4.5 Project Nessie
  - 6.4.6 Apache Gravitino
  - 6.4.7 Lakekeeper
  - 6.4.8 AWS Glue Data Catalog
  - 6.4.9 Dremio Catalog
  - 6.4.10 Snowflake Open Catalog
  - 6.4.11 Databricks Unity Catalog
- 6.5 Choisir le bon catalogue : Évaluer les options à travers des scénarios
  - 6.5.1 Scénario : Une équipe de données de taille moyenne migrant depuis Hive
  - 6.5.2 Scénario : Une startup cloud-native en croissance rapide
  - 6.5.3 Scénario : Une entreprise multinationale avec une gouvernance stricte des données
  - 6.5.4 Scénario : Une startup SaaS priorisant la simplicité opérationnelle
  - 6.5.5 Scénario : Une grande entreprise avec des besoins multi-cloud et de gouvernance fédérée
  - 6.5.6 Scénario : Entreprise financière nécessitant un clonage quotidien d'environnement pour les tests de stress
  - 6.5.7 Scénario : Migration Iceberg progressive avec fédération de requêtes à travers les systèmes legacy
  - 6.5.8 Scénario : Adoption légère du lakehouse avec catalogue Hadoop et Python
- 6.6 Résumé

### **Chapitre 7 - CONCEPTION DE LA COUCHE DE FÉDÉRATION**
- 7.1 Ce qu'est la fédération de données et pourquoi elle compte
  - 7.1.1 Cas d'usage et défis courants motivant les besoins de fédération
  - 7.1.2 Comment la fédération s'aligne avec l'agilité et l'accessibilité
- 7.2 Exigences clés pour la fédération
  - 7.2.1 Prendre en charge des sources de données diverses sans duplication
  - 7.2.2 Assurer une sémantique et une logique métier cohérentes
  - 7.2.3 Fournir une connectivité transparente pour les outils d'analyse
  - 7.2.4 Introduction à Dremio et Trino
- 7.3 Dremio
  - 7.3.1 Architecture de Dremio
  - 7.3.2 Écosystème de connecteurs de Dremio et focus centré sur Iceberg
  - 7.3.3 Améliorations de performance de Dremio
- 7.4 Trino
  - 7.4.1 Architecture modulaire pour la prise en charge de nombreuses sources
  - 7.4.2 Flexibilité et configurabilité pour des environnements complexes
  - 7.4.3 Évolution dirigée par la communauté et extensions de fournisseurs
  - 7.4.4 Considérations de couche sémantique dans Trino
- 7.5 Modèles de déploiement
  - 7.5.1 Déploiement avec Dremio
  - 7.5.2 Déploiement avec Trino
- 7.6 Scénarios de décision de plateforme de fédération
  - 7.6.1 Environnement multi-sources fragmenté : Trino pour la largeur des connecteurs
  - 7.6.2 Construction d'un lakehouse Iceberg natif : Dremio pour les fonctionnalités Iceberg natives
  - 7.6.3 Autonomiser les utilisateurs métier avec l'interface utilisateur et les jeux de données gouvernés : Dremio
  - 7.6.4 Interrogation légère des jeux de données Hudi : Trino via AWS Athena
  - 7.6.5 Modernisation Cloudera on-prem : Trino remplaçant Impala pour les performances
  - 7.6.6 Stratégie Iceberg cloud hybride : Dremio reliant on-prem et ADLS
- 7.7 Alternatives de fédération
  - 7.7.1 Virtualisation via les raccourcis dans OneLake
  - 7.7.2 Virtualisation de données native IA avec Spice.ai
  - 7.7.3 Choisir la bonne solution
- 7.8 Résumé

### **Chapitre 8 - COMPRENDRE LA COUCHE DE CONSOMMATION**
- 8.1 Revenir sur les avantages du lakehouse pour la consommation
- 8.2 Connecter le lakehouse aux personnes
- 8.3 Revenir sur les exigences de notre audit
  - 8.3.1 Interprétation des exigences pour la consommation
  - 8.3.2 Exigences pour les outils BI
  - 8.3.3 Exigences pour les environnements de notebooks interactifs
  - 8.3.4 Exigences pour l'IA et les outils spécialisés de consommation de données
- 8.4 Interfaces ouvertes pour une consommation transparente
  - 8.4.1 JDBC et ODBC
  - 8.4.2 Arrow Flight
  - 8.4.3 Model Context Protocol (MCP)
- 8.5 Outils d'intelligence d'affaires dans le lakehouse
  - 8.5.1 Outils BI open source
  - 8.5.2 Outils BI commerciaux
- 8.6 Outils pour les charges de travail d'IA et d'apprentissage automatique
- 8.7 Choisir les bons outils de consommation : Dix scénarios illustrés
  - 8.7.1 Startup avec un focus data science
  - 8.7.2 Grande institution financière avec une gouvernance stricte
  - 8.7.3 Plateforme e-commerce de taille moyenne construisant des analyses intégrées
  - 8.7.4 Organisation média décentralisée permettant l'analyse en libre-service
  - 8.7.5 Agence gouvernementale équilibrant la transparence publique et le contrôle interne
  - 8.7.6 Fournisseur de soins de santé avec des contraintes de conformité et de localité des données
  - 8.7.7 Entreprise de logistique unifiant les opérations en temps réel et l'analyse historique
  - 8.7.8 Entreprise SaaS offrant un accès personnalisable aux données aux clients
  - 8.7.9 Organisation à but non lucratif soutenant la recherche collaborative
  - 8.7.10 Entreprise manufacturière permettant la maintenance prédictive
- 8.8 Résumé

## **PARTIE 3 : OPÉRER VOTRE LAKEHOUSE APACHE ICEBERG**

Voici la structure complète des **chapitres 9, 10, 11, 12, 13 et 14** du livre "Architecting an Apache Iceberg Lakehouse" par Alex Merced, avec les chapitres 11, 12, 13 et 14 basés sur le contenu du Livre Blanc sur le Streaming Lakehouse :[1]

## **Chapitre 9 - MAINTENIR UN LAKEHOUSE ICEBERG**

### 9.1 Problème : Fichiers de données sous-optimaux
- 9.1.1 Petits fichiers
- 9.1.2 Données mal colocalisées
- 9.1.3 Prolifération des métadonnées
- 9.1.4 Impacts de performance Merge-on-read (MOR)

### 9.2 Solution : Compaction
- 9.2.1 Qu'est-ce que la compaction ?
- 9.2.2 Taille de fichier cible
- 9.2.3 Fichiers à inclure
- 9.2.4 Utilisation de filtres pour délimiter la compaction

### 9.3 Gestion de l'empreinte de stockage et rétention des données
- 9.3.1 Exécution de l'expiration des snapshots
- 9.3.2 COW vs MOR : Implications pour la rétention des données
- 9.3.3 Considérations réglementaires pour la suppression des données

### 9.4 Exploration des tables de métadonnées d'Apache Iceberg

### 9.5 Contrôles d'accès dans un lakehouse Iceberg
- 9.5.1 Contrôles de la couche de stockage
- 9.5.2 Contrôles au niveau du catalogue
- 9.5.3 Contrôles d'accès au niveau du moteur

### 9.6 Résumé

***

## **Chapitre 10 - OPÉRATIONNALISER APACHE ICEBERG**

### 10.1 Orchestration du lakehouse
- 10.1.1 Choix des outils et modèles d'orchestration
- 10.1.2 Déclencheurs basés sur les métadonnées pour une maintenance proactive
- 10.1.3 Politiques de maintenance par table
- 10.1.4 Intégration de la surveillance et des alertes
- 10.1.5 Mise en pratique de l'orchestration

### 10.2 Audit du lakehouse
- 10.2.1 Tirer parti de l'historique des snapshots pour le suivi des changements
- 10.2.2 Utilisation du branchement et du marquage pour la gouvernance
- 10.2.3 Implémentation des politiques de rétention des fichiers et snapshots
- 10.2.4 Orchestration pratique des politiques de rétention
- 10.2.5 Suppression sécurisée des données
- 10.2.6 Audit d'accès et gouvernance
- 10.2.7 Audit pratique avec Iceberg : Exemples de flux de travail

### 10.3 Récupération après sinistre dans le lakehouse
- 10.3.1 Le rôle du catalogue de métadonnées dans la récupération après sinistre
- 10.3.2 Protection contre la perte et la corruption des données
- 10.3.3 Récupération multi-région et multi-environnement
- 10.3.4 Retour en arrière et voyage dans le temps dans la réponse aux incidents
- 10.3.5 Automatisation des procédures de récupération après sinistre
- 10.3.6 Validation de la préparation à la récupération
- 10.3.7 Récupération après sinistre par automatisation
- 10.3.8 Exemples pratiques : Automatisation des flux de travail de récupération

### 10.4 Résumé

***

## **Chapitre 11 - L'ÉVOLUTION VERS LE STREAMING LAKEHOUSE**

### 11.1 De l'Architecture Lambda au Streaming Lakehouse
- 11.1.1 Les limites de l'Architecture Lambda
  - 11.1.1.1 La couche de vitesse (Speed Layer)
  - 11.1.1.2 La couche de lot (Batch Layer)
  - 11.1.1.3 Complexité opérationnelle et divergence des données
- 11.1.2 L'avènement de l'Architecture Kappa
  - 11.1.2.1 Traitement unifié par flux
  - 11.1.2.2 Limitations des moteurs de streaming purs
- 11.1.3 Le Streaming Lakehouse : La Synthèse
  - 11.1.3.1 Ingestion en temps réel
  - 11.1.3.2 Correction transactionnelle avec propriétés ACID
  - 11.1.3.3 Unification du stockage

### 11.2 Le Rôle de Confluent et Kafka dans l'Écosystème Moderne
- 11.2.1 Kafka comme système nerveux central
- 11.2.2 Plateforme de traitement et de gouvernance des données en mouvement
- 11.2.3 Cas d'usage : Transformation architecturale des institutions financières
  - 11.2.3.1 Banque Royale du Canada (RBC) : Passage du mainframe à l'architecture événementielle
  - 11.2.3.2 Réduction de la latence de détection des anomalies
- 11.2.4 Découplage des systèmes producteurs et consommateurs
- 11.2.5 Exemple Shopify : Traitement de milliards d'événements quotidiens

### 11.3 Résumé

***

## **Chapitre 12 - L'INTÉGRATION AVEC MICROSOFT FABRIC ET POWER BI**

### 12.1 OneLake Shortcuts et Virtualisation
- 12.1.1 Concept de Shortcuts dans OneLake
  - 12.1.1.1 Montage de tables Iceberg externes sans copie de données
  - 12.1.1.2 Support des sources S3 et ADLS générées par Confluent/Snowflake
- 12.1.2 Virtualisation Bidirectionnelle
  - 12.1.2.1 Couche de traduction de métadonnées basée sur Apache XTable
  - 12.1.2.2 Mapping dynamique des métadonnées Iceberg vers Delta Lake
  - 12.1.2.3 Accessibilité via moteurs Spark de Fabric et SQL Endpoint
- 12.1.3 Contraintes et considérations
  - 12.1.3.1 Contrainte de région : alignement géographique requis
  - 12.1.3.2 Impact sur les coûts d'egress et les performances
  - 12.1.3.3 Cas spécifique : banques canadiennes et région Canada Central

### 12.2 Power BI Direct Lake : Latence et Performance
- 12.2.1 Le mode Direct Lake comme rupture technologique
  - 12.2.1.1 Comparaison avec le mode Import et DirectQuery
  - 12.2.1.2 Lecture directe des fichiers Parquet par le moteur VertiPaq
- 12.2.2 Impact et capacités
  - 12.2.2.1 Visualisation de volumes massifs (Pétaoctets)
  - 12.2.2.2 Performances interactives proches du mode Import
- 12.2.3 Latence de synchronisation
  - 12.2.3.1 Processus de synchronisation Kafka → Iceberg → OneLake → Power BI
  - 12.2.3.2 Variation de latence selon la configuration de cache
  - 12.2.3.3 Considérations pour tableaux de bord opérationnels temps réel

### 12.3 Résumé

***

## **Chapitre 13 - CONTEXTE CANADIEN ET ÉTUDES DE CAS**

### 13.1 Introduction au contexte canadien
- 13.1.1 Souveraineté numérique et modernisation des infrastructures
- 13.1.2 Influence sur l'adoption des technologies de Streaming Lakehouse

### 13.2 Étude de Cas : Banque Royale du Canada (RBC)
- 13.2.1 Contexte et défis initiaux
  - 13.2.1.1 Dépendance aux mainframes coûteux (MIPS)
  - 13.2.1.2 Difficulté à innover sur des données cloisonnées
- 13.2.2 Solution architecturale
  - 13.2.2.1 Utilisation de Kafka pour "découper le monolithe" (Monolith Slicing)
  - 13.2.2.2 Capture en temps réel des transactions
  - 13.2.2.3 Diffusion vers applications aval sans re-solliciter le mainframe
- 13.2.3 Résultats et bénéfices
  - 13.2.3.1 Réduction drastique des coûts MIPS
  - 13.2.3.2 Accélération de la détection de fraude (de plusieurs semaines à quelques secondes)
  - 13.2.3.3 Historisation avec Iceberg pour l'entraînement de modèles IA
  - 13.2.3.4 Données souveraines hébergées au Canada

### 13.3 Étude de Cas : Bell Canada
- 13.3.1 Contexte et défis
  - 13.3.1.1 Volumes massifs de logs hétérogènes
  - 13.3.1.2 Sources multiples : routeurs, box, antennes
- 13.3.2 Solution mise en place
  - 13.3.2.1 Ingestion via Kafka
  - 13.3.2.2 Normalisation des logs
  - 13.3.2.3 Passage à une architecture Lakehouse
- 13.3.3 Bénéfices opérationnels
  - 13.3.3.1 Conservation à long terme à faible coût (conformité légale)
  - 13.3.3.2 Stockage objet économique
  - 13.3.3.3 Requêtes SQL rapides pour investigation d'incidents de sécurité
  - 13.3.3.4 Support du SOC (Security Operations Center)

### 13.4 Souveraineté des Données et Infrastructure Régionale
- 13.4.1 Conformité et directives fédérales
  - 13.4.1.1 Stratégie infonuagique du gouvernement du Canada
  - 13.4.1.2 Exigences de résidence des données au pays
- 13.4.2 Comparaison régionale : AWS Canada vs US East
  - 13.4.2.1 AWS Canada Central (ca-central-1) vs US East (N. Virginia)
  - 13.4.2.2 Coûts et considérations financières (+10-15% pour la région canadienne)
  - 13.4.2.3 Déploiement de services de pointe
  - 13.4.2.4 Mandat pour données PII bancaires et gouvernementales
- 13.4.3 Analyse de latence
  - 13.4.3.1 Latence réseau pour utilisateurs basés à Toronto/Montréal
  - 13.4.3.2 Comparaison ca-central-1 (<10ms) vs Virginie (~20-30ms)
  - 13.4.3.3 Impact sur applications interactives Power BI Direct Lake

### 13.5 Résumé

***

## **Chapitre 14 - CONCLUSION ET PERSPECTIVES 2026**

### 14.1 L'architecture de Streaming Lakehouse comme état de l'art
- 14.1.1 Unification de Kafka, Iceberg et Fabric
- 14.1.2 Concilier l'agilité du temps réel avec la rigueur de l'analytique transactionnelle
- 14.1.3 Positionnement en 2025 dans la gestion de données moderne

### 14.2 Perspectives technologiques pour 2026
- 14.2.1 L'émergence du "Diskless Kafka"
  - 14.2.1.1 Kafka utilisant Iceberg/S3 comme stockage primaire
  - 14.2.1.2 Élimination de la duplication sur disques locaux
  - 14.2.1.3 Impact sur l'architecture et les performances
- 14.2.2 Standardisation des catalogues via le protocole REST
  - 14.2.2.1 Avantages de la standardisation
  - 14.2.2.2 Interopérabilité accrue entre systèmes

### 14.3 Implications stratégiques pour les organisations canadiennes
- 14.3.1 Investissement technologique comme décision stratégique
- 14.3.2 Bénéfices organisationnels
  - 14.3.2.1 Innovation et compétitivité
  - 14.3.2.2 Conformité réglementaire
  - 14.3.2.3 Adaptation à une économie numérique accélérée
- 14.3.3 Recommandations pour l'adoption

### 14.4 Résumé final

## **ANNEXE A : LES TABLES DE MÉTADONNÉES**

### A.1 Interrogation des tables de métadonnées Iceberg

### A.2 La table de métadonnées history

### A.3 La table de métadonnées snapshots

### A.4 La table de métadonnées metadata_log_entries

### A.5 La table de métadonnées manifests

### A.6 La table de métadonnées partitions

### A.7 La table de métadonnées files

### A.8 La table de métadonnées manifests

### A.9 La table de métadonnées partitions

### A.10 La table de métadonnées position_deletes

### A.11 La table de métadonnées all_data_files

### A.12 La table de métadonnées all_delete_files

### A.13 La table de métadonnées all_entries

### A.14 La table de métadonnées all_manifests

### A.15 La table de métadonnées refs

### A.16 Surveillance de la santé des tables avec les tables de métadonnées

***

## **ANNEXE B : PYTHON POUR APACHE ICEBERG**

### B.1 PyIceberg

### B.2 Polars

### B.3 DuckDB

### B.4 Daft

### B.5 Dremio

### B.6 Bauplan

### B.7 SpiceAI

### B.8 Résumé et meilleures pratiques

***

## **ANNEXE C : LA SPÉCIFICATION APACHE ICEBERG**

### C.1 Comprendre la spécification Iceberg
- C.1.1 Qu'est-ce qu'une spécification de format de table ?
- C.1.2 Pourquoi Iceberg formalise le comportement des tables
- C.1.3 Évolution de la spécification : principes de versionnement et compatibilité

### C.2 Versions du format de table Iceberg
- C.2.1 Version 1 : Fondation pour les tables analytiques
- C.2.2 Version 2 : Suppressions au niveau des lignes et écritures plus strictes
- C.2.3 Version 3 : Types étendus et capacités avancées
- C.2.4 Version 4 : Performance, portabilité et préparation au temps réel

### C.3 Gestion des snapshots et métadonnées de table
- C.3.1 Fichiers de métadonnées de table
- C.3.2 Snapshots et la liste des manifestes
- C.3.3 Numéros de séquence et concurrence optimiste

### C.4 La spécification REST Catalog
- C.4.1 Aperçu et objectif
- C.4.2 Configuration du catalogue et points de terminaison par défaut
- C.4.3 Espaces de noms, tables et vues
- C.4.4 Enregistrement des tables, métriques et transactions
- C.4.5 Prise en charge OAuth2 et considérations de sécurité
- C.4.6 Le point de terminaison de planification de scan

### C.5 Spécification du format de fichier Puffin
- C.5.1 Qu'est-ce qu'un fichier Puffin ?
- C.5.2 Stockage des métriques au niveau des colonnes et index personnalisés
- C.5.3 Intégration avec les métadonnées de table Iceberg

### C.6 Compatibilité et migration
- C.6.1 Lecture et écriture à travers les versions de format
- C.6.2 Mise à niveau des tables vers des versions plus récentes de la spécification
- C.6.3 Gestion de la compatibilité descendante en pratique
