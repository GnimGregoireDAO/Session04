# Semaine 12 - Révision Web02

## Applications de type Single-Page (SPA)

### Concept
- Une application web qui interagit avec l'utilisateur en modifiant dynamiquement la page courante plutôt qu'en chargeant des pages complètes du serveur
- Fonctionne dans un navigateur et ne nécessite pas de rechargement pendant son utilisation

### Caractéristiques
- Navigation sans rechargement de page complète
- Chargement initial des ressources (HTML, CSS, JS)
- Utilisation intensive de JavaScript pour modifier le DOM
- Communication avec le serveur via des API (généralement RESTful)
- Meilleure expérience utilisateur (UX) avec des transitions fluides

### Avantages
- Expérience utilisateur améliorée et plus rapide
- Réduction du trafic serveur (chargement unique des ressources)
- Séparation claire entre frontend et backend
- Structure plus modulaire et facile à maintenir

### Inconvénients
- Complexité accrue du développement
- Problèmes potentiels de SEO (résolus par le rendu côté serveur)
- Premier chargement potentiellement plus lent
- Consommation mémoire plus importante

### Frameworks populaires pour SPA
- Angular
- React
- Vue.js
- Svelte
- Ember.js

## Le Framework Angular

### Présentation
- Framework JavaScript open-source développé par Google
- Permet de créer des applications web dynamiques côté client
- Utilise TypeScript comme langage de programmation
- Basé sur une architecture à composants

### Caractéristiques principales
- Architecture MVC (Modèle-Vue-Contrôleur)
- Data binding bidirectionnel
- Injection de dépendances
- Système de modules
- Routing intégré
- Tests unitaires facilités
- Templates déclaratifs

### Structure d'un projet Angular
- **Components**: Blocs de construction UI avec logique associée
- **Services**: Logique partagée entre composants
- **Modules**: Organisation du code en blocs fonctionnels
- **Directives**: Extension du HTML avec fonctionnalités personnalisées
- **Pipes**: Transformation de données dans le template

### Cycle de vie des composants
- `ngOnInit`: Après la création du composant
- `ngOnChanges`: Quand les données liées changent
- `ngOnDestroy`: Avant la destruction du composant
- Autres hooks: ngDoCheck, ngAfterContentInit, ngAfterViewInit, etc.

### Commandes CLI utiles
- `ng new app-name`: Créer une nouvelle application
- `ng serve`: Lancer le serveur de développement
- `ng generate component|service|module name`: Générer des éléments
- `ng build`: Construire l'application pour production
- `ng test`: Exécuter les tests

### Principaux décorateurs
- `@Component`: Définir un composant
- `@Injectable`: Définir un service injectable
- `@NgModule`: Définir un module
- `@Input/@Output`: Permettre la communication entre composants

### Évolution
- Angular (2+) est une réécriture complète d'AngularJS (v1)
- Mises à jour régulières et prévisibles (tous les 6 mois)
- Forte adoption dans l'industrie pour les applications d'entreprise
