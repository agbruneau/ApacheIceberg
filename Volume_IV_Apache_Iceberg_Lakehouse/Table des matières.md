# VOLUME IV : APACHE ICEBERG - LE LAKEHOUSE MODERNE

_Architecture, Conception et Opérations du Data Lakehouse_

---

## PARTIE 1 : LA VALEUR DU LAKEHOUSE

### **Chapitre IV.1 - LE MONDE DU LAKEHOUSE APACHE ICEBERG**

- IV.1.1 Qu'est-ce qu'un data lakehouse
- IV.1.2 Qu'est-ce qu'Apache Iceberg ?
- IV.1.3 Les avantages d'Apache Iceberg
- IV.1.4 Les composants d'un lakehouse Apache Iceberg
- IV.1.5 Résumé

### **Chapitre IV.2 - ANATOMIE TECHNIQUE D'APACHE ICEBERG**

- IV.2.1 Hiérarchie des fichiers et gestion des métadonnées
- IV.2.2 Stratégies d'écriture : Copy-on-Write vs Merge-on-Read
- IV.2.3 Gestion de l'évolution de schéma
- IV.2.4 Partitionnement masqué (Hidden Partitioning)
- IV.2.5 Résumé

### **Chapitre IV.3 - MISE EN PRATIQUE AVEC APACHE ICEBERG**

- IV.3.1 Configuration d'un environnement Apache Iceberg
- IV.3.2 Création de tables Iceberg dans Spark
- IV.3.3 Lecture des tables Iceberg dans Dremio
- IV.3.4 Création d'un tableau de bord BI
- IV.3.5 Résumé

---

## PARTIE 2 : CONCEVOIR VOTRE ARCHITECTURE

### **Chapitre IV.4 - PRÉPARER VOTRE PASSAGE À APACHE ICEBERG**

- IV.4.1 Réalisation de l'audit de votre plateforme
- IV.4.2 L'audit de la Banque Hamerliwa en action
- IV.4.3 De l'audit aux exigences
- IV.4.4 Plan architectural et présentation itinérante
- IV.4.5 Résumé

### **Chapitre IV.5 - SÉLECTION DE LA COUCHE DE STOCKAGE**

- IV.5.1 Exigences de stockage
- IV.5.2 Stockage par blocs vs objet
- IV.5.3 Les standards dans la couche de stockage
- IV.5.4 Solutions de stockage
- IV.5.5 Sélection basée sur les exigences
- IV.5.6 Résumé

### **Chapitre IV.6 - ARCHITECTURE DE LA COUCHE D'INGESTION**

- IV.6.1 Exigences d'ingestion
- IV.6.2 Modèles et architectures d'ingestion
- IV.6.3 Comment Iceberg gère les écritures
- IV.6.4 Patterns d'ingestion Kafka vers Iceberg
- IV.6.5 Intégration avec Kafka Schema Registry
- IV.6.6 Outils et frameworks pour l'ingestion
- IV.6.7 Application des exigences en contexte
- IV.6.8 Résumé

### **Chapitre IV.7 - IMPLÉMENTATION DE LA COUCHE DE CATALOGUE**

- IV.7.1 Le rôle du catalogue dans les lakehouses
- IV.7.2 Évaluation des exigences du catalogue
- IV.7.3 Spécification Apache Iceberg REST Catalog
- IV.7.4 Options de catalogue
- IV.7.5 Choisir le bon catalogue
- IV.7.6 Résumé

### **Chapitre IV.8 - CONCEPTION DE LA COUCHE DE FÉDÉRATION**

- IV.8.1 Ce qu'est la fédération de données
- IV.8.2 Exigences clés pour la fédération
- IV.8.3 Dremio
- IV.8.4 Trino
- IV.8.5 Modèles de déploiement
- IV.8.6 Scénarios de décision
- IV.8.7 Alternatives de fédération
- IV.8.8 Résumé

### **Chapitre IV.9 - COMPRENDRE LA COUCHE DE CONSOMMATION**

