# Fiche de révision - Gestion des incidents selon ITIL (Semaine 8)

## Introduction à la gestion des incidents

### Définition et objectif

| **Concept**            | **Description**                                                                   |
| ---------------------- | --------------------------------------------------------------------------------- |
| **Incident**           | Interruption non planifiée ou dégradation de la qualité d'un service informatique |
| **Objectif principal** | Restaurer les conditions normales de service aussi rapidement que possible        |

### Sources de signalement des incidents

Les incidents peuvent être signalés de différentes manières :

- **Par les utilisateurs** : via appel téléphonique, clavardage, courriel ou portail
- **Par le personnel technique** : un administrateur système qui détecte des anomalies
- **Par les systèmes de surveillance** : via des outils comme Nagios qui détectent automatiquement les problèmes et créent des billets

## Aperçu du processus de gestion des incidents

Le processus de gestion des incidents se déroule généralement en plusieurs étapes :

### 1. Détection et enregistrement

Cette étape consiste à :

- Recevoir le signalement de l'incident
- Créer un billet avec un numéro unique
- Enregistrer les informations essentielles :
  - Nom de la personne signalant l'incident
  - Systèmes affectés (CI - Configuration Items)
  - Description détaillée de l'incident
  - Messages d'erreur, actions effectuées avant l'incident, tentatives de résolution

> **Important :** Un enregistrement complet évite de devoir recontacter l'utilisateur pour obtenir des détails supplémentaires.

### 2. Classification et priorisation

#### Classification

La classification permet de catégoriser l'incident selon sa nature :

- Vise à associer l'incident à une catégorie principale puis à des sous-catégories
- Facilite l'attribution à la bonne équipe de support
- Doit être révisée lors de la résolution pour s'assurer de sa justesse

**Méthodes de classification courantes :**

1. **Hiérarchie à plusieurs niveaux :**

   - Catégorie > Sous-catégorie > Type de produit > Type de problème
   - Exemple : Matériel > PC > Écran > Dysfonctionnement

2. **Hiérarchie simplifiée :**
   - Catégorie > Type > Item
   - Exemple : PC > Écran > Dysfonctionnement

> **Conseil :** Limiter le nombre de catégories et de niveaux pour éviter les erreurs de classification et réduire le temps de création de l'incident.

#### Priorisation

La priorité d'un incident est déterminée par deux facteurs clés :

| **Concept** | **Définition**                                                     |
| ----------- | ------------------------------------------------------------------ |
| **Impact**  | L'ampleur des dégâts, matérialisés ou non, de la situation         |
| **Urgence** | La vitesse de réaction requise pour ramener le service en fonction |

**Matrice de priorités :** La priorité est généralement déterminée à l'aide d'une matrice d'impact et d'urgence.

|                                                                                 | **Urgence haute**<br>Action rapide requise | **Urgence moyenne**<br>Action dans les prochaines 72h | **Urgence basse**<br>Action dans les prochains jours |
| ------------------------------------------------------------------------------- | :----------------------------------------: | :---------------------------------------------------: | :--------------------------------------------------: |
| **Impact haut**<br>Affecte tous les utilisateurs ou opérations critiques        |              P1<br>Très haute              |                      P2<br>Haute                      |                    P3<br>Moyenne                     |
| **Impact moyen**<br>Affecte plusieurs utilisateurs ou opérations importantes    |                P2<br>Haute                 |                     P3<br>Moyenne                     |                     P4<br>Basse                      |
| **Impact bas**<br>Affecte un ou peu d'utilisateurs, ou opérations non-critiques |               P3<br>Moyenne                |                      P4<br>Basse                      |                   P5<br>Très basse                   |

> **Important :** Le contexte peut justifier d'ajuster la priorité déterminée par la matrice. Par exemple, un problème d'imprimante qui pourrait affecter la production dans 3 jours mérite une priorité plus élevée qu'indiqué par la matrice.

