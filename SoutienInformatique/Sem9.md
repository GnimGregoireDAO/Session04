# Fiche de révision - Gestion des demandes et des accès (Semaine 9)

## Partie 1 : Gestion des demandes (requêtes)

### Distinction entre incident et demande

| **Type**     | **Définition**                                                                    | **Formulation simple**                         | **Exemple**                                                              |
| ------------ | --------------------------------------------------------------------------------- | ---------------------------------------------- | ------------------------------------------------------------------------ |
| **Incident** | Interruption non planifiée ou dégradation de la qualité d'un service informatique | "J'ai quelque chose qui ne fonctionne plus"    | Un accès VPN qui fonctionnait hier et qui ne fonctionne plus aujourd'hui |
| **Demande**  | Un nouveau besoin d'un utilisateur                                                | "J'ai besoin de quelque chose que je n'ai pas" | Demande d'accès VPN pour un utilisateur qui n'en a jamais eu             |

> **Objectif principal de la gestion des demandes :** Offrir aux utilisateurs un canal au travers duquel sont demandés des services.

### Sources de signalement des demandes

Contrairement aux incidents qui peuvent être détectés par différentes sources, les demandes sont exclusivement signalées par les utilisateurs via :

- Appel téléphonique
- Clavardage
- Courriel
- Portail web

> **Point important :** Les administrateurs et les systèmes de surveillance ne peuvent pas deviner les besoins des utilisateurs.

### Processus de gestion des demandes

Le processus de gestion des demandes est similaire à celui des incidents avec quelques différences clés :

1. **Détection et enregistrement** (même processus que pour les incidents)
2. **Classification et priorisation** (avec différences spécifiques aux demandes)
3. **Validation et approbation** (au lieu du diagnostic pour les incidents)
4. **Affectation et escalade** (même processus que pour les incidents)
5. **Résolution** (avec considérations spécifiques aux demandes)
6. **Clôture** (même processus que pour les incidents)

### Différences entre le processus de gestion des incidents et des demandes

#### 1. Classification et priorisation

- **Classification différente :** Adaptée au contexte des demandes

  - Exemple : La classification "PC > Écran > Défectueux" n'existe pas pour une demande
  - Une classification équivalente pour une demande serait "PC > Écran > 2e écran requis"

