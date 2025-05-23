# Fiche de révision - Résolution de problèmes et Introduction à ITIL (Semaine 7)

## Partie 1 : Trucs et outils pour la résolution de problèmes

### Identification des types d'informations

Pour résoudre efficacement un problème informatique, il est essentiel de distinguer différents types d'informations :

| **Type d'information**           | **Définition**                                                        | **Caractéristiques**                                                                 | **Exemple**                                                                                        |
| -------------------------------- | --------------------------------------------------------------------- | ------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------- |
| **Faits**                        | Information validée ou tenue pour vraie provenant d'une source fiable | • Vérifiable<br>• Objectif<br>• Basé sur des observations directes                   | • "L'ordinateur est éteint"<br>• "Le message d'erreur affiché est XYZ"                             |
| **Déductions/Inférences**        | Information obtenue par raisonnement logique à partir des faits       | • N'est pas directement mentionnée<br>• Résulte d'un processus de réflexion          | • Si plusieurs appareils ne fonctionnent plus après un orage, on peut déduire une panne de courant |
| **Informations non pertinentes** | Information qui n'a pas d'impact sur le problème actuel               | • Peut distraire du vrai problème<br>• Mène souvent à des pistes erronées            | • Information sur une mise à jour Windows alors que le problème est un disque dur défectueux       |
| **Présomptions**                 | Information présumée vraie sans vérification concrète                 | • Basée sur des opinions ou intuitions<br>• Souvent influencée par l'effet de groupe | • "Ce problème est forcément dû au réseau" sans avoir vérifié                                      |
| **Symptômes**                    | Effets observables du problème, non la cause                          | • Observable et mesurable<br>• Indique qu'un problème existe                         | • Application qui gèle<br>• Lenteur du système                                                     |

> **Point important :** Ne pas confondre symptômes et causes. Traiter uniquement le symptôme (ex: redémarrer un serveur) sans identifier la cause sous-jacente ne résout pas définitivement le problème.

### Application à la résolution de problèmes

La capacité à distinguer ces types d'informations permet de :

1. **Éviter les fausses pistes** causées par des présomptions ou des informations non pertinentes
2. **Identifier la racine du problème** plutôt que de simplement traiter les symptômes
3. **Prioriser les actions** en se basant sur des faits vérifiés plutôt que des suppositions
4. **Communiquer efficacement** avec les utilisateurs et les collègues en se basant sur des informations fiables

## Partie 2 : Introduction à ITIL

### Qu'est-ce qu'ITIL ?

**ITIL** (Information Technology Infrastructure Library) est un ensemble de définitions et de bonnes/meilleures pratiques en gestion des TI. Il s'agit d'un référentiel qui encadre diverses activités des services informatiques.

> **Définition d'un référentiel :** Un système de références, un ensemble structuré d'informations contenant des définitions, des solutions et des pratiques relatives à un domaine de connaissance spécifique.

La version actuelle d'ITIL (v4) s'intègre avec d'autres approches modernes comme Agile, Lean, DevOps et le référentiel CobIT.

### Processus ITIL clés

#### Processus approfondis dans le cours

| **Processus**                                            | **Description**                                                                                                                                                 |
| -------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Centre de services TI (Service Desk)**                 | Prendre en charge les billets de service des utilisateurs et des clients des produits et services informatiques                                                 |
| **Gestion des incidents, des requêtes et des problèmes** | Encadrer les demandes des utilisateurs et clients, ainsi que leurs situations problèmes, pour fournir un service efficace et efficient de façon professionnelle |
| **Gestion des changements**                              | Planifier les changements aux systèmes informatiques                                                                                                            |

#### Processus survolés dans le cours

| **Processus**                                           | **Description**                                                                                             |
| ------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| **Gestion des événements**                              | Surveiller les systèmes informatiques pour réagir rapidement aux pannes et agir proactivement               |
| **Gestion des déploiements et des mises en production** | Élaborer les tests de vérification et les activités de livraison des produits/services informatiques        |
| **Gestion des connaissances**                           | Assurer que les systèmes et les pratiques sont bien documentés                                              |
| **Gestion des actifs et des configurations**            | Connaître l'environnement informatique dans son ensemble                                                    |
| **Amélioration continue**                               | S'améliorer constamment pour atteindre des niveaux plus élevés de performance, d'efficacité et d'efficience |

