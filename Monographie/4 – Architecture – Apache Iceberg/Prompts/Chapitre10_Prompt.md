# Prompt pour le Chapitre 10 : Maintenir un Lakehouse Iceberg en Production

## 1. Rôle et Objectif

Tu rédiges le Chapitre 10 : MAINTENIR UN LAKEHOUSE ICEBERG EN PRODUCTION. Chapitre opérationnel critique sur la maintenance des données.

## 2. Contexte Global

- **Contexte géographique :** Application de la **Loi 25** (Québec) et RGPD.

## 3. Contenu Spécifique à Traiter (Scope)

- **10.1 Problèmes :** Petits fichiers, métadonnées excessives, performance MOR.
- **10.2 Compaction :** Bin-Packing, Sort, Z-Order (multidimensionnel). Paramètres, sélection, fréquence.
- **10.3 Rétention et Suppression :** Expiration snapshots, Droit à l'oubli (Loi 25/RGPD), procédure remove_orphan_files.
- **10.4 Tables de métadonnées :** Inspection, diagnostics, monitoring.
- **10.5 Contrôles d'accès :** Stockage, Catalogue, Moteur.
- **10.6 Résumé.**

## 4. Directives de Recherche Profonde

- Recherche les implications techniques exactes du "Droit à l'oubli" sur des formats immutables comme Iceberg (méthode de suppression avec compaction forcée).
- Trouve des recommandations de taille de fichier cible pour S3 vs HDFS.

## 5. Directives de Formatage

- Utilise le format Markdown.
- Code snippet : Procédure Spark SQL pour lancer une compaction Z-Order.
- Code snippet : Procédure de maintenance complète (expire_snapshots + remove_orphan_files).
