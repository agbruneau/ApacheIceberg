# Prompt pour le Chapitre 2 : Anatomie Technique d'Apache Iceberg

## 1. Rôle et Objectif

Tu rédiges le Chapitre 2 : ANATOMIE TECHNIQUE D'APACHE ICEBERG. C'est le chapitre le plus technique sur les internes ("Deep Dive"). Il doit permettre à un architecte de comprendre exactement ce qui se passe sur le disque.

## 2. Contexte Global

- **Public :** Architectes de Solutions et Data Engineers Principaux.
- **Ton :** Expert, précis, technique.
- **Contexte technologique :** Focus sur la structure de fichiers et les mécanismes d'écriture.

## 3. Contenu Spécifique à Traiter (Scope)

- **2.1 Hiérarchie des fichiers :** metadata.json, Manifest List, Manifest Files, Data Files (Parquet/ORC/Avro), Isolation ACID.
- **2.2 Stratégies d'écriture (CRITIQUE) :** Comparaison détaillée Copy-on-Write (CoW) vs Merge-on-Read (MoR). Matrice décisionnelle, impact latence/lecture.
- **2.3 Gestion de l'évolution de schéma :** Column IDs vs noms, compatibilité historique.
- **2.4 Partitionnement masqué :** Concept, transformations (bucket, truncate, etc.), élagage (pruning).
- **2.5 Résumé.**

## 4. Directives de Recherche Profonde (Deep Research)

- Cherche les spécifications techniques (Iceberg Spec v2/v3) concernant les formats de fichiers.
- Trouve des benchmarks de performance comparant CoW et MoR sur des workloads d'ingestion et de lecture.

## 5. Directives de Formatage

- Utilise le format Markdown.
- **Obligatoire :** Un diagramme Mermaid complexe montrant la hiérarchie des métadonnées (Pointeurs du catalogue -> Metadata.json -> Manifest List -> Manifest -> Data).
- Tableau comparatif strict : Copy-on-Write vs Merge-on-Read (Cas d'usage, Avantages, Inconvénients).
