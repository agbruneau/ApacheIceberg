# Apache Kafka — Découvrir la plateforme événementielle

---

### **INTRODUCTION - PLATEFORME STRATÉGIQUE**

- I.1 Fondations de Kafka : Au-delà du Bus de Messages
- I.2 Analyse des Patrons d'Architecture Stratégiques
  - I.2.1 Communication entre Microservices via la Chorégraphie
  - I.2.2 CQRS (Command Query Responsibility Segregation)
  - I.2.3 Event Sourcing
  - I.2.4 Data Mesh (Maillage de Données)
- I.3 Cadre de Décision pour les Modèles de Déploiement
  - I.3.1 L'Arbitrage Fondamental : Auto-hébergé vs. Service Géré
  - I.3.2 Panorama des Services Gérés dans le Cloud
  - I.3.3 La Transition Stratégique : de ZooKeeper à KRaft
- I.4 Cadre d'Aide à la Décision Stratégique
  - I.4.1 Archétype 1 : Pipelines de Données à Haut Débit
  - I.4.2 Archétype 2 : Microservices Critiques
  - I.4.3 Archétype 3 : Plateforme de Données Analytiques d'Entreprise
- I.5 Kafka comme Catalyseur de l'Entreprise en Temps Réel
- I.6 Résumé

### **Chapitre 1 - DÉCOUVRIR KAFKA EN TANT QU’ARCHITECTE**

- 1.1 La perspective de l'architecte sur Kafka
  - 1.1.1 Architecture événementielle
  - 1.1.2 Gestion d'une myriade de données
- 1.2 Notes de terrain : Parcours d'un projet événementiel
- 1.3 Acteurs clés de l'écosystème Kafka
  - 1.3.1 Brokers et clients
  - 1.3.2 Gestion des métadonnées du cluster
- 1.4 Principes d'architecture
  - 1.4.1 Le patron Publication-Abonnement (Publish-Subscribe)
  - 1.4.2 Livraison fiable
- 1.5 Le journal des transactions (commit log)
  - 1.5.1 Conception et gestion des flux de données
  - 1.5.2 Schema Registry : gestion des contrats de données
  - 1.5.3 Kafka Connect : réplication de données sans code
  - 1.5.4 Transformation des données (streaming frameworks)
- 1.6 Impact sur les opérations et l'infrastructure
- 1.7 Application de Kafka en entreprise
- 1.8 Notes de terrain : Démarrer avec un projet Kafka
- 1.9 Résumé

### **Chapitre 2 - ARCHITECTURE D'UN CLUSTER KAFKA**

- 2.1 L'Unité Fondamentale : Anatomie d'un Message Kafka
- 2.2 Organisation Logique : Topics, Partitions et Stratégies de Partitionnement
- 2.3 Représentation Physique : Segments de Log et Indexation
- 2.4 Durabilité et Haute Disponibilité : Le Modèle de Réplication
- 2.5 Gestion du Cycle de Vie des Données : Rétention et Compactage
- 2.6 Recommandations Architecturales et Bonnes Pratiques
- 2.7 Résumé

### **Chapitre 3 - CLIENTS KAFKA ET PRODUCTION DE MESSAGES**

- 3.1 L'Anatomie d'un Producer Kafka
- 3.2 Garanties Fondamentales de Production : Fiabilité et Cohérence des Données
- 3.3 Stratégies de Partitionnement et Ordonnancement des Messages
- 3.4 Sérialisation des Données et Gestion des Schémas
- 3.5 Optimisation des Performances et Gestion des Ressources
- 3.6 Recommandations Architecturales pour les Producers
- 3.7 Résumé

### **Chapitre 4 - CRÉATION D'APPLICATIONS CONSOMMATRICES**

- 4.1 Consommateur Kafka : architecture et principes fondamentaux
- 4.2 Atteindre le parallélisme : groupes de consommateurs et scalabilité
- 4.3 Maîtriser le rééquilibrage des consommateurs
- 4.4 Modèles de conception fondamentaux pour la consommation de données
- 4.5 Stratégies de consommation avancées
- 4.6 Réglage des performances : équilibrer débit et latence
- 4.7 Construire des consommateurs résilients et prêts pour l'exploitation
- 4.8 Résumé

