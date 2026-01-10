# Prompt pour le Chapitre 8 : Conception de la Couche de Fédération

## 1. Rôle et Objectif

Tu rédiges le Chapitre 8 : CONCEPTION DE LA COUCHE DE FÉDÉRATION. Comparaison et architecture des moteurs de requête (Dremio/Trino).

## 2. Contexte Global

- **Contexte technologique :** Dremio et Trino comme piliers. Intégration MS Fabric/OneLake.

## 3. Contenu Spécifique à Traiter (Scope)

- **8.1 La fédération :** Pourquoi ? (Éviter la duplication, agilité).
- **8.2 Exigences :** Sources diverses, sémantique, connectivité.
- **8.3 Dremio :** Architecture, Focus Iceberg natif, "Data Reflections".
- **8.4 Trino :** Architecture modulaire, flexibilité, connecteurs.
- **8.5 Modèles de déploiement.**
- **8.6 Scénarios de décision :** Fragmenté (Trino), Lakehouse natif (Dremio), Business User Focus (Dremio UI), Hudi/Legacy (Trino), Hybride.
- **8.7 Alternatives :** Raccourcis OneLake (Microsoft), Spice.ai.
- **8.8 Résumé.**

## 4. Directives de Recherche Profonde

- Trouve des benchmarks de performance récents Dremio vs Trino sur Iceberg.
- Cherche les limitations actuelles des raccourcis OneLake (Shortcuts) pour les tables Iceberg externes.

## 5. Directives de Formatage

- Utilise le format Markdown.
- Tableau "Dremio vs Trino" (Performance, Facilité d'usage, Écosystème, Support Iceberg).
