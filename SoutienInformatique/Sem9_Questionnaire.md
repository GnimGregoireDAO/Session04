# Questionnaire d'entraînement - Semaine 9 Soutien Informatique

## Questions à choix multiples

1. **Quelle est la principale différence entre un incident et une demande selon ITIL?**

   - [ ] a) Un incident est toujours de haute priorité, une demande est toujours de basse priorité
   - [ ] b) Un incident concerne un problème avec un équipement, une demande concerne un problème logiciel
   - [ ] c) Un incident est une interruption non planifiée d'un service existant, une demande est un besoin de nouveau service
   - [ ] d) Un incident est signalé par les utilisateurs, une demande est détectée par les systèmes de surveillance

2. **Quelle étape remplace le "diagnostic" dans le processus de gestion des demandes?**

   - [ ] a) Évaluation
   - [ ] b) Validation et approbation
   - [ ] c) Priorisation avancée
   - [ ] d) Planification de la résolution

3. **Qu'est-ce qu'une demande "standard" selon ITIL?**

   - [ ] a) Une demande qui n'exige pas d'approbation
   - [ ] b) Une demande qui fait partie du catalogue de services habituels
   - [ ] c) Une demande qui peut être résolue en moins d'une heure
   - [ ] d) Une demande qui vient d'un utilisateur régulier

4. **Pourquoi est-il recommandé d'utiliser des matrices de priorités différentes pour les incidents et les demandes?**

   - [ ] a) Pour équilibrer la charge de travail entre les équipes de support
   - [ ] b) Car les demandes sont généralement plus urgentes que les incidents
   - [ ] c) Car les demandes peuvent nécessiter des achats préalables et des approbations
   - [ ] d) Car les demandes sont toujours moins prioritaires que les incidents

5. **Quel est l'objectif principal de la gestion des accès?**

   - [ ] a) Limiter le nombre d'utilisateurs ayant accès aux systèmes
   - [ ] b) Fournir aux utilisateurs les privilèges nécessaires pour utiliser un service
   - [ ] c) Automatiser le processus d'attribution des droits
   - [ ] d) Documenter toutes les tentatives d'accès non autorisées

6. **Quelles sont les trois composantes de la gestion des accès?**

   - [ ] a) Identité, authentification, autorisation
   - [ ] b) Identité, accès, droits
   - [ ] c) Utilisateur, système, permission
   - [ ] d) Création, modification, suppression

7. **Quelle est la meilleure pratique concernant les demandes d'accès du type "je veux un accès comme untel"?**

   - [ ] a) Toujours les accepter car elles simplifient le processus
   - [ ] b) Les refuser systématiquement car elles violent les principes de sécurité
   - [ ] c) Vérifier avec le gestionnaire si tous les accès sont nécessaires
   - [ ] d) Vérifier chaque accès et obtenir les autorisations appropriées pour chacun

8. **Quelle est la bonne pratique pour la gestion des comptes de consultants externes?**

   - [ ] a) Leur donner uniquement des accès en lecture seule
   - [ ] b) Configurer les comptes avec une date d'expiration correspondant à la fin du mandat
   - [ ] c) Leur créer des comptes génériques partagés entre tous les consultants
   - [ ] d) Utiliser les mêmes paramètres que pour les employés permanents

## Questions à développement court

9. **Expliquez pourquoi il est important d'avoir des SLA (ententes de niveaux de service) différents pour les demandes standards et non-standards.**

10. **Décrivez les risques associés à l'attribution d'accès "comme untel" et comment les mitiger.**

11. **Expliquez l'importance des revues périodiques de privilèges et comment elles devraient être organisées.**

12. **Pourquoi est-il recommandé d'utiliser des groupes dans Active Directory plutôt que d'attribuer des droits directement aux utilisateurs? Donnez un exemple concret.**

## Mises en situation

13. **Vous recevez une demande pour installer un logiciel spécialisé de CAO (Conception Assistée par Ordinateur) sur le poste de travail d'un nouvel ingénieur. Le logiciel n'a jamais été installé dans l'entreprise auparavant.**

    a) Comment classifieriez-vous cette demande (standard ou non-standard) et quelle priorité lui attribueriez-vous? Justifiez votre réponse.

    b) Quelles validations et approbations seraient nécessaires avant de procéder à l'installation?

    c) Quelles informations devriez-vous recueillir pour documenter correctement cette demande?

    d) Quel SLA (entente de niveau de service) s'appliquerait à cette demande et pourquoi?