### L'exploitation des services

L'exploitation des services concerne la réalisation de toutes les activités nécessaires à la fourniture et au support des services. Elle repose sur trois piliers essentiels :

1. **Ressources humaines** (personnel compétent)
2. **Technologies** (outils adaptés)
3. **Processus** (méthodes efficaces)

> **Point important :** La livraison de services est un équilibre entre ces trois éléments. Pour améliorer la qualité de service, il faut intervenir sur ces trois aspects, pas uniquement sur l'un d'entre eux.

### L'impact d'ajouter plus de personnes

L'ajout de personnel augmente de façon exponentielle les liens de communication dans une organisation :

- P = Nombre de personnes
- L = Nombre de liens de communication
- L = P \* (P - 1)

Bien que la hiérarchisation réduise certains liens, l'augmentation du personnel a un impact significatif sur la complexité de la communication.

### Outils de gestion ITIL

Des outils spécifiques intègrent les processus ITIL pour guider les utilisateurs :

- **Exemples d'outils :** ConnectWise Manage, Octopus ITSM, BMC Track-IT, Service Now, JIRA Service Desk, GLPI
- **Avantages :** Les utilisateurs n'ont pas nécessairement besoin de connaître tous les détails des processus ITIL
- **Fonctionnalités couvertes :** Gestion des incidents/requêtes, des problèmes, des configurations, des changements
- **Préparation nécessaire :** Configuration initiale (utilisateurs, inventaire, rôles, équipes)

### Terminologie ITIL

| **Terme**                   | **Définition**                                                                                                            | **Expression simple**                                             |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| **Incident**                | Interruption non planifiée ou dégradation de la qualité d'un service informatique                                         | "J'ai quelque chose qui ne fonctionne plus ou qui fonctionne mal" |
| **Requête**                 | Demande d'un utilisateur pour une information, un conseil, un ajout/retrait de matériel/logiciel, ou l'accès à un système | "J'ai besoin de quelque chose que je n'ai pas"                    |
| **CI (Configuration Item)** | Élément géré par ou supportant les services informatiques                                                                 | Tout élément faisant partie de l'infrastructure TI                |

### Exemples de CI (Configuration Items)

| **Catégorie**               | **Description**                                                                      |
| --------------------------- | ------------------------------------------------------------------------------------ |
| **Documentation**           | Tous les documents relatifs à la gestion des TI                                      |
| **Données**                 | Les données d'entreprises conservées en bases de données                             |
| **Fournisseurs**            | Les fournisseurs de services TI                                                      |
| **Utilisateurs et clients** | Tous les utilisateurs et tous les clients                                            |
| **Équipements**             | Serveurs, imprimantes, postes de travail, routeurs, pare-feu, etc.                   |
| **Logiciels**               | Tous les logiciels, incluant ceux utilisés par les TI pour gérer les infrastructures |
| **Licences**                | Toutes les licences d'activation des logiciels et systèmes d'exploitation            |
| **Contrats**                | Tous les contrats servant à la bonne marche des TI                                   |

## Partie 3 : Présentation de GLPI

### Introduction à GLPI

GLPI est un outil de gestion qui met en œuvre les concepts ITIL. Il permet :

- La gestion des incidents et requêtes
- La gestion des problèmes
- La gestion des changements
- La gestion des assets (CI)

### Interface utilisateur de GLPI

#### Vue des employés

- Page d'accueil avec fonctionnalités : créer un billet, gérer ses billets, réserver un équipement, consulter la FAQ
- Zone de messages pour informer sur des situations problèmes ou interventions planifiées
- Formulaire de création de billet simplifié
- Vue limitée aux billets de l'utilisateur

#### Vue du centre d'assistance

- Accès à tous les billets
- Fonctionnalités de gestion complètes
- Communication avec les utilisateurs via messages publics et privés
- Outils de résolution des problèmes

### Utilisation dans le processus de résolution

GLPI s'intègre dans le processus de résolution de problèmes :

1. Réception du billet (déclencheur)
2. Évaluation des informations disponibles
3. Collecte d'informations supplémentaires via les fonctionnalités de communication
4. Documentation des actions et solutions
5. Clôture du billet une fois le problème résolu