### **Chapitre 5 - CAS D’UTILISATION KAFKA**

- 5.1 Quand choisir Kafka — et quand ne pas le faire
- 5.2 Naviguer dans l'implémentation en contexte réel
  - 5.2.1 Microservices événementiels
  - 5.2.2 Intégration de données
  - 5.2.3 Collecte de journaux (logs)
  - 5.2.4 Traitement de données en temps réel
- 5.3 Différences avec d'autres plateformes de messagerie
- 5.4 Alternatives à Kafka
- 5.5 Résumé

### **Chapitre 6 - CONTRATS DE DONNÉES**

- 6.1 Traduire les produits d'affaires en schémas
- 6.2 Comment Kafka gère la structure des événements
- 6.3 Défis dans la conception d'événements
- 6.4 Structure de l'événement et mapping
- 6.5 Notes de terrain : Stratégies de données pour le projet Customer360
- 6.6 Schema Registry dans l'écosystème Kafka
- 6.7 Problèmes courants dans la gestion des contrats de données
- 6.8 Résumé

### **Chapitre 7 - PATRONS D’INTERACTION KAFKA**

- 7.1 Notes de terrain : Utiliser Kafka ou non : les cas problématiques
- 7.2 Implémentation d'un maillage de données (data mesh)
- 7.3 Utilisation de Kafka Connect
- 7.4 Assurer la garantie de livraison
- 7.5 Résumé

### **Chapitre 8 - CONCEPTION D’APPLICATION DE TRAITEMENT DE FLUX EN CONTINU**

- 8.1 L'Ère du Temps Réel : Du Traitement par Lots au Traitement en Flux
- 8.2 Introduction à Kafka Streams : Une Bibliothèque pour le Traitement en Flux
- 8.3 Architecture et Concepts Clés de Kafka Streams
- 8.4 Développement d'Applications : Des Opérations Simples aux Logiques Complexes
- 8.5 Gestion de l'État, Cohérence et Tolérance aux Pannes
- 8.6 Positionnement dans l'Écosystème du Traitement de Données
- 8.7 Considérations Opérationnelles et Bonnes Pratiques pour la Production
- 8.8 Cas d'Usage Architectural : Construction d'une Vue Client 360 en Temps Réel
- 8.9 Résumé

### **Chapitre 9 - GESTION KAFKA D’ENTREPRISE**

- 9.1 Stratégies de Déploiement et Modèles d'Architecture
- 9.2 Dimensionnement et Scalabilité du Cluster
- 9.3 Optimisation des Performances et Monitoring
- 9.4 Sécurité de Niveau Entreprise
- 9.5 Gouvernance Opérationnelle et Gestion du Cycle de Vie
- 9.6 Plan de Reprise d'Activité (PRA) et Haute Disponibilité
- 9.7 Résumé

### **Chapitre 10 - ORGANISATION D’UN PROJET KAFKA**

- 10.1 Définition des exigences d'un projet Kafka
- 10.2 Maintenir la structure du cluster : Outils, GitOps et environnements
- 10.3 Tester les applications Kafka
- 10.4 Résumé

### **Chapitre 11 - OPÉRER KAFKA**

- 11.1 Évolution et Mises à Niveau du Cluster
- 11.2 Mobilité des Données
- 11.3 Surveillance du Cluster Kafka
- 11.4 Clinique d'Optimisation des Performances
- 11.5 Reprise Après Sinistre et Basculement (Failover)
- 11.6 Résumé

### **Chapitre 12 - AVENIR KAFKA**

- 12.1 Les origines de Kafka : vers une dorsale événementielle
- 12.2 Kafka comme plateforme d'orchestration
- 12.3 Kafka sans serveur (Serverless) et sans disque
- 12.4 Kafka dans le monde de l'IA/AA
- 12.5 Kafka et les agents d'IA
- 12.6 Résumé