- **Distinction entre demandes standards et non-standards :**

  - **Demandes standards :** Font partie du catalogue de services habituels (installation d'Acrobat Reader, accès à un dossier réseau, etc.)
  - **Demandes non-standards :** Ne font pas partie du catalogue habituel (installation d'un logiciel spécialisé, configuration particulière, etc.)

- **Matrice de priorités :** L'entreprise peut utiliser une matrice distincte pour les demandes

#### 2. Validation et approbation (au lieu du diagnostic)

- **Validation :** Vérifier que la demande est conforme et complète

  - Niveau 1 : Vérification de la conformité et complétude de la demande
  - Niveaux 2 et 3 : Vérification de la disponibilité des ressources (licences, impact sur les systèmes, etc.)

- **Approbation :** Obtenir les autorisations nécessaires
  - Nécessaire car les demandes génèrent souvent des coûts (achat de logiciel, de matériel, etc.)
  - Essentielle pour les demandes d'accès qui impliquent des considérations de sécurité
  - Les approbations doivent être conservées avec la demande

#### 3. Résolution

- **Respecter strictement la demande et l'autorisation :**
  - Donner exactement ce qui a été demandé et autorisé, ni plus ni moins
  - Ne pas prendre d'initiative qui dépasserait la portée de la demande ou de l'autorisation

### Ententes de niveaux de service (SLA)

Les ententes de niveaux de service pour les demandes diffèrent généralement de celles des incidents pour plusieurs raisons :

- Les demandes peuvent nécessiter des achats préalables
- Les demandes non-standards peuvent exiger des tests et une documentation
- Les demandes peuvent dépendre de l'approbation de tierces parties

#### Exemples de SLA pour les demandes standards (heures normales d'affaires)

| **Priorité** | **Temps de prise en charge** | **Temps de résolution** |
| ------------ | ---------------------------- | ----------------------- |
| P1           | 30 minutes                   | 2 heures                |
| P2           | 2 heures                     | 4 heures                |
| P3           | 4 heures                     | 8 heures                |
| P4           | 3 jours                      | 5 jours                 |
| P5           | 5 jours                      | 10 jours                |

#### Exemples de SLA pour les demandes standards (hors heures d'affaires)

| **Priorité** | **Temps de prise en charge** | **Temps de résolution** |
| ------------ | ---------------------------- | ----------------------- |
| P1           | 30 minutes                   | 4 heures                |
| P2           | 2 heures                     | 8 heures                |
| P3           | N/A                          | N/A                     |
| P4           | N/A                          | N/A                     |
| P5           | N/A                          | N/A                     |

#### SLA pour les demandes non-standards

| **Priorité** | **Temps de prise en charge** | **Temps de résolution** |
| ------------ | ---------------------------- | ----------------------- |
| Non-standard | 5 jours                      | Meilleur effort         |

> **Point important :** Pour les demandes non-standards, il est recommandé de ne pas promettre un temps de résolution précis en raison de leur complexité variable.

## Partie 2 : Gestion des accès

### Objectif et importance

**Objectif :** Fournir aux utilisateurs les privilèges (droits) nécessaires pour utiliser un service ou un groupe de services.

La gestion des accès :

- Doit être réalisée en accord avec les politiques de sécurité de l'information de l'entreprise
- Est critique dans la gestion de la sécurité globale de l'organisation

### Composantes de la gestion des accès

| **Composante**          | **Description**                                                                                                         | **Question clé**                                                                                |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| **Identité**            | Informations concernant les utilisateurs, permettant de les distinguer au sein de l'organisation                        | Qui est cet utilisateur?                                                                        |
| **Accès**               | Niveau et étendue des possibilités fonctionnelles ou des données d'un service qu'un utilisateur est autorisé à utiliser | À quoi l'utilisateur a-t-il accès?                                                              |
| **Droits (privilèges)** | Ce que l'utilisateur peut accomplir dans les accès donnés                                                               | Quels droits avons-nous effectivement donnés? (lecture, écriture, suppression, modification...) |

### Activités de la gestion des accès

#### 1. Vérifier l'identité du demandeur et valider la requête

- Vérification d'identité à la réception de la requête
- Vérification de la validité de la demande
- Obtention des autorisations nécessaires auprès des propriétaires de données/applications

#### 2. Accorder les droits

- Donner les droits demandés, ni plus ni moins
- Utiliser de préférence des groupes globaux dans l'annuaire (AD, LDAP)
- Éviter les comptes locaux qui compliquent le suivi des accès

#### 3. Surveiller les statuts des identités

- Suivre les mouvements de personnel (embauches, départs, transferts)
- Collaborer avec les RH pour obtenir un rapport hebdomadaire des mouvements
- Gérer les accès en fonction des changements de statut des employés

#### 4. Enregistrer et surveiller les accès

- Surveiller l'utilisation des accès, particulièrement pour les systèmes critiques
- Effectuer une revue des journaux de connexion
- Réaliser une revue annuelle des privilèges

### Risques et bonnes pratiques

#### Risques dans la gestion des accès

- **Accès "comme untel" :** Risque de donner des accès non autorisés ou trop larges
- **Manque de traçabilité :** Difficultés à suivre qui a accès à quoi et pourquoi
- **Comptes orphelins :** Accès qui restent actifs après le départ d'un employé

#### Mouvements de personnel et gestion des accès

| **Type de mouvement**     | **Actions requises**                                                           |
| ------------------------- | ------------------------------------------------------------------------------ |
| **Arrivées**              | Planifier la création des comptes, vérifier les besoins matériels et logiciels |
| **Départs**               | Planifier la désactivation des comptes, récupérer le matériel                  |
| **Changements de statut** | Ajuster les accès selon le nouveau rôle                                        |

#### Revues de privilèges

- Effectuer des revues périodiques (minimum annuelles)
- Prioriser les accès à hauts privilèges et les systèmes critiques
- Fournir aux responsables la liste des personnes ayant des accès pour validation

#### Gestion des comptes spéciaux

- **Consultants :** Configurer les comptes avec date d'expiration
- **Fournisseurs :** Activer les comptes uniquement pendant les périodes d'intervention
- **Comptes génériques :** Éviter leur utilisation autant que possible
- **Comptes de service :** Configurer en mode non-interactif

#### Bonnes pratiques pour la réinitialisation des mots de passe

- Vérifier rigoureusement l'identité de la personne
- Communiquer le nouveau mot de passe de façon sécurisée (ex: boîte vocale professionnelle)
- Forcer le changement du mot de passe à la première connexion
- Éviter d'utiliser toujours le même mot de passe temporaire
