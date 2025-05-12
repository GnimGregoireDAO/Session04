# Fiche de Révision Angular - Semaine 13 : Web02

## Table des Matières

1. [Introduction à Angular](#introduction-à-angular)
2. [Les Composants](#les-composants)
3. [Transfert de Données](#transfert-de-donn%C3%A9es)
4. [Interpolation](#interpolation)
5. [Property Binding](#property-binding)
6. [Data Binding](#data-binding)
7. [Event Binding](#event-binding)
8. [Directives](#directives)
9. [Pipes](#pipes)
10. [Services](#services)
11. [Routing](#routing)
12. [Programmation Asynchrone et Observables](#programmation-asynchrone-et-observables)
13. [Conclusion](#conclusion)

---

## 1. Introduction à Angular

Angular est un framework développé et maintenu par Google.
Il permet de créer des applications web modernes, robustes et maintenables.
Angular repose sur TypeScript, offrant ainsi typage fort et meilleures pratiques de développement.
Ce framework adopte une architecture modulaire et repose fondamentalement sur le concept des composants.
Parmi ses atouts, on retrouve la gestion avancée du DOM, la séparation des responsabilités (MVC/MVVM), et la facilité d'intégration d'outils tiers.

### Points clés de l'introduction

- **Framework complet** : Angular offre une solution "tout en un" pour développer des applications.
- **Basé sur TypeScript** : Ce langage offre des fonctionnalités modernes avec la sécurité du typage.
- **Architecture orientée composants** : Chaque partie de l'application est regroupée dans des composants modulaires.
- **Outils intégrés** : Angular CLI, routing, services, etc.

### Quelques avantages d'Angular

1. **Scalabilité** : Adapté pour des projets de toutes tailles.
2. **Maintenance facilitée** : Une structure claire et des conventions strictes.
3. **Communauté dynamique** : Large écosystème et support important.
4. **Outils de développement** : CLI performant, tests unitaires, et plus.

Pour bien démarrer, assure-toi d'avoir Node.js, npm et Angular CLI installés sur ta machine.

---

## 2. Les Composants

Les composants sont la pierre angulaire d’Angular.
Un composant se compose généralement de trois parties :

1. **La classe TypeScript** qui contient la logique.
2. **Le template HTML** qui représente la vue.
3. **Le fichier de style (CSS/SCSS)** qui gère l’apparence.

### Cycle de vie d’un composant

Angular offre différents hooks du cycle de vie :

- `ngOnInit()` : Appelé après l’initialisation du composant.
- `ngOnChanges()` : Déclenché lors du changement des valeurs d’entrée.
- `ngDoCheck()` : Permet d’effectuer des vérifications personnalisées.
- `ngAfterViewInit()` : Appelé après l’initialisation des vues du composant.
- `ngOnDestroy()` : Permet de réaliser des nettoyages (unsubscribe, etc.).

### Exemple de composant simple

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
selector: 'app-exemple',
template: `
    <h2>Bonjour depuis l'exemple de composant !</h2>
    <p>{{ message }}</p>
`,
styles: [`
    h2 { color: #1976d2; }
    p { font-size: 16px; }
`]
})
export class ExempleComponent implements OnInit {
message: string = 'Bienvenue dans Angular';

constructor() { }

ngOnInit(): void {
    // Initialisation des données
    this.message += ' - Composant initialisé';
}
}
```

### Détails et bonnes pratiques des composants

1. **Séparation de la logique et de la vue** : Pense à garder ta logique métier dans la classe.
2. **Réutilisation** : Crée des composants réutilisables pour éviter la duplication.
3. **Communication entre composants** : Utilise `@Input()` et `@Output()` pour échanger des données.
4. **Gestion du cycle de vie** : Utilise correctement les hooks pour optimiser la performance.

---

#### Approfondissement - Récapitulatif des points essentiels sur les composants

1. Un composant Angular est encapsulé et isolé.
2. Chaque composant possède sa propre logique de rendu.
3. Les composants facilitent la division de l’application en parties indépendantes.
4. Angular CLI peut générer automatiquement des composants avec la commande `ng generate component NomDuComposant`.

**Exemples de commandes CLI :**

- Créer un nouveau composant : `ng generate component mon-composant`
- Créer un service associé : `ng generate service mon-service`

---

#### Détail : Communication entre composants parent et enfant

- Pour envoyer des données du parent vers l’enfant, utilise le décorateur `@Input()`.
- Pour notifier le parent à partir de l’enfant, utilise `@Output()` associé à un `EventEmitter`.

**Exemple de composant parent et enfant :**

**Composant Enfant (enfant.component.ts) :**

```typescript
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({
selector: 'app-enfant',
template: `
    <div>
      <p>Message du parent: {{ parentMessage }}</p>
      <button (click)="notifierParent()">Notifier le parent</button>
    </div>
`
})
export class EnfantComponent {
@Input() parentMessage: string = '';
@Output() reponse = new EventEmitter<string>();

notifierParent() {
    this.reponse.emit('L\'enfant a répondu !');
}
}
```

**Composant Parent (parent.component.ts) :**

```typescript
import { Component } from '@angular/core';

@Component({
selector: 'app-parent',
template: `
    <div>
      <app-enfant [parentMessage]="messageParent" (reponse)="gérerRéponse($event)"></app-enfant>
      <p>{{ reponseEnfant }}</p>
    </div>
`
})
export class ParentComponent {
messageParent: string = 'Salut de la part du parent!';
reponseEnfant: string = '';

gérerRéponse(event: string) {
    this.reponseEnfant = event;
}
}
```

#### Conseils supplémentaires sur les composants

1. Utilise les décorateurs Angular pour enrichir tes classes.
2. Implémente les interfaces Angular pour bénéficier de la suggestion d’IDE.
3. Teste chaque composant isolément.
4. Structure ton application avec des modules pour éviter les dépendances circulaires.

----------------------------------------------------------------

## 3. Transfert de Données

Le transfert de données en Angular se fait principalement grâce à :

- `@Input()` pour recevoir des données dans un composant enfant.
- `@Output()` et `EventEmitter` pour émettre des événements vers le composant parent.
- Les services, qui permettent de partager des données entre composants non liés.

### Transfert via @Input()

Le décorateur `@Input()` permet à un composant parent de passer des données à un composant enfant.

**Exemple d’utilisation :**

```typescript
export class EnfantComponent {
@Input() dataFromParent!: string;
}
```

Dans le template du composant parent, on utilise :

```html
<app-enfant [dataFromParent]="maVariable"></app-enfant>
```

### Transfert via @Output() et EventEmitter

Le décorateur `@Output()` couplé avec `EventEmitter` permet à un composant enfant de communiquer vers son parent.

**Exemple d’utilisation :**

```typescript
export class EnfantComponent {
@Output() dataToParent = new EventEmitter<string>();

envoyerDonnee() {
    this.dataToParent.emit('Voici la donnée envoyée par l\'enfant.');
}
}
```

Dans le composant parent, la réception se fait via un binding d’événement :

```html
<app-enfant (dataToParent)="recevoirDonnee($event)"></app-enfant>
```

### Transfert via Services

Les services Angular permettent de stocker et de partager des données entre de multiples composants.

**Exemple de service :**

```typescript
import { Injectable } from '@angular/core';
import { BehaviorSubject } from 'rxjs';

@Injectable({
providedIn: 'root'
})
export class DataService {
private dataSource = new BehaviorSubject<string>('valeur initiale');
currentData = this.dataSource.asObservable();

changeData(newData: string) {
    this.dataSource.next(newData);
}
}
```

**Utilisation dans un composant :**

```typescript
export class ExempleComponent implements OnInit {
data: string = '';

constructor(private dataService: DataService) { }

ngOnInit(): void {
    this.dataService.currentData.subscribe(data => {
      this.data = data;
    });
}
}
```

### Bonnes pratiques pour le transfert de données

1. Toujours valider les données avant transmission.
2. Utiliser des services pour centraliser l’état de l’application.
3. Employer `BehaviorSubject` lorsque tu souhaites avoir une valeur par défaut.
4. Veiller à se désabonner des observables dans `ngOnDestroy()` pour éviter les fuites de mémoire.

----------------------------------------------------------------

## 4. Interpolation

L'interpolation permet d’insérer des données dynamiques dans le template HTML.
On utilise la syntaxe `{{ expression }}` pour évaluer et afficher des variables.

### Exemples simples d'interpolation

1. Afficher une variable :

```html
<p>{{ titre }}</p>
```

2. Afficher le résultat d'une expression :

```html
<p>{{ 5 + 3 }}</p>
```

3. Afficher le résultat d'un appel de fonction :

```html
<p>{{ getMessage() }}</p>
```

### Remarques importantes

- L’interpolation est évaluée à chaque cycle de détection de changement.
- Elle fonctionne uniquement dans le contexte du template.
- Utile pour afficher des valeurs simples et pour le binding de texte.

### Cas pratiques

1. Afficher un objet JSON :

```html
<pre>{{ monObjet | json }}</pre>
```

2. Utiliser l’interpolation dans des balises HTML personnalisées.

3. Combiner l’interpolation avec d’autres bindings pour enrichir l’affichage.

#### Points à retenir

- L'interpolation est la méthode la plus simple pour afficher des données.
- Elle ne permet pas de modifier les valeurs, seulement de les afficher.
- C'est une technique purement unidirectionnelle (du composant vers la vue).

----------------------------------------------------------------

## 5. Property Binding

Le property binding permet de lier une propriété d’un élément DOM à une propriété du composant.

### Syntaxe du property binding

On entoure la propriété HTML avec des crochets :

```html
<img [src]="urlImage">
```

### Utilisation courante

1. Lier une source d’image :

- Si `urlImage` est une variable du composant, alors la source de l’image sera mise à jour dynamiquement.

2. Lier des attributs comme `disabled` ou `readonly` :

```html
<button [disabled]="estDesactive">Cliquez-moi</button>
```

### Avantages du property binding

- Il permet de changer dynamiquement l’état des éléments.
- Il assure que la vue reflète toujours la valeur la plus récente du composant.

### Bonnes pratiques

1. Préfère le property binding pour les attributs et non les interpolations.
2. Utilise des expressions simples pour ne pas surcharger le cycle de détection de changement.
3. Évite de manipuler le DOM directement.

#### Exemple complet

**Template :**

```html
<div>
<input [value]="nom" [disabled]="estEnLectureSeule">
<img [src]="urlImage" alt="Image dynamique">
</div>
```

**Composant :**

```typescript
export class MonComposant {
nom: string = 'Angular';
estEnLectureSeule: boolean = false;
urlImage: string = '<https://angular.io/assets/images/logos/angular/angular.png>';
}
```

----------------------------------------------------------------

## 6. Data Binding

Le data binding est un concept central qui regroupe plusieurs types de liaisons :

- **Interpolation** : Pour afficher des données.
- **Property Binding** : Pour lier des propriétés d’éléments.
- **Event Binding** : Pour capter des actions utilisateurs.
- **Two-way Binding** : Combinaison d’un property binding et d’un event binding.

### Two-way Binding

Syntaxe : `[(ngModel)]` (nécessite l’import du module `FormsModule`).

**Exemple :**

```html
<input [(ngModel)]="pseudo" placeholder="Entrez votre pseudo">
<p>Votre pseudo : {{ pseudo }}</p>
```

**Composant :**

```typescript
export class ExempleBindingComponent {
pseudo: string = '';
}
```

### Avantages du two-way binding

1. Synchronisation automatique entre modèle et vue.
2. Réduction du code nécessaire pour la gestion des formulaires.
3. Amélioration de la lisibilité du code.

#### Conseils pour le data binding

- Évitez d’utiliser des expressions compliquées directement dans le template.
- Privilégiez la séparation des préoccupations en déléguant la logique aux composants.
- Testez régulièrement le comportement du binding pour éviter les incohérences.

----------------------------------------------------------------

## 7. Event Binding

Le event binding permet de capter et de gérer des événements du DOM.

### Syntaxe de l’event binding

On utilise la syntaxe avec des parenthèses :

```html
<button (click)="executerAction()">Cliquez ici</button>
```

### Exemples d’événements

1. **click** : Déclenché lors d’un clic sur un élément.
2. **keyup** : Pour capter la frappe au clavier.
3. **mouseover** : Pour détecter le passage de la souris.

### Exemple complet avec event binding

**Template :**

```html
<div>
<button (click)="changerMessage()">Changer le message</button>
<p>{{ message }}</p>
</div>
```

**Composant :**

```typescript
export class ActionComponent {
message: string = 'Message initial';

changerMessage() {
    this.message = 'Le message a été mis à jour !';
}
}
```

### Bonnes pratiques pour l’event binding

1. Utilise des méthodes de composants pour gérer la logique des événements.
2. Limite la logique directement dans le template pour plus de clarté.
3. Vérifie que les événements n’entraînent pas des changements non prévus dans l’interface.

----------------------------------------------------------------

## 8. Directives

Les directives sont des marqueurs sur un élément DOM qui indiquent à Angular de lui appliquer un comportement particulier.

### Types de directives

1. **Directives structurelles** : Modifient la structure du DOM.

- Exemples : `*ngIf`, `*ngFor`, `*ngSwitch`.

2. **Directives attributs** : Modifient l’apparence ou le comportement d’un élément existant.

- Exemples : `[ngClass]`, `[ngStyle]`.

3. **Directives personnalisées** : Créées par le développeur pour étendre les fonctionnalités.

### Exemples de directives structurelles

**ngIf :**

```html
<p *ngIf="estVisible">Ce paragraphe est visible si estVisible est vrai.</p>
```

**ngFor :**

```html
<ul>
<li *ngFor="let item of items">{{ item }}</li>
</ul>
```

### Exemple de directive d’attribut

```html
<div [ngClass]="{'alert-success': isSuccess, 'alert-danger': !isSuccess}">
Ce div change de style selon la condition.
</div>
```

### Création d’une directive personnalisée

**Exemple : Directive pour changer la couleur de fond au survol**

```typescript
import { Directive, ElementRef, HostListener, Input } from '@angular/core';

@Directive({
selector: '[appSurvol]'
})
export class SurvolDirective {
@Input('appSurvol') couleurSurvol: string = 'yellow';

constructor(private el: ElementRef) { }

@HostListener('mouseenter') onMouseEnter() {
    this.changeBackground(this.couleurSurvol);
}

@HostListener('mouseleave') onMouseLeave() {
    this.changeBackground('');
}

private changeBackground(color: string) {
    this.el.nativeElement.style.backgroundColor = color;
}
}
```

### Bonnes pratiques pour les directives

- Crée des directives pour réutiliser du comportement sur plusieurs composants.
- Garde la logique au sein des directives simple et isolée.
- Teste tes directives de manière indépendante.

#### Points supplémentaires sur les directives

1. Les directives structurelles modifient le DOM (ajout ou suppression d’éléments).
2. Les directives attributs peuvent changer les styles, classes ou attributs.
3. Pour les directives personnalisées, veille à bien documenter leur usage.
4. Utilise le décorateur `@HostBinding` pour lier des propriétés d’un élément.
5. Utilise le décorateur `@HostListener` pour écouter des événements sur l’élément hôte.

----------------------------------------------------------------

## 9. Pipes

Les pipes servent à transformer l’affichage des données dans les templates.

### Pipes intégrés

Quelques pipes standards :

1. `date` : Formate une date.
2. `uppercase` et `lowercase` : Convertissent une chaîne en majuscules ou minuscules.
3. `currency` : Formate un nombre en tant que devise.
4. `percent` : Formate un nombre en pourcentage.
5. `json` : Affiche un objet JSON sous forme de chaîne lisible.

**Exemple d’utilisation :**

```html
<p>La date du jour : {{ aujourdHui | date:'fullDate' }}</p>
<p>{{ 'angular' | uppercase }}</p>
<p>{{ montant | currency:'EUR' }}</p>
```

### Création d’un pipe personnalisé

**Exemple : Pipe pour inverser une chaîne**

```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
name: 'inverse'
})
export class InversePipe implements PipeTransform {
transform(value: string): string {
    return value.split('').reverse().join('');
}
}
```

**Utilisation dans un template :**

```html
<p>{{ 'Angular' | inverse }}</p>
```

### Conseils pour les pipes

1. Les pipes doivent être sans effets de bord (pure functions) lorsqu’ils sont pure.
2. Pour des transformations complexes, envisage de créer des pipes personnalisés.
3. Attention aux performances : un pipe impure sera appelé à chaque détection de changement.
4. Teste tes pipes via des tests unitaires pour assurer leur cohérence.

----------------------------------------------------------------

## 10. Services

Les services sont des classes qui permettent de partager des fonctionnalités ou données entre composants.

### Création d’un service

On utilise le décorateur `@Injectable()` pour déclarer un service.

**Exemple simple :**

```typescript
import { Injectable } from '@angular/core';

@Injectable({
providedIn: 'root'
})
export class LoggerService {
log(message: string) {
    console.log(`LoggerService: ${message}`);
}
}
```

### Injection de dépendance

Une fois un service créé, tu peux l’injecter dans n’importe quel composant via le constructeur.

**Exemple dans un composant :**

```typescript
export class ExempleServiceComponent implements OnInit {
constructor(private logger: LoggerService) { }

ngOnInit(): void {
    this.logger.log('Component initialisé');
}
}
```

### Bonnes pratiques pour les services

1. Centralise la logique métier réutilisable dans des services.
2. Utilise des Observables dans tes services pour un flux de données réactif.
3. Implémente des tests unitaires pour valider le comportement du service.
4. Organise tes services par domaines fonctionnels.
5. Utilise `providedIn: 'root'` pour éviter des doublons et simplifier l’injection.

#### Autres conseils

- Sépare la logique métier et la logique de présentation.
- Évite les dépendances croisées entre services pour maintenir une architecture modulaire.
- Documente chaque service pour faciliter la maintenance.

----------------------------------------------------------------

## 11. Routing

Le routing permet de naviguer entre différentes vues ou pages d’une application Angular.

### Configuration du Routing

Le routing se configure en créant un module de routage (souvent `app-routing.module.ts`).

**Exemple de configuration de base :**

```typescript
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import { AccueilComponent } from './accueil/accueil.component';
import { AproposComponent } from './apropos/apropos.component';

const routes: Routes = [
{ path: '', component: AccueilComponent },
{ path: 'apropos', component: AproposComponent },
{ path: '**', redirectTo: '' }
];

@NgModule({
imports: [RouterModule.forRoot(routes)],
exports: [RouterModule]
})
export class AppRoutingModule { }
```

### Navigation dans l’application

Tu utilises `<router-outlet></router-outlet>` dans ton template principal pour afficher les composants associés aux routes.

**Exemple dans app.component.html :**

```html
<nav>
<a routerLink="/">Accueil</a>
<a routerLink="/apropos">À propos</a>
</nav>

<router-outlet></router-outlet>
```

### Paramètres de route et routeurs enfants

- Pour passer des paramètres, utilise `:id` dans la configuration des routes.
- Les routes enfants permettent de créer des sous-vues dans une application.

**Exemple de route avec paramètre :**

```typescript
{ path: 'produit/:id', component: ProduitComponent }
```

Dans le composant, récupère le paramètre via `ActivatedRoute`.

```typescript
import { ActivatedRoute } from '@angular/router';

export class ProduitComponent implements OnInit {
id: string | null = null;

constructor(private route: ActivatedRoute) { }

ngOnInit(): void {
    this.id = this.route.snapshot.paramMap.get('id');
}
}
```

### Conseils pour le routing

1. Utilise des routes paresseuses (lazy-loading) pour améliorer les performances.
2. Gère les erreurs de navigation (page 404) en configurant une route de redirection.
3. Documente la configuration des routes pour une meilleure lecture.
4. Organise les modules par fonctionnalité pour faciliter le lazy-loading.

----------------------------------------------------------------

## 12. Programmation Asynchrone et Observables

Angular utilise RxJS pour la programmation asynchrone.

### Les Observables

- Un Observable est un flux de données auquel on peut s’abonner.
- Il permet de gérer des événements asynchrones comme des requêtes HTTP.

**Exemple basique :**

```typescript
import { Observable, of } from 'rxjs';

const observable: Observable<number> = of(1, 2, 3, 4, 5);
observable.subscribe(val => console.log(val));
```

### Utilisation avec HttpClient

Le service `HttpClient` retourne des observables pour les opérations HTTP.

**Exemple d’appel HTTP :**

```typescript
import { HttpClient } from '@angular/common/http';

export class DataComponent implements OnInit {
data: any;

constructor(private http: HttpClient) { }

ngOnInit(): void {
    this.http.get('https://api.exemple.com/data')
      .subscribe(response => {
        this.data = response;
      });
}
}
```

### Les opérateurs RxJS

RxJS offre de nombreux opérateurs pour manipuler les observables :

1. **map** : Pour transformer des valeurs.
2. **filter** : Pour filtrer les valeurs.
3. **mergeMap** : Pour aplatir et combiner des observables.
4. **debounceTime** : Pour réguler le flux d’événements.
5. **switchMap** : Pour annuler d’anciennes souscriptions en cas de nouvel événement.

**Exemple avec l’opérateur map :**

```typescript
import { map } from 'rxjs/operators';

this.http.get('<https://api.exemple.com/data>')
.pipe(map((response: any) => response.data))
.subscribe(data => console.log(data));
```

### Bonnes pratiques en programmation asynchrone

1. Toujours se désabonner dans `ngOnDestroy()` pour éviter les fuites de mémoire.
2. Utiliser des opérateurs comme `takeUntil` pour gérer la durée de vie des abonnements.
3. Préférer les observables pour les opérations pouvant émettre plusieurs valeurs.
4. Gérer les erreurs avec les opérateurs `catchError` et `retry`.

#### Exemple d’utilisation de takeUntil

```typescript
import { Subject } from 'rxjs';
import { takeUntil } from 'rxjs/operators';

export class ExempleComponent implements OnDestroy {
private unsubscribe$ = new Subject<void>();

constructor(private http: HttpClient) { }

ngOnInit(): void {
    this.http.get('https://api.exemple.com/data')
      .pipe(takeUntil(this.unsubscribe$))
      .subscribe(data => console.log(data));
}

ngOnDestroy(): void {
    this.unsubscribe$.next();
    this.unsubscribe$.complete();
}
}
```

#### Points supplémentaires sur les observables

1. Les observables facilitent la gestion des flux événementiels.
2. Ils permettent une composition fluide des opérations asynchrones.
3. L’utilisation combinée d’opérateurs permet d’optimiser les performances.
4. Adopte une approche réactive pour construire des applications performantes.

----------------------------------------------------------------

## 13. Conclusion

Cette fiche de révision couvre en profondeur les concepts fondamentaux d’Angular abordés durant la semaine 13 du cours Web02.

### Récapitulatif des points essentiels

1. **Composants** : La base de toute appli Angular, avec un cycle de vie riche.
2. **Transfert de Données** : Utilisation de `@Input()`, `@Output()` et des services pour la communication inter-composants.
3. **Interpolation** : Méthode simple pour insérer des données dans le template.
4. **Property Binding** : Liaison dynamique des attributs HTML.
5. **Data Binding** : Combinaison des différents types de binding pour synchroniser modèle et vue.
6. **Event Binding** : Gestion des interactions utilisateurs.
7. **Directives** : Extensions du comportement du DOM via des directives structurelles et attributs.
8. **Pipes** : Transformation et formatage des données dans les templates.
9. **Services** : Partage de logique métier et d’état via l’injection de dépendance.
10. **Routing** : Navigation et gestion des vues avec le module de routage.
11. **Programmation Asynchrone et Observables** : Utilisation d’RxJS pour gérer les flux de données asynchrones.

### Derniers conseils pour une maîtrise d’Angular

- **Pratique régulière** : Expérimente chaque concept dans des projets réels ou des exercices.
- **Lire la documentation officielle** : Angular dispose d’une documentation riche et constamment mise à jour.
- **Participer à la communauté** : Les forums et GitHub sont d’excellents endroits pour échanger sur les meilleures pratiques.
- **Tester son code** : Utilise des tests unitaires et d’intégration pour assurer la robustesse de ton application.
- **Rester curieux** : Angular évolue régulièrement, donc reste informé des nouveautés.

### Quelques ressources supplémentaires

1. [Documentation Angular](https://angular.io/docs)
2. [Tutoriel Angular sur Angular University](https://angular-university.io/)
3. [Guide complet sur RxJS](https://rxjs-dev.firebaseapp.com/)
4. [Angular CLI Documentation](https://angular.io/cli)

### Mot de la fin

La compréhension de ces concepts te permettra de développer des applications web robustes et évolutives. Ne néglige aucun détail, car la maîtrise d’Angular passe par la compréhension de chaque petite pièce du puzzle.

Merci d’avoir parcouru cette fiche de révision détaillée. N’oublie pas que la pratique et la révision régulière sont les clés de la réussite en développement.

---

## Annexes et Exercices Complémentaires

### Exercice 1 : Créer un composant interactif

**Objectif :** Créer un composant affichant une liste de produits avec la possibilité de filtrer cette liste via un input.  
**Instructions :**  
a. Crée un composant `ProductListComponent`.  
b. Utilise l’interpolation pour afficher le nom de chaque produit.  
c. Ajoute un `@Input()` pour passer la liste des produits.  
d. Implémente un champ de recherche avec le two-way binding pour filtrer les produits.  
e. Affiche dynamiquement la liste filtrée en utilisant `*ngFor`.

### Exercice 2 : Communication entre Composants

**Objectif :** Mettre en place une communication bidirectionnelle entre un composant parent et un composant enfant.  
**Instructions :**  
a. Crée un composant parent `DashboardComponent` et un composant enfant `NotificationComponent`.  
b. Utilise `@Input()` pour envoyer un message du parent à l’enfant.  
c. Dans le composant enfant, ajoute un bouton qui, via un `@Output()`, émet un événement lorsque l’utilisateur clique dessus.  
d. Dans le composant parent, récupère cet événement et affiche une alerte.

### Exercice 3 : Création d’une Directive Personnalisée

**Objectif :** Créer une directive personnalisée qui change le style d’un élément lors du survol.  
**Instructions :**  
a. Crée une directive `HighlightDirective` à partir d’un `@Directive()`.  
b. Utilise `@HostListener` pour détecter les événements `mouseenter` et `mouseleave`.  
c. Applique la directive sur divers éléments de ton application pour tester son comportement.

### Exercice 4 : Utilisation de Pipes Personnalisés

**Objectif :** Créer un pipe personnalisé permettant de formater une chaîne en inversant son ordre.  
**Instructions :**  
a. Crée un pipe `ReversePipe`.  
b. Implémente la fonction de transformation qui inverse la chaîne donnée.  
c. Teste le pipe dans un template sur différents textes.

### Exercice 5 : Configuration du Routing

**Objectif :** Mettre en place un système de navigation entre plusieurs vues.  
**Instructions :**  
a. Configure les routes pour naviguer entre une page d’accueil, une page "À propos" et une page "Contact".  
b. Utilise `<router-outlet></router-outlet>` dans ton composant principal.  
c. Implémente des liens de navigation avec `routerLink`.

### Exercice 6 : Programmation Asynchrone avec Observables

**Objectif :** Récupérer des données depuis une API et les afficher dans un composant.  
**Instructions :**  
a. Crée un service `DataService` qui utilise `HttpClient` pour faire une requête GET.  
b. Dans un composant, abonne-toi à cet observable pour afficher les données dans une liste.  
c. Utilise des opérateurs RxJS pour transformer les données avant l’affichage.

### Exercice 7 : Test Unitaire d’un Service

**Objectif :** Écrire un test unitaire pour valider le fonctionnement d’un service.  
**Instructions :**  
a. Crée un service `MathService` avec une méthode `addition(a: number, b: number): number`.  
b. Écris un test unitaire avec Jasmine/Karma pour vérifier que la méthode retourne la somme correcte.  
c. Assure-toi que le service est correctement injecté dans le test.

### Exercice 8 : Gestion d’Erreur dans les Observables

**Objectif :** Mettre en place une gestion d’erreur dans un appel HTTP.  
**Instructions :**  
a. Dans ton service `DataService`, utilise l’opérateur `catchError` pour gérer les erreurs.
b. Affiche un message d’erreur dans le composant si l’API renvoie une erreur.
c. Utilise `retry` pour retenter l’appel en cas d’échec.

### Exercice 9 : Optimisation avec Lazy-Loading

**Objectif :** Implémenter le lazy-loading pour un module spécifique de ton application.  
**Instructions :**  
a. Crée un module `AdminModule` avec ses propres composants.
b. Configure le routing pour charger ce module de manière paresseuse.
c. Vérifie l’améli
