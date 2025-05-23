# Questionnaire d'entraînement - Semaine 8 Soutien Informatique

## Questions à choix multiples

1. **Quelle est la définition d'un incident selon ITIL?**

   - [ ] a) Un problème récurrent dont la cause est inconnue
   - [ ] b) Une demande d'information ou de service de la part d'un utilisateur
   - [ ] c) Une interruption non planifiée ou une dégradation de la qualité d'un service informatique
   - [ ] d) Un changement planifié dans l'infrastructure informatique

2. **Quel est l'objectif principal de la gestion des incidents?**

   - [ ] a) Déterminer la cause racine des problèmes
   - [ ] b) Restaurer les conditions normales de service aussi rapidement que possible
   - [ ] c) Améliorer les processus informatiques
   - [ ] d) Prévenir les incidents futurs

3. **Parmi les suivants, qui peut signaler un incident?**

   - [ ] a) Uniquement le centre de services
   - [ ] b) Uniquement les utilisateurs
   - [ ] c) Uniquement les systèmes de surveillance automatisés
   - [ ] d) Les utilisateurs, le personnel technique et les systèmes de surveillance

4. **Quels sont les deux facteurs principaux utilisés pour déterminer la priorité d'un incident?**

   - [ ] a) Coût et temps
   - [ ] b) Impact et urgence
   - [ ] c) Complexité et criticité
   - [ ] d) Catégorie et utilisateur concerné

5. **Quelle équipe est généralement responsable de la clôture définitive d'un incident?**

   - [ ] a) L'équipe qui a résolu l'incident
   - [ ] b) Le centre de services
   - [ ] c) L'utilisateur qui a signalé l'incident
   - [ ] d) Le gestionnaire de l'équipe concernée

6. **Dans une matrice de priorités, si un incident a un impact moyen et une urgence haute, quelle est généralement sa priorité?**

   - [ ] a) P1 (Très haute)
   - [ ] b) P2 (Haute)
   - [ ] c) P3 (Moyenne)
   - [ ] d) P4 (Basse)

7. **Pourquoi est-il important de limiter le nombre de catégories et de niveaux dans la classification des incidents?**

   - [ ] a) Pour réduire les coûts de maintenance du système de tickets
   - [ ] b) Pour éviter les erreurs de classification et réduire le temps de création de l'incident
   - [ ] c) Car ITIL impose un maximum de 5 catégories
   - [ ] d) Pour faciliter la génération des rapports de performance

8. **Que doit-on faire si, pendant la résolution d'un incident, on découvre que la classification initiale était erronée?**

   - [ ] a) Fermer l'incident et en créer un nouveau avec la bonne classification
   - [ ] b) Ignorer l'erreur et continuer avec la classification initiale
   - [ ] c) Ajuster la classification pour qu'elle soit adéquate
   - [ ] d) Escalader l'incident au niveau supérieur

## Questions à développement court

9. **Expliquez l'importance de la documentation des incidents et donnez trois caractéristiques d'une bonne documentation.**

10. **Décrivez les différentes situations qui peuvent se présenter après le diagnostic d'un incident et comment procéder pour chacune d'elles.**

11. **Quelle est la différence entre l'affectation et l'escalade d'un incident? Dans quelles circonstances devrait-on recourir à une escalade?**

12. **Pourquoi le contexte peut-il justifier d'ajuster la priorité déterminée par la matrice de priorités? Donnez un exemple concret.**

## Mises en situation

13. **Vous recevez un appel d'un utilisateur qui vous informe que son application de messagerie ne fonctionne plus. Il s'agit d'un cadre de direction qui a une présentation importante à faire dans 2 heures et a besoin d'accéder à des documents joints à ses emails.**

    a) Quelles informations essentielles devriez-vous recueillir lors de l'enregistrement de cet incident?

    b) Comment classifieriez-vous cet incident et quelle priorité lui attribueriez-vous? Justifiez votre réponse.

    c) Décrivez les étapes que vous suivriez pour gérer cet incident, de son enregistrement jusqu'à sa clôture.

