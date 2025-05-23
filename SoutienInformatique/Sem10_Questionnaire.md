# Questionnaire d'entraînement - Semaine 10 Soutien Informatique

## Questions à choix multiples

1. **Quelle est la définition d'un problème selon ITIL?**

   - [ ] a) Une interruption non planifiée ou dégradation de la qualité d'un service informatique
   - [ ] b) La cause inconnue d'un ou plusieurs incidents de même classification
   - [ ] c) Une demande de service formulée par un utilisateur
   - [ ] d) Un événement qui pourrait affecter un service si aucune action n'est entreprise

2. **Qu'est-ce qu'une erreur connue dans le contexte de la gestion des problèmes?**

   - [ ] a) Un incident récurrent dont la solution est documentée
   - [ ] b) Un bug logiciel signalé par le fournisseur
   - [ ] c) Un problème dont la cause première est documentée et pour lequel une solution de contournement existe
   - [ ] d) Une erreur fréquemment commise par les utilisateurs

3. **Quel est l'objectif principal de la gestion des problèmes?**

   - [ ] a) Éliminer les répétitions d'incidents
   - [ ] b) Restaurer le service aussi rapidement que possible
   - [ ] c) Répondre aux demandes des utilisateurs
   - [ ] d) Gérer les changements dans l'infrastructure informatique

4. **Quelle étape du processus de gestion des problèmes vise à déterminer la cause originelle ("root cause")?**

   - [ ] a) Détection et enregistrement
   - [ ] b) Classification et priorisation
   - [ ] c) Diagnostic / investigation
   - [ ] d) Erreur connue et contournement

5. **Parmi les sources suivantes, laquelle peut conduire à la détection d'un problème?**

   - [ ] a) Une série d'incidents de même catégorie
   - [ ] b) Un utilisateur qui signale un incident
   - [ ] c) Une demande de nouveau service
   - [ ] d) Un changement planifié dans l'infrastructure

6. **Pourquoi n'y a-t-il généralement pas d'ententes de niveaux de service (SLA) associées aux priorités dans la gestion des problèmes?**

   - [ ] a) Parce que les problèmes sont toujours de basse priorité
   - [ ] b) Parce qu'il est difficile de prévoir la durée des investigations
   - [ ] c) Parce que les problèmes sont traités uniquement pendant les heures creuses
   - [ ] d) Parce que la résolution des problèmes est toujours immédiate

7. **Quelle est la différence principale entre un symptôme et une cause dans le cadre de la gestion des problèmes?**

   - [ ] a) Un symptôme est rapporté par les utilisateurs, une cause est identifiée par les techniciens
   - [ ] b) Un symptôme est temporaire, une cause est permanente
   - [ ] c) Un symptôme est la manifestation visible du problème, une cause est la raison fondamentale expliquant pourquoi le problème existe
   - [ ] d) Un symptôme est lié au matériel, une cause est liée au logiciel

8. **À quel moment un problème peut-il être considéré comme clos?**

   - [ ] a) Dès qu'une solution de contournement a été identifiée
   - [ ] b) Dès que la cause première a été identifiée
   - [ ] c) Lorsque tous les incidents liés ont été résolus
   - [ ] d) Lorsque la solution permanente a été implantée et qu'il est prouvé que le problème est entièrement résolu

## Questions à développement court

9. **Expliquez la différence entre un incident et un problème selon ITIL, et pourquoi cette distinction est importante pour le support informatique.**

10. **Décrivez la progression typique dans la compréhension d'un problème, depuis sa détection initiale jusqu'à sa résolution complète.**

11. **Pourquoi est-il crucial de ne pas confondre symptômes et causes lors de l'investigation d'un problème? Donnez un exemple concret.**

12. **Expliquez l'importance des solutions de contournement dans le processus de gestion des problèmes et quand elles devraient être mises en place.**

## Mises en situation

13. **Depuis deux semaines, plusieurs utilisateurs de différents départements signalent que l'application de comptabilité se bloque de façon aléatoire, les obligeant à redémarrer l'application et à récupérer leurs données. Le niveau 1 du centre de services a traité chaque cas individuellement, mais les incidents persistent.**

    a) Comment aborderiez-vous cette situation du point de vue de la gestion des problèmes?

    b) Quelles informations seraient importantes à recueillir pour créer un billet de problème pertinent?

    c) Proposez une classification et une priorisation pour ce problème, en justifiant votre choix.

    d) Décrivez les étapes d'investigation que vous entreprendriez pour identifier la cause racine.

14. **Une analyse des incidents des trois derniers mois révèle que les imprimantes d'un certain modèle tombent régulièrement en panne après avoir imprimé environ 5000 pages. Le fournisseur n'a pas signalé de problème connu avec ce modèle.**

    a) Comment classifieriez-vous et prioriseriez-vous ce problème?

    b) Quelles sources d'information consulteriez-vous pour mener votre investigation?

    c) Si vous identifiez la cause mais que la solution définitive nécessite le remplacement de toutes les imprimantes (ce qui prendra plusieurs semaines), quelle solution de contournement pourriez-vous proposer?

    d) Comment documenteriez-vous cette erreur connue dans votre système de gestion des billets?

