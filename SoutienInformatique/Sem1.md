# Fiche de révision - Concepts clés en Soutien Informatique (Semaine 1)

## 1. Efficacité vs Efficience

| **Concept**    | **Définition**                                                                                                   | **Caractéristiques**                                                                                            | **Exemples**                                                                                                       |
| -------------- | ---------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| **Efficacité** | **Capacité à exécuter tous les aspects d'une demande.**                                                          | • Remplir toutes les exigences<br>• Focus sur les résultats<br>• Atteindre tous les objectifs fixés             | Préparer une présentation, réserver une salle, organiser l'enregistrement et envoyer les invitations comme demandé |
| **Efficience** | **Capacité de produire le maximum de résultats avec le minimum de ressources (employés, efforts, argent, etc).** | • Optimisation des ressources<br>• Respect des budgets, des délais<br>• Maximiser le ratio résultats/ressources | Installer une salle de formation en utilisant moins de budget que prévu ou en moins de temps                       |

> **⚠️ Précisions importantes :**
>
> - **Sur l'efficacité :** Prioritisez d'abord les attentes essentielles avant de viser l'efficacité complète
> - **Sur l'efficience :** Attention aux gains d'efficience qui pourraient réduire la qualité (obsolescence programmée, réduction excessive de services, etc.)

## 2. Réactivité vs Proactivité

| **Concept**     | **Définition**                                                                                                | **Approche**                                                     | **Quand l'utiliser**                                            |
| --------------- | ------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- | --------------------------------------------------------------- |
| **Réactivité**  | **Attendre qu'un événement se produise pour réagir.**                                                         | • Résolution de problèmes existants<br>• Action après l'incident | Quand le risque est faible (faible probabilité, impact limité)  |
| **Proactivité** | **Prévoir un événement et mettre en place les mesures correctives ou de mitigation avant qu'il se produise.** | • Anticipation des problèmes<br>• Prévention                     | Quand le risque est élevé (forte probabilité, impact important) |

> **Types de mesures proactives :**
>
> - **Mesures correctives :** Corriger la situation AVANT que le problème se produise (ex: éliminer un bogue, remplacer un équipement défaillant)
> - **Mesures de mitigation :** Mettre en place une solution qui RÉDUIT L'IMPACT du problème quand il se produira (ex: redondance d'équipements, mécanismes de timeout)

## 3. Analyse de risques

| **Composante**  | **Description**                                     | **Évaluation**                                                                                  |
| --------------- | --------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| **Probabilité** | Chances que l'événement se produise                 | • Entre 0% et 100%<br>• Basée sur l'historique et le contexte                                   |
| **Impact**      | Conséquences si l'événement se matérialise          | Évalué sur les aspects:<br>• Coûts<br>• Temps<br>• Qualité<br>• Portée                          |
| **Urgence**     | Rapidité d'action requise si l'événement se produit | • Action immédiate (1)<br>• Dans les 24h (0.8)<br>• Dans les 3 jours (0.6)<br>• Plus tard (0.3) |

> **📊 Formule de calcul du risque :**
>
> **RISQUE = PROBABILITÉ × IMPACT × URGENCE × 100**
>
> _Exemple 1:_ Verglas important (P=45%, I=40%, U=1) → Risque = 0.45 × 0.40 × 1 × 100 = **18**
>
> _Exemple 2:_ Panne serveur courriel (P=15%, I=25%, U=0.8) → Risque = 0.15 × 0.25 × 0.8 × 100 = **3**

## 4. Responsabilité vs Imputabilité

| **Concept**        | **Définition**                                                                                                     | **Focus**                                                                         | **Exemples**                                                                                        |
| ------------------ | ------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| **Responsabilité** | **Obligation de répondre de ses actions ou de celles des autres, d'être garant de quelque chose.**                 | • Exécution des tâches<br>• S'assurer du succès de l'activité dont on a la charge | Un technicien responsable de l'installation d'équipements                                           |
| **Imputabilité**   | **Obligation de démontrer que dans la gestion des ressources confiées, on s'est conformé à certaines conditions.** | • Reddition de comptes<br>• Répondre des résultats des activités déléguées        | Un VP informatique imputable de la sécurité des données même s'il n'exécute pas lui-même les tâches |

> **🔍 Applications pratiques :**
>
> - **Cas Desjardins (2019) :** Vol de données par un employé → VP sécurité congédié (imputable des résultats) → Président fait des entrevues (imputable de l'ensemble)
> - **Cas fournisseur Internet :** Panne chez le fournisseur → L'administrateur réseau reste imputable même s'il n'est pas responsable de la panne (doit faire des suivis, communiquer, envisager des changements)