14. **Un gestionnaire vous demande de créer un accès pour une nouvelle employée (Lucie) qui remplace une personne qui prend sa retraite (Martin). Le gestionnaire vous indique simplement : "Donnez à Lucie exactement les mêmes accès que Martin".**

    a) Quels sont les risques associés à cette approche?

    b) Comment géreriez-vous cette demande de manière conforme aux bonnes pratiques de gestion des accès?

    c) Quelles informations rechercheriez-vous avant de créer les accès pour Lucie?

    d) Comment documenteriez-vous les accès créés pour faciliter les futures revues de privilèges?

15. **Un administrateur de système signale qu'un compte désactivé il y a six mois (appartenant à un ancien employé) a été utilisé pour se connecter à un serveur la nuit dernière.**

    a) Comment cela a-t-il pu se produire et quelles failles potentielles dans le processus de gestion des accès cela révèle-t-il?

    b) Quelles actions immédiates prendriez-vous pour sécuriser les systèmes?

    c) Quelles améliorations recommanderiez-vous pour le processus de gestion des accès afin d'éviter ce type de situation à l'avenir?

    d) Comment déterminer l'étendue potentielle de la compromission?

## Analyse de cas

16. **Scénario : Une entreprise de développement logiciel utilise le même processus et les mêmes SLA pour gérer à la fois les incidents et les demandes. Ils font face à plusieurs problèmes :**

- Les utilisateurs sont frustrés car les demandes de nouveaux logiciels ou équipements prennent trop de temps
- Le département informatique est débordé et a du mal à respecter ses engagements de service
- Les techniciens traitent les demandes de manière incohérente, certains demandant des approbations, d'autres non
- Des accès ont été accordés à des employés sans les autorisations appropriées

  a) Identifiez les principales lacunes dans leur processus actuel.

  b) Proposez une restructuration des processus de gestion des incidents et des demandes pour cette entreprise.

  c) Suggérez des SLA appropriés pour différentes catégories de demandes.

  d) Décrivez un processus de gestion des accès qui pourrait être mis en place pour éviter les problèmes d'accès non autorisés.

  e) Comment cette entreprise devrait-elle gérer et prioriser les demandes non-standards?

## Réponses

1. c
2. b
3. b
4. c
5. b
6. b
7. d
8. b
9. _Il est important d'avoir des SLA différents pour les demandes standards et non-standards car ces deux types de demandes impliquent des niveaux de complexité et d'incertitude très différents. Les demandes standards sont prévisibles, répétitives et font partie des opérations courantes, ce qui permet d'établir des délais précis basés sur l'expérience. En revanche, les demandes non-standards peuvent nécessiter des recherches, des tests, des achats de matériel ou logiciel, des approbations multiples ou des configurations spéciales. Leur temps de résolution est donc imprévisible. Établir des SLA irréalistes pour les demandes non-standards conduirait à des engagements impossibles à tenir, créant des attentes non satisfaites et de la frustration chez les utilisateurs._
10. _Les risques associés à l'attribution d'accès "comme untel" sont multiples : 1) Attribution de droits excessifs ou non nécessaires pour le rôle actuel de l'utilisateur; 2) Violation potentielle de la confidentialité si l'utilisateur de référence avait des accès spéciaux à des informations sensibles; 3) Contournement du processus d'approbation car les propriétaires des données/systèmes ne sont pas consultés; 4) Perpétuation d'erreurs si l'utilisateur de référence avait lui-même des accès inappropriés. Pour mitiger ces risques, il faut : extraire la liste des accès de l'utilisateur de référence, la soumettre au gestionnaire pour validation, obtenir l'approbation des propriétaires des données/systèmes pour chaque accès, et documenter clairement les accès accordés avec leurs justifications et approbations._
11. _Les revues périodiques de privilèges sont essentielles car elles constituent le dernier filet de sécurité pour détecter les accès inappropriés qui n'ont pas été correctement gérés lors des changements de statut des employés. Elles permettent d'identifier : les accès qui auraient dû être révoqués suite à un changement de rôle, les accès accordés temporairement mais jamais retirés, et les accès excessifs accordés par erreur. Ces revues devraient être organisées au moins annuellement, en priorisant les systèmes critiques et les accès à hauts privilèges. Le processus devrait impliquer les propriétaires des données et systèmes, qui reçoivent une liste des utilisateurs ayant accès à leurs ressources pour validation. Les anomalies identifiées doivent être corrigées immédiatement et le processus de gestion des accès ajusté pour éviter les mêmes erreurs à l'avenir._
12. _Réponses variables selon l'analyse_
13. _Réponses variables selon l'analyse_
14. _Réponses variables selon l'analyse_
15. _Réponses variables selon l'analyse_
16. _Réponses variables selon l'analyse_
