# Fiche de révision - Gestion des problèmes selon ITIL (Semaine 10)

## Terminologie de la gestion des problèmes

| **Terme**                     | **Définition**                                                                                                                                                                                         |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Problème**                  | Cause inconnue d'un ou plusieurs incidents de même classification (catégorie). D'où l'importance de valider la catégorie de l'incident lors de la clôture dudit incident.                              |
| **Erreur connue**             | Problème dont la cause première est documentée et pour lequel une solution de contournement existe. Par contre la solution définitive au problème est encore inconnue, ou en attente d'être implantée. |
| **Solution de contournement** | Réduit ou élimine l'impact d'un incident ou d'un problème pour lesquels une solution définitive n'est pas encore disponible.                                                                           |

> **Point important :** Un problème diffère d'un incident. Alors qu'un incident est une interruption de service qui affecte directement les utilisateurs, un problème est la cause sous-jacente qui peut être à l'origine de plusieurs incidents similaires.

## Objectifs de la gestion des problèmes

| **Objectif**                                | **Explication**                                                                                                                                                                                                                                         |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Éliminer les répétitions d'incidents**    | Réduire ou éliminer les incidents récurrents qui perturbent les services informatiques.                                                                                                                                                                 |
| **Minimiser l'impact des incidents**        | En identifiant une solution de contournement, réduire les durées des pannes et, dans certains cas, éviter complètement les impacts.                                                                                                                     |
| **Prévenir les problèmes et les incidents** | Anticiper les problèmes potentiels avant qu'ils ne causent des incidents. Les erreurs connues ne sont pas obligatoirement des incidents déjà vécus dans votre environnement (ex: anomalie détectée lors d'une analyse, avertissement d'un fournisseur). |

## Aperçu du processus de gestion des problèmes

Le processus de gestion des problèmes se déroule généralement en plusieurs étapes :

### 1. Détection et enregistrement

La détection d'un problème peut résulter de :

- Une série d'incidents de même catégorie
- Une analyse technique de l'infrastructure TI révélant une faille
- Un événement mettant en évidence un incident qui révèle une situation plus sérieuse
- Un avis d'un fournisseur de produits ou service
- Une analyse approfondie des incidents des derniers mois révélant une tendance problématique

L'enregistrement se fait en créant un billet de problème dans le système de gestion des billets. Une fois le problème créé, tous les incidents en rapport avec ce problème y sont liés.

### 2. Classification et priorisation

#### Classification

- Utilise généralement les mêmes catégories que celles associées aux incidents
- Facilite l'attribution du problème à l'équipe appropriée

#### Priorisation

- Peut utiliser une matrice spécifique aux problèmes ou la même que celle des incidents
- Les priorités servent à déterminer quels problèmes sont investigués en premier
- Généralement, il n'y a pas d'ententes de niveaux de service (SLA) associées aux priorités dans la gestion des problèmes, car il est difficile de prévoir la durée des investigations

> **Remarque :** Dans certains outils comme GLPI, une seule matrice de priorités peut être utilisée pour tous les types de billets (incidents, problèmes, demandes).

### 3. Diagnostic / investigation

Cette étape vise à déterminer la cause originelle ("root cause") du problème. Il est crucial de ne pas confondre symptômes et causes :

- **Symptôme :** Manifestation visible du problème (ex: corruption de fichiers)
- **Cause :** Raison fondamentale expliquant pourquoi le problème existe (ex: disque dur défectueux)

L'investigation peut nécessiter :

- L'analyse des journaux système
- L'inspection matérielle
- La consultation de bases de connaissances
- Des tests approfondis
- La consultation d'experts ou de fournisseurs

### 4. Erreur connue et contournement

Lorsqu'une investigation approfondie est nécessaire et risque de prendre du temps, il est recommandé d'identifier des solutions de contournement ("workarounds") permettant de :

- Corriger temporairement les incidents reliés au problème
- Redonner rapidement le service aux utilisateurs
- Limiter l'impact du problème pendant la recherche d'une solution permanente

La progression dans la compréhension d'un problème suit généralement ces étapes :

1. **Problème :** Cause inconnue d'incidents récurrents
2. **Erreur connue :** Source identifiée mais raison non entièrement comprise
3. **Solution :** Compréhension complète permettant de résoudre définitivement le problème

### 5. Résolution

Dans cette étape :

- La solution définitive est identifiée et appliquée
- Le processus de gestion des changements est mis en œuvre pour implémenter la solution
- Les tests sont effectués pour confirmer que la solution résout effectivement le problème

### 6. Clôture

La clôture du problème intervient lorsque :

- La solution permanente a été implantée
- Il est prouvé que le problème est entièrement résolu
- Tous les incidents liés au problème qui sont encore ouverts sont fermés
- L'erreur connue est retirée du système
- Le centre de services est avisé de la résolution
- La solution est documentée pour référence future

## Étude de cas pratique : Corruption de fichiers

### Contexte

Des utilisateurs signalent régulièrement des corruptions de fichiers depuis deux mois. Cette situation entraîne :

- Perte de temps pour les techniciens (recherche de fichiers non corrompus dans les sauvegardes)
- Perte d'heures de travail pour les utilisateurs
- Dans certains cas, perte complète de travail (impossible de trouver des versions non corrompues)

### Démarche de résolution

#### 1. Détection et enregistrement

- Création d'un billet de problème
- Documentation des symptômes observés et des impacts

#### 2. Classification et priorisation

- Classification : "Logiciels et applications > Défectuosité > Système de fichiers"
- Urgence : Haute (pertes de données significatives avec impacts potentiellement financiers)
- Impact : Moyen (affecte plusieurs utilisateurs et opérations importantes)
- Priorité résultante : Haute

#### 3. Diagnostic / investigation

- Vérification du matériel de stockage (NAS/SAN)
- Analyse des journaux système
- Inspection des indicateurs matériels
- Découverte d'une LED clignotante orange sur un disque du NAS/SAN
- Consultation du manuel du fabricant : indication d'un disque en problème pouvant causer des corruptions

#### 4. Erreur connue et contournement

- Documentation de l'erreur connue : disque défectueux dans le NAS/SAN
- Dans ce cas, pas de solution de contournement disponible
- Commande d'un disque de remplacement

#### 5. Résolution

- Remplacement du disque défectueux
- Période d'observation pour confirmer la résolution
- Vérification que les corruptions de fichiers ne se reproduisent plus

#### 6. Clôture

- Confirmation que la classification était adéquate
- Documentation complète de la solution
- Fermeture du billet de problème

## Bonnes pratiques pour la gestion des problèmes

1. **Distinguer clairement incidents et problèmes :**

   - Les incidents sont des interruptions de service
   - Les problèmes sont les causes sous-jacentes des incidents

2. **Mettre l'accent sur l'investigation :**

   - Prendre le temps nécessaire pour identifier la cause racine
   - Ne pas se contenter de solutions temporaires

3. **Documenter soigneusement :**

   - Tous les symptômes observés
   - Les étapes d'investigation entreprises
   - Les solutions de contournement identifiées
   - La solution définitive

4. **Maintenir une base de données d'erreurs connues :**

   - Permet de résoudre plus rapidement les incidents futurs
   - Facilite la formation des nouveaux techniciens

5. **Faire le lien entre incidents et problèmes :**
   - Associer les incidents au problème correspondant
   - Permet de mesurer l'impact global du problème