- IV.9.1 Revenir sur les avantages du lakehouse
- IV.9.2 Connecter le lakehouse aux personnes
- IV.9.3 Revenir sur les exigences de l'audit
- IV.9.4 Interfaces ouvertes pour une consommation transparente
- IV.9.5 Outils d'intelligence d'affaires
- IV.9.6 Outils pour l'IA et l'apprentissage automatique
- IV.9.7 Choisir les bons outils de consommation
- IV.9.8 Résumé

---

## PARTIE 3 : OPÉRER VOTRE LAKEHOUSE

### **Chapitre IV.10 - MAINTENIR UN LAKEHOUSE ICEBERG EN PRODUCTION**

- IV.10.1 Problème : Fichiers de données sous-optimaux
- IV.10.2 Solution : Compaction
- IV.10.3 Gestion de l'empreinte de stockage
- IV.10.4 Exploration des tables de métadonnées
- IV.10.5 Contrôles d'accès dans un lakehouse
- IV.10.6 Résumé

### **Chapitre IV.11 - OPÉRATIONNALISER APACHE ICEBERG**

- IV.11.1 Orchestration du lakehouse
- IV.11.2 Audit du lakehouse
- IV.11.3 Récupération après sinistre
- IV.11.4 Résumé

### **Chapitre IV.12 - L'ÉVOLUTION VERS LE STREAMING LAKEHOUSE**

- IV.12.1 De l'Architecture Lambda au Streaming Lakehouse
- IV.12.2 Le Rôle de Confluent et Kafka
- IV.12.3 Résumé

### **Chapitre IV.13 - SÉCURITÉ, GOUVERNANCE ET CONFORMITÉ DU LAKEHOUSE**

- IV.13.1 Fondements de la sécurité
- IV.13.2 Gouvernance des données à l'échelle entreprise
- IV.13.3 Conformité réglementaire (RGPD, Loi 25)
- IV.13.4 Contrôles d'accès avancés
- IV.13.5 Patterns d'architecture sécurisée
- IV.13.6 Résumé

---

## PARTIE 4 : INTÉGRATIONS ET PERSPECTIVES

### **Chapitre IV.14 - L'INTÉGRATION AVEC MICROSOFT FABRIC ET POWER BI**

- IV.14.1 OneLake Shortcuts et Virtualisation
- IV.14.2 Power BI Direct Lake : Latence et Performance
- IV.14.3 Résumé

### **Chapitre IV.15 - CONTEXTE CANADIEN ET ÉTUDES DE CAS**

- IV.15.1 Introduction au contexte canadien
- IV.15.2 Étude de Cas : Banque Royale du Canada (RBC)
- IV.15.3 Étude de Cas : Bell Canada
- IV.15.4 Souveraineté des Données et Infrastructure Régionale
- IV.15.5 Résumé

### **Chapitre IV.16 - CONCLUSION FINALE ET PERSPECTIVES 2026-2030**

- IV.16.1 L'architecture de Streaming Lakehouse comme état de l'art
- IV.16.2 Perspectives technologiques 2026-2028
- IV.16.3 Horizons 2028-2030 : L'ère de l'IA
- IV.16.4 Implications stratégiques pour les organisations canadiennes
- IV.16.5 Résumé final et appel à l'action

---

## ANNEXES DU VOLUME IV

### **Annexe A - LA SPÉCIFICATION APACHE ICEBERG**

- A.1 Comprendre la spécification Iceberg
- A.2 Versions du format de table Iceberg
- A.3 Gestion des snapshots et métadonnées
- A.4 La spécification REST Catalog
- A.5 Spécification du format de fichier Puffin
- A.6 Compatibilité et migration

### **Annexe B - GLOSSAIRE**

- B.1 Terminologie Apache Iceberg
- B.2 Terminologie Lakehouse et Data Engineering
- B.3 Terminologie Streaming et Kafka
- B.4 Acronymes et abréviations

---

## Résumé du Volume IV

| Partie    | Titre                        | Chapitres  |
| --------- | ---------------------------- | ---------- |
| 1         | La Valeur du Lakehouse       | 3          |
| 2         | Concevoir Votre Architecture | 6          |
| 3         | Opérer Votre Lakehouse       | 4          |
| 4         | Intégrations et Perspectives | 3          |
| Annexes   | -                            | 2          |
| **Total** | -                            | **16 + 2** |