14. **Vous êtes technicien au centre de services et vous recevez une alerte automatique indiquant que le serveur de base de données principal est tombé en panne. Cette base de données est utilisée par plusieurs applications critiques de l'entreprise.**

    a) Comment procéderiez-vous pour l'enregistrement et la classification de cet incident?

    b) Quelle priorité attribueriez-vous à cet incident et pourquoi?

    c) Dans ce cas, une escalade serait-elle appropriée? Si oui, expliquez pourquoi et comment vous procéderiez.

    d) Quels types de suivis effectueriez-vous pendant la résolution de cet incident?

15. **Un utilisateur signale qu'il ne peut pas imprimer sur l'imprimante du bureau. Après investigation, vous constatez que plusieurs utilisateurs rencontrent le même problème. Vous vérifiez l'imprimante et remarquez qu'elle affiche un message d'erreur indiquant un bourrage papier.**

    a) Comment la détection de ce problème affecte-t-elle la classification et la priorité de l'incident?

    b) Rédigez un exemple de documentation que vous incluriez dans le billet d'incident après la résolution.

    c) Comment géreriez-vous la communication avec les utilisateurs affectés tout au long du processus?

## Analyse de cas

16. **Lisez le scénario suivant et répondez aux questions :**

Un technicien reçoit un billet concernant un problème d'accès à une application financière critique. L'utilisateur, le directeur financier, ne peut pas accéder à l'application depuis son ordinateur portable et reçoit un message d'erreur "Connexion refusée". Le technicien note les informations suivantes :

- Le problème est survenu après une mise à jour de sécurité déployée la nuit précédente
- D'autres utilisateurs de la même équipe peuvent accéder à l'application sans problème
- Le directeur financier doit finaliser les rapports trimestriels avant la fin de la journée
- Le directeur financier peut accéder à toutes ses autres applications
- Le technicien vérifie les permissions et constate qu'elles semblent correctes

  a) Classifiez et priorisez cet incident en justifiant votre décision.

  b) Décrivez les étapes de diagnostic que vous entreprendriez pour résoudre ce problème.

  c) Si vous ne pouvez pas résoudre cet incident immédiatement, à quelle équipe l'affecteriez-vous et quels suivis effectueriez-vous?

  d) Rédigez un exemple de documentation complète que vous incluriez dans le billet après la résolution du problème.

## Réponses

1. c
2. b
3. d
4. b
5. b
6. b
7. b
8. c
9. _La documentation des incidents est essentielle car elle permet à n'importe quel technicien de comprendre l'incident et les solutions tentées, même des mois plus tard. Une bonne documentation doit être : 1) Concise mais complète, fournissant toutes les informations nécessaires sans détails superflus; 2) Structurée en points avec des phrases courtes qui décrivent clairement les actions effectuées et leurs résultats; 3) Chronologique, suivant l'ordre des étapes réalisées pour faciliter la compréhension du processus de résolution._
10. _Après le diagnostic d'un incident, quatre situations peuvent se présenter : 1) Une solution a été identifiée et peut être appliquée par le technicien actuel - dans ce cas, on passe directement à l'étape de résolution; 2) Une solution a été identifiée mais le technicien n'a pas les permissions nécessaires pour l'appliquer - l'incident doit être affecté à une équipe ayant les droits appropriés; 3) Aucune solution n'a été trouvée et le technicien (souvent de niveau 1) n'a pas le temps d'investiguer davantage - l'incident doit être affecté à un niveau supérieur; 4) Le technicien n'a pas les compétences nécessaires pour résoudre ce type de problème - l'incident doit être affecté à une équipe spécialisée appropriée._
11. _L'affectation est le transfert de l'incident à l'équipe de support appropriée pour sa résolution, tandis que l'escalade consiste à informer les membres de la direction d'un incident majeur nécessitant une attention immédiate. On recourt à l'escalade pour les incidents de priorité élevée (généralement P1) qui ont un impact significatif sur les opérations de l'entreprise et nécessitent une mobilisation rapide des ressources. Par exemple, une panne complète du système de facturation qui empêche l'entreprise de recevoir des paiements justifierait une escalade pour mobiliser rapidement toutes les ressources nécessaires à sa résolution._
12. _Réponses variables selon l'analyse_
13. _Réponses variables selon l'analyse_
14. _Réponses variables selon l'analyse_
15. _Réponses variables selon l'analyse_
16. _Réponses variables selon l'analyse_
