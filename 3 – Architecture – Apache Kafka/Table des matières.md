Titre : Apache Kafka - Découvrir la plateforme événementielle
Table des matières
Introduction : Plateforme Stratégique 1
I.2. Fondations de Kafka : Au-delà du Bus de Messages 1
I.3. Analyse des Patrons d'Architecture Stratégiques 2
I.3.1 Communication entre Microservices via la Chorégraphie 2
I.3.2 CQRS (Command Query Responsibility Segregation) 3
I.3.3 Event Sourcing 3
I.3.4 Data Mesh (Maillage de Données) 3
I.4. Cadre de Décision pour les Modèles de Déploiement 4
I.4.1 L'Arbitrage Fondamental : Auto-hébergé vs. Service Géré 4
I.4.2 Panorama des Services Gérés dans le Cloud 5
I.4.3 La Transition Stratégique : de ZooKeeper à KRaft 5
I.5. Cadre d'Aide à la Décision Stratégique 5
Archétype 1 : Pipelines de Données à Haut Débit (Agrégation de Logs, IoT) 6
Archétype 2 : Microservices Critiques (Commandes, Paiements) 6
Archétype 3 : Plateforme de Données Analytiques d'Entreprise 6
I.6. Kafka comme Catalyseur de l'Entreprise en Temps Réel 7
Chapitre 1 : Découvrir Kafka en tant qu’architecte 15
1.1 La perspective de l'architecte sur Kafka 15
1.1.1 Architecture événementielle 15
1.1.2 Gestion d'une myriade de données 16
1.2 Notes de terrain : Parcours d'un projet événementiel 16
1.3 Acteurs clés de l'écosystème Kafka 17
1.3.1 Brokers et clients 17
1.3.2 Gestion des métadonnées du cluster 18
1.4 Principes d'architecture 20
1.4.1 Le patron Publication-Abonnement (Publish-Subscribe) 20
1.4.2 Livraison fiable 20
1.5 Le journal des transactions (commit log) 22
1.5.1 Conception et gestion des flux de données 22
1.5.2 Schema Registry : gestion des contrats de données 22
1.5.3 Kafka Connect : réplication de données sans code 23
1.5.4 Transformation des données (streaming frameworks) 23
1.6 Impact sur les opérations et l'infrastructure 25
1.6.1 Optimisation et maintenance de Kafka 25
1.6.2 Options sur site (on-premise) et infonuagiques (cloud) 25
1.6.3 Solutions d'autres fournisseurs infonuagiques 26
1.7 Application de Kafka en entreprise 27
1.7.1 Utilisation de Kafka pour le stockage de messages 27
1.7.2 Utilisation de Kafka pour le stockage de données 27
1.7.3 En quoi Kafka est différent 28
1.8 Notes de terrain : Démarrer avec un projet Kafka 29
Premières étapes essentielles 29
Pièges courants à éviter 29
1.9 Ressources en ligne 30
1.10 Résumé 30
Chapitre 2 : Architecture d'un Cluster Kafka 35
Introduction 35
2.1 L'Unité Fondamentale : Anatomie d'un Message Kafka 35
Décomposition de l'enregistrement 35
Le rôle central de la Clé 36
La Valeur (Payload) et l'importance de la sérialisation 36
2.2 Organisation Logique : Topics, Partitions et Stratégies de Partitionnement 37
Le Topic comme un journal de transactions (commit log) distribué 37
La Partition : unité de parallélisme, d'ordonnancement et de stockage 37
Stratégies de partitionnement 38
Garanties et implications 38
2.3 Représentation Physique : Segments de Log et Indexation 39
De la partition logique au stockage physique 39
Le cycle de vie d'un segment 39
Mécanismes d'indexation 39
Extension du stockage : Tiered Storage 40
2.4 Durabilité et Haute Disponibilité : Le Modèle de Réplication 40
L'architecture Leader-Follower 40
Le Facteur de Réplication (replication.factor) 41
Les In-Sync Replicas (ISR) 41
Le High-Water Mark (HWM) 41
L'équation de la durabilité 42
2.5 Gestion du Cycle de Vie des Données : Rétention et Compactage 43
La politique de rétention (delete) 43
La politique de compactage (compact) 43
La gestion des suppressions via les "Tombstones" 44
Analyse comparative et politique combinée 44
2.6 Recommandations Architecturales et Bonnes Pratiques 45
Dimensionnement des partitions 45
Le choix de la clé de partitionnement 45
Configurer pour la durabilité vs. la disponibilité 45
Documenter l'architecture : l'utilité d'AsyncAPI 46
Chapitre 3 : Clients Kafka et Production de Messages 49
Introduction 49
3.1 L'Anatomie d'un Producer Kafka 49
3.2 Garanties Fondamentales de Production : Fiabilité et Cohérence des Données 51
3.3 Stratégies de Partitionnement et Ordonnancement des Messages 54
3.4 Sérialisation des Données et Gestion des Schémas 56
3.5 Optimisation des Performances et Gestion des Ressources 58
Conclusion du Chapitre : Recommandations Architecturales pour les Producers 60
Chapitre 4 : Création d'applications consommatrices 64
4.1 Consommateur Kafka : architecture et principes fondamentaux 64
4.1.1 Anatomie d'un consommateur : de l'interrogation au traitement 64
4.1.2 Le rôle central des offsets : suivre la progression dans un journal immuable 65
4.1.3 Le topic \_\_consumer_offsets : un état géré par le courtier 65
4.2 Atteindre le parallélisme : groupes de consommateurs et scalabilité 65
4.2.1 Le protocole du groupe de consommateurs : coordonner la consommation distribuée 66
4.2.2 À l'intérieur du groupe : les rôles du coordinateur de groupe et du leader de groupe 66
4.2.3 Stratégies d'assignation de partitions : une analyse comparative 67
4.3 Maîtriser le rééquilibrage des consommateurs 68
4.3.1 Déclencheurs et impacts du rééquilibrage 68
4.3.2 L'évolution des protocoles de rééquilibrage : de l'impératif au coopératif 68
4.3.3 Le protocole de nouvelle génération (KIP-848) : coordination côté serveur et gains de performance 69
4.3.4 Stratégie architecturale : atténuer les tempêtes de rééquilibrage avec l'adhésion statique au groupe 69
4.4 Modèles de conception fondamentaux pour la consommation de données 70
4.4.1 Gestion des offsets : le choix critique entre validation automatique et manuelle 70
4.4.2 Garantir l'intégrité des données : modèles de consommateur idempotent 71
4.4.3 Atteindre la sémantique "exactement une fois" : boucles transactionnelles "consommer-transformer-produire" 71
4.4.4 Niveaux d'isolation transactionnelle : comprendre read_committed vs read_uncommitted 72
4.5 Stratégies de consommation avancées 72
4.5.1 Consommer des topics compactés pour la gestion d'état et la mise en cache 72
4.5.2 Consommation sans code : intégration avec les connecteurs Kafka Connect Sink 73
4.5.3 Le Proxy REST Kafka : compromis architecturaux pour les environnements non-JVM 73
4.6 Réglage des performances : équilibrer débit et latence 74
4.6.1 Réglage pour un débit élevé : optimiser le traitement par lots et la récupération de données 74
4.6.2 Réglage pour une faible latence : minimiser le délai de transmission des messages 75
4.6.3 Le rôle de la compression : une comparaison des codecs 75
4.7 Construire des consommateurs résilients et prêts pour l'exploitation 76
4.7.1 Gestion avancée des erreurs : tentatives non bloquantes et files de messages morts 76
4.7.2 Surveillance et observabilité : métriques clés pour la santé des consommateurs 76
4.7.3 Dépannage des problèmes courants : un guide pour les architectes 77
Chapitre 5 : Cas d’utilisation Kafka 82
5.1 Quand choisir Kafka — et quand ne pas le faire 82
Le Principe Fondamental : Kafka comme Journal de Commit Distribué 82
Scénarios Idéaux pour Kafka (Les "Sweet Spots") 82
Les Anti-Patrons : Quand Kafka est un mauvais choix 83
5.2 Naviguer dans l'implémentation en contexte réel 83
5.2.1 Microservices événementiels 84
5.2.2 Intégration de données 84
5.2.3 Collecte de journaux (logs) 85
5.2.4 Traitement de données en temps réel 85
5.3 Différences avec d'autres plateformes de messagerie 86
5.3.1 Modèle publication-abonnement 86
5.3.2 Données partitionnées 86
5.3.3 Absence de logique côté broker 86
5.3.4 Accès séquentiel aux données 86
5.3.5 Persistance des messages 86
5.3.6 Limitations dans la gestion des messages volumineux 87
5.3.7 Évolutivité et haut débit 87
5.3.8 Tolérance aux pannes 87
5.3.9 Traitement par lots (batch) 87
5.3.10 Absence d'ordonnancement global 88
5.4 Alternatives à Kafka 88
5.4.1 RabbitMQ 89
5.4.2 Apache Pulsar 89
5.4.3 Solutions des fournisseurs infonuagiques 90
5.5 Ressources en ligne 92
5.6 Résumé 92
Chapitre 6 : Contrats de données 96
Traduire les produits d'affaires en schémas 96
Comment Kafka gère la structure des événements 97
Les événements dans Kafka 97
Défis dans la conception d'événements 98
Événements de changement d'état : représenter les changements d'état 98
Événements composites, atomiques et agrégés : représenter les flux d'événements 98
Intégrer l'état dans la notification 99
Structure de l'événement 100
Mapper les événements aux messages Kafka 101
Notes de terrain : Stratégies de données pour le projet Customer360 101
Gouvernance des événements 101
Schémas de données 101
Notes de terrain : Sélection du format de données pour le projet Customer360 102
Propriété des données 102
Organisation des données et communication des changements 103
Notes de terrain : Conception des événements pour le projet Customer360 103
Schema Registry 104
Le Schema Registry dans l'écosystème Kafka 104
Le rôle des schémas 104
Le concept de Sujet (Subject) 104
Vérification de la compatibilité 105
Alternatives au Schema Registry 106
Cas pratique : contrats de données utilisant le serveur centralisé 106
Extensions commerciales pour les contrats de données 107
Problèmes courants dans la gestion des contrats de données 107
Absence de validation côté serveur 107
Suppression de champs avec une pierre tombale (tombstone) pour les topics non compactés 108
Migration de l'état 108
Génération automatique de schémas 108
Ressources en ligne 109
Résumé 109
Chapitre 7 : Patrons d’interaction Kafka 114
7.1 Notes de terrain : Utiliser Kafka ou non : les cas problématiques 114
7.1.1 Utilisation de Kafka dans les Microservices 114
7.1.2 Traitement de données avec des pipelines Kafka 115
7.1.3 Patron Requête-Réponse 116
7.1.4 Patron CQRS 116
7.1.5 Event Sourcing avec captures d'état (snapshotting) 117
7.2 Implémentation d'un maillage de données (data mesh) 117
7.2.1 Notes de terrain : Implémenter un maillage de données avec Kafka 117
7.2.2 Kafka comme maillage de données 118
7.2.3 Propriété par domaine 118
7.2.4 La donnée comme produit 118
7.2.5 Gouvernance fédérée 119
7.2.6 Plateforme en libre-service 119
7.3 Utilisation de Kafka Connect 120
7.3.1 Kafka Connect en un coup d'œil 120
7.3.2 Architecture interne de Kafka Connect 120
7.3.3 Convertisseurs (Converters) 121
7.3.4 Transformations sur message unique (Single Message Transformations) 121
7.3.5 Connecteurs sources (Source connectors) 121
7.3.6 Connecteurs de destination (Sink connectors) 122
7.3.7 Changements dans la structure des données entrantes 122
7.3.8 Intégration avec les services infonuagiques 123
7.3.9 Notes de terrain : Choisir un connecteur pour Customer360 123
7.3.10 Problèmes courants de Kafka Connect 124
7.4 Assurer la garantie de livraison 124
7.4.1 Producteurs idempotents 124
7.4.2 Comprendre les transactions Kafka 125
7.4.3 La sémantique de livraison unique exacte (Exactly-once) 125
7.5 Ressources en ligne 126
7.6 Résumé 127
Chapitre 8 : Conception d’application de traitement de flux en continu 131
8.1. L'Ère du Temps Réel : Du Traitement par Lots au Traitement en Flux 131
Limitations des architectures de traitement par lots (Batch Processing) 131
L'impératif du traitement des "données en mouvement" (Data in Motion) 131
Principes fondamentaux et cas d'usage du traitement en flux (Stream Processing) 132
8.2. Introduction à Kafka Streams : Une Bibliothèque pour le Traitement en Flux 133
Relation avec les composants fondamentaux de Kafka 133
Positionnement : Pourquoi une bibliothèque et non un framework? 134
Objectifs de conception : Simplicité, élasticité et intégration 134
8.3. Architecture et Concepts Clés de Kafka Streams 135
Le modèle de parallélisme : Partitions, Tâches et Threads 135
La topologie de processeurs : Définir le flux de données 135
La dualité flux-table : KStream vs. KTable 136
La gestion du temps : Temps d'événement vs. Temps de traitement 137
8.4. Développement d'Applications : Des Opérations Simples aux Logiques Complexes 137
8.4.1. L'API DSL vs. l'API Processeur : Un Choix Architectural 137
8.4.2. Transformations sans État (Stateless) 138
8.4.3. Transformations avec État (Stateful) 139
8.5. Gestion de l'État, Cohérence et Tolérance aux Pannes 140
Les State Stores : Persistance et interrogeabilité 140
Durabilité et restauration : Le rôle des Changelog Topics et de la réplication 140
Sémantique Exactly-Once (EOS) : Garantir la cohérence de l'état 141
8.6. Positionnement dans l'Écosystème du Traitement de Données 141
Analyse comparative : Kafka Streams vs. Apache Flink et Apache Spark 142
Complémentarité avec Flink : L'abstraction SQL 143
Alternatives dans les Services Cloud Managés 143
8.7. Considérations Opérationnelles et Bonnes Pratiques pour la Production 144
8.7.1. Planification des Capacités (Capacity Planning) 144
8.7.2. Stratégies de Partitionnement des Topics 145
8.7.3. Gestion des Événements Désordonnés et Tardifs 146
8.7.4. Surveillance, Débogage et Gestion des Erreurs 146
8.8. Cas d'Usage Architectural : Construction d'une Vue Client 360 en Temps Réel 147
Conception de l'architecture événementielle 147
Implémentation avec Kafka Streams : Agrégation de flux et enrichissement de données 148
Activation des requêtes interactives pour l'exposition des données 148
Chapitre 9 : Gestion Kafka d’entreprise 152
Introduction du Chapitre 152
Stratégies de Déploiement et Modèles d'Architecture 152
L'Évolution Architecturale : De ZooKeeper à KRaft 152
Modèles de Déploiement : Auto-hébergé, Géré et Hybride 154
Déploiement sur Kubernetes : L'Approche Cloud-Native avec Strimzi 157
Dimensionnement et Scalabilité du Cluster 158
Principes de Dimensionnement de l'Infrastructure ("Right-Sizing") 158
Stratégies de Partitionnement pour la Performance et la Scalabilité 159
Scalabilité des Clients : Producteurs, Consommateurs et Kafka Streams 160
Optimisation des Performances et Monitoring 161
Métriques Clés et Méthodologies de Benchmarking 161
Réglages Fins (Tuning) des Composants Kafka 162
Sécurité de Niveau Entreprise 164
Chiffrement des Données : en Transit et au Repos 164
Authentification des Clients et des Brokers 164
Autorisation et Contrôle d'Accès Granulaire avec les ACLs 165
Gouvernance Opérationnelle et Gestion du Cycle de Vie 166
Opérations Administratives Courantes 166
Gouvernance des Données et Gestion des Schémas 167
Plan de Reprise d'Activité (PRA) et Haute Disponibilité 168
Monitoring, Alerting et Résolution d'Incidents 168
Chapitre 10 : Organisation d’un projet Kafka 174
10.1 Définition des exigences d'un projet Kafka 174
10.1.1 Notes de terrain : Collecte des cas d'utilisation et des exigences 174
10.1.2 Identification des flux de travail événementiels 175
10.1.3 Transformer les flux de travail d'affaires en événements 176
10.1.4 Recueil des exigences fonctionnelles pour les topics Kafka 177
10.1.5 Identification des exigences non fonctionnelles 179
10.2 Maintenir la structure du cluster 182
10.2.1 Utilisation d'outils 182
10.2.2 Utilisation de GitOps pour les configurations Kafka 183
10.2.3 Utilisation de l'API d'administration de Kafka 184
10.2.4 Mise en place des environnements 186
10.2.5 Notes de terrain : choisir une solution pour le projet Customer360 188
10.3 Tester les applications Kafka 189
10.3.1 Tests unitaires 189
10.3.2 Tests d'intégration 190
10.3.3 Tests de performance 191
10.4 Ressources en ligne 192
10.5 Résumé 192
Chapitre 11 : Opérer Kafka 197
Évolution et Mises à Niveau du Cluster 197
Ajout de Brokers et Répartition de la Charge 197
Retrait d'un Broker du Cluster 198
Mise à Niveau des Clients et du Cluster 199
Mobilité des Données 200
Surveillance du Cluster Kafka 200
Types de Métriques dans la Surveillance 201
Objets de Surveillance de Kafka 201
Propriété des Responsabilités de Surveillance 203
Piles (Stacks) et Outils de Surveillance 204
Clinique d'Optimisation des Performances 204
Équilibrer le Débit et la Latence 205
Équilibrer la Sécurité des Données et la Disponibilité 206
Reprise Après Sinistre et Basculement (Failover) 207
Ingénierie RTO/RPO 207
Ressources en Ligne 209
Résumé 209
Chapitre 12 : Avenir Kafka 215
12.1 Les origines de Kafka : vers une dorsale événementielle 215
Contexte Initial : Le Défi de LinkedIn 215
Le Changement de Paradigme : Du Message Broker au Log Distribué 216
L'Évolution vers la Dorsale Événementielle 217
12.2 Kafka comme plateforme d'orchestration 217
12.2.1 Intégration avec de nouveaux environnements d'exécution (runtimes) 217
12.2.2 Kafka avec WebAssembly 218
12.3 Kafka sans serveur (Serverless) 219
12.3.1 Kafka en périphérie de réseau (at the edge) 219
12.3.2 Kafka sans disque : Découpler le stockage des brokers 219
12.4 Kafka dans le monde de l'IA/AA 221
12.4.1 Apprentissage incrémental (Online Machine Learning) 221
12.4.2 Mettre l'analytique en mouvement 222
12.5 Kafka et les agents d'IA 222
12.6 Résumé 223