15. **Le serveur de messagerie de l'entreprise devient extrêmement lent tous les lundis matin entre 9h et 10h, causant des retards dans la réception et l'envoi des courriels. Les autres jours de la semaine, le système fonctionne normalement.**

    a) Identifiez les sources potentielles de ce problème.

    b) Quelles données devriez-vous collecter pour votre investigation?

    c) Proposez un plan d'investigation méthodique pour identifier la cause racine.

    d) Comment géreriez-vous la communication avec les utilisateurs pendant que vous travaillez sur ce problème récurrent?

## Analyse de cas

16. **Étude de cas : Corruption de fichiers sur le serveur de fichiers**

Un technicien a ouvert un billet de problème suite à plusieurs incidents de corruption de fichiers signalés par différents utilisateurs. Voici les informations disponibles :

- Les corruptions touchent des fichiers de différents types (Word, Excel, PDF)
- Les fichiers sont stockés sur un serveur NAS
- Les corruptions semblent aléatoires et ne touchent pas tous les fichiers
- Certains fichiers sont partiellement corrompus (certaines informations illisibles), d'autres complètement (impossible d'ouvrir le fichier)
- Les sauvegardes contiennent parfois déjà des versions corrompues des fichiers
- Le problème est apparu il y a environ deux mois

  a) Classifiez et priorisez ce problème en justifiant votre choix.

  b) Quelles seraient vos premières étapes d'investigation pour ce problème? Listez au moins cinq vérifications que vous effectueriez.

  c) Supposons que vous découvriez qu'un des disques du NAS présente une LED orange clignotante. Après consultation du manuel, vous découvrez que cela indique un disque défaillant. Comment documenteriez-vous cette erreur connue? Quelle serait votre solution à court terme et votre plan pour une résolution définitive?

  d) Comment confirmeriez-vous que le problème est réellement résolu après le remplacement du disque? Quelle période d'observation recommanderiez-vous avant de clore le billet de problème?

## Réponses

1. b
2. c
3. a
4. c
5. a
6. b
7. c
8. d
9. _Un incident est une interruption non planifiée ou une dégradation de la qualité d'un service informatique qui affecte directement les utilisateurs, tandis qu'un problème est la cause sous-jacente d'un ou plusieurs incidents similaires. Cette distinction est cruciale car elle permet d'adopter des approches différentes : la gestion des incidents vise à restaurer rapidement le service pour minimiser l'impact sur les utilisateurs, alors que la gestion des problèmes cherche à identifier et éliminer la cause racine pour éviter la récurrence des incidents. Sans cette distinction, les équipes de support risquent de se concentrer uniquement sur la résolution des symptômes sans jamais éliminer la cause fondamentale, ce qui conduit à des incidents répétitifs et à une perte continue de ressources._
10. _La progression typique dans la compréhension d'un problème suit généralement ces étapes : 1) Identification du problème : on constate des incidents récurrents de même nature mais on ignore leur cause; 2) Investigation préliminaire : collecte d'informations, analyse des tendances et des circonstances entourant les incidents; 3) Identification de l'erreur connue : on détermine la source du problème (ex: composant défectueux) sans nécessairement comprendre entièrement pourquoi ou comment elle cause les incidents; 4) Analyse approfondie : on cherche à comprendre précisément le mécanisme par lequel la source identifiée génère les incidents; 5) Élaboration de la solution : une fois le mécanisme compris, on peut concevoir une solution permanente; 6) Validation : après mise en place de la solution, on vérifie que les incidents ne se reproduisent plus. Cette progression méthodique permet d'éviter les solutions hâtives qui ne traiteraient pas la cause réelle._
11. _Confondre symptômes et causes lors de l'investigation d'un problème peut mener à des solutions inefficaces qui ne résolvent pas le problème fondamental. Le symptôme est ce que l'on observe (la manifestation visible), tandis que la cause est ce qui provoque cette manifestation. Par exemple, des corruptions de fichiers (symptôme) peuvent être causées par un disque dur défectueux (cause). Si un technicien se concentre uniquement sur la restauration des fichiers corrompus sans identifier le disque défectueux, les corruptions continueront d'apparaître. En identifiant correctement la cause (disque défectueux), on peut mettre en place une solution permanente (remplacement du disque) qui éliminera définitivement le symptôme. Cette distinction permet d'optimiser les ressources et d'éviter les interventions répétitives._
12. _Les solutions de contournement sont essentielles dans le processus de gestion des problèmes car elles permettent de minimiser ou d'éliminer l'impact d'un incident ou d'un problème en attendant qu'une solution définitive soit disponible. Elles devraient être mises en place dès qu'on identifie que l'investigation et la résolution définitive prendront du temps, particulièrement pour les problèmes à impact élevé. Par exemple, si un serveur de base de données présente des lenteurs à cause d'une requête mal optimisée, une solution de contournement pourrait être de planifier cette requête pendant les heures creuses ou de mettre en place une limitation temporaire du nombre d'utilisateurs simultanés, pendant qu'on travaille sur l'optimisation de la requête. Ces solutions permettent aux utilisateurs de continuer à travailler malgré le problème sous-jacent, réduisant ainsi l'impact sur la productivité et la satisfaction des utilisateurs._
13. _Réponses variables selon l'analyse_
14. _Réponses variables selon l'analyse_
15. _Réponses variables selon l'analyse_
16. _Réponses variables selon l'analyse_
