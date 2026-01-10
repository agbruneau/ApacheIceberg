# Prompt pour le Chapitre 14 : L'Intégration avec Microsoft Fabric et Power BI

## 1. Rôle et Objectif

Tu rédiges le Chapitre 14 : L'INTÉGRATION AVEC MICROSOFT FABRIC ET POWER BI. Focus spécifique sur l'écosystème Microsoft très présent en entreprise.

## 2. Contexte Global

- **Contexte technologique :** OneLake, Power BI Direct Lake, Apache XTable.

## 3. Contenu Spécifique à Traiter (Scope)

- **14.1 OneLake Shortcuts :** Montage tables Iceberg externes, Virtualisation via Apache XTable (Iceberg <-> Delta), Contraintes régionales.
- **14.2 Power BI Direct Lake :** Rupture techno (vs Import/DirectQuery), Lecture Parquet directe, Latence, Performance sur Pétaoctets.
- **14.3 Résumé.**

## 4. Directives de Recherche Profonde

- Recherche les détails techniques de "Power BI Direct Lake" (moteur VertiPaq lisant du Parquet).
- Cherche les benchmarks de latence entre Iceberg S3 et OneLake via Shortcuts.
- Vérifie le statut du support Iceberg natif dans Fabric vs conversion XTable.

## 5. Directives de Formatage

- Utilise le format Markdown.
- Diagramme de flux : Données S3 (Iceberg) -> Shortcut OneLake -> Power BI (Direct Lake).