### 3. Diagnostic

Cette étape consiste à :

- Analyser l'incident en utilisant le processus de résolution de problèmes
- Confirmer la classification et la priorité de l'incident
- Rechercher des solutions possibles

Le diagnostic peut mener à deux résultats :

1. Une solution est trouvée → On passe à l'étape de résolution
2. Aucune solution n'est trouvée ou la solution exige des permissions particulières → On passe à l'étape d'affectation

### 4. Affectation et escalade (+ suivis)

#### Affectation

- Transfert de l'incident vers l'équipe de support appropriée
- Peut être réajustée si le diagnostic révèle que l'incident relève d'une autre équipe

#### Escalade

- Utilisée pour les incidents majeurs (généralement priorité P1)
- Implique d'informer les membres de la direction de l'entreprise
- Permet une prise en charge rapide des situations graves

#### Suivis

- Le centre de services reste responsable de s'assurer que l'incident est résolu
- Des suivis réguliers sont effectués pour vérifier la progression
- La fréquence des suivis dépend de la priorité de l'incident

### 5. Résolution

Dans cette étape :

- La solution identifiée est mise en œuvre
- L'incident est marqué comme résolu
- La confirmation de l'utilisateur est idéalement obtenue
- Les étapes de résolution et informations pertinentes sont documentées

### 6. Clôture

La clôture de l'incident :

- Est exclusivement effectuée par le centre de services
- Comprend la vérification que la classification était adéquate
- Inclut généralement l'envoi d'un message à l'utilisateur
- Peut inclure un sondage de satisfaction
- Permet à l'utilisateur de demander la réouverture si le problème persiste

## Bonnes pratiques pour la documentation des incidents

Dans le cadre de la gestion des incidents, la documentation doit être :

- Concise mais complète
- Structurée en phrases courtes, point par point
- Axée sur les actions effectuées et leurs résultats

**Exemple de bonne documentation :**

```
- J'ai modifié la clé de registre HKEY... et ça n'a pas fonctionné. J'ai remis à la valeur initiale.
- J'ai modifié le paramètre de résolution d'écran dans Windows, sans succès.
- J'ai modifié le paramètre « Screen size » dans le fichier config.txt pour la valeur 1248x728 et j'ai redémarré le programme. Ça a fonctionné.
```

L'objectif est de laisser des traces qui permettront à un autre technicien ou à vous-même ultérieurement de :

- Comprendre l'incident
- Connaître les informations recueillies
- Suivre les étapes réalisées pour résoudre l'incident

## Application pratique : Étude de cas

### Cas : Problème d'accès à la feuille de temps

**Scénario :** Arthur Vincent appelle concernant des difficultés d'accès à sa feuille de temps. Il reçoit le message "Accès interdit. Contacter votre administrateur" lors de la tentative de connexion. Tout fonctionnait bien la veille.

#### 1. Détection et enregistrement

- Créer un billet en identifiant le demandeur (Arthur Vincent)
- Vérifier/confirmer la localisation (Usine 1)
- Décrire précisément l'incident (logiciel, message d'erreur, contexte)

#### 2. Classification et priorisation

- Classifier : Accès > Accès à une application > Gestion du Temps
- Identifier les CI : Logiciel > Agendrix
- Déterminer l'impact (Bas - un seul utilisateur affecté)
- Évaluer l'urgence (Haute - besoin de résolution avant vendredi)
- Priorité résultante : P3 (Moyenne)

#### 3. Diagnostic

- Utiliser le diagramme de résolution de problèmes
- Consulter la base de connaissances
- Identifier une solution potentielle

#### 4. Résolution

- Appliquer la solution (fermer et redémarrer l'application)
- Vérifier avec l'utilisateur que le problème est résolu
- Documenter la solution appliquée

#### 5. Clôture

- Confirmer que la classification est correcte
- Documenter la solution dans le billet
- Fermer l'incident
