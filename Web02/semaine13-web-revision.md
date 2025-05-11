# Fiche de Révision Angular - Semaine 13 : Web02

1.
2.

3. ## Table des Matières

4. 1. [Introduction à Angular](#introduction-à-angular)
5. 2. [Les Composants](#les-composants)
6. 3. [Transfert de Données](#transfert-de-donn%C3%A9es)
7. 4. [Interpolation](#interpolation)
8. 5. [Property Binding](#property-binding)
9. 6. [Data Binding](#data-binding)
10. 7. [Event Binding](#event-binding)
11. 8. [Directives](#directives)
12. 9. [Pipes](#pipes)
13. 10. [Services](#services)
14. 11. [Routing](#routing)
15. 12. [Programmation Asynchrone et Observables](#programmation-asynchrone-et-observables)
16. 13. [Conclusion](#conclusion)
17.
18. ---
19.

20. ## 1. Introduction à Angular

21.
22. Angular est un framework développé et maintenu par Google.
23. Il permet de créer des applications web modernes, robustes et maintenables.
24. Angular repose sur TypeScript, offrant ainsi typage fort et meilleures pratiques de développement.
25. Ce framework adopte une architecture modulaire et repose fondamentalement sur le concept des composants.
26. Parmi ses atouts, on retrouve la gestion avancée du DOM, la séparation des responsabilités (MVC/MVVM), et la facilité d’intégration d’outils tiers.
27.

28. ### Points clés de l’introduction

29.
30. - **Framework complet** : Angular offre une solution “tout en un” pour développer des applications.
31. - **Basé sur TypeScript** : Ce langage offre des fonctionnalités modernes avec la sécurité du typage.
32. - **Architecture orientée composants** : Chaque partie de l’application est regroupée dans des composants modulaires.
33. - **Outils intégrés** : Angular CLI, routing, services, etc.
34.

35. ### Quelques avantages d’Angular

36.
37. 1. **Scalabilité** : Adapté pour des projets de toutes tailles.
38. 2. **Maintenance facilitée** : Une structure claire et des conventions strictes.
39. 3. **Communauté dynamique** : Large écosystème et support important.
40. 4. **Outils de développement** : CLI performant, tests unitaires, et plus.
41.
42. (Ligne vide)
43.
44. Pour bien démarrer, assure-toi d’avoir Node.js, npm et Angular CLI installés sur ta machine.
45.
46. ---
47.

48. ## 2. Les Composants

49.
50. Les composants sont la pierre angulaire d’Angular.
51. Un composant se compose généralement de trois parties :
52. 1. **La classe TypeScript** qui contient la logique.
53. 2. **Le template HTML** qui représente la vue.
54. 3. **Le fichier de style (CSS/SCSS)** qui gère l’apparence.
55.

56. ### Cycle de vie d’un composant

57.
58. Angular offre différents hooks du cycle de vie :
59.
60. - `ngOnInit()` : Appelé après l’initialisation du composant.
61. - `ngOnChanges()` : Déclenché lors du changement des valeurs d’entrée.
62. - `ngDoCheck()` : Permet d’effectuer des vérifications personnalisées.
63. - `ngAfterViewInit()` : Appelé après l’initialisation des vues du composant.
64. - `ngOnDestroy()` : Permet de réaliser des nettoyages (unsubscribe, etc.).
65.

66. ### Exemple de composant simple

67.

68. ```typescript
69. import { Component, OnInit } from '@angular/core';
70.
71. @Component({
72. selector: 'app-exemple',
73. template: `
74.     <h2>Bonjour depuis l'exemple de composant !</h2>
75.     <p>{{ message }}</p>
76. `,
77. styles: [`
78.     h2 { color: #1976d2; }
79.     p { font-size: 16px; }
80. `]
81. })
82. export class ExempleComponent implements OnInit {
83. message: string = 'Bienvenue dans Angular';
84.
85. constructor() { }
86.
87. ngOnInit(): void {
88.     // Initialisation des données
89.     this.message += ' - Composant initialisé';
90. }
91. }

92. ```
93.

94. ### Détails et bonnes pratiques des composants

95.
96. 1. **Séparation de la logique et de la vue** : Pense à garder ta logique métier dans la classe.
97. 2. **Réutilisation** : Crée des composants réutilisables pour éviter la duplication.
98. 3. **Communication entre composants** : Utilise `@Input()` et `@Output()` pour échanger des données.
99. 4. **Gestion du cycle de vie** : Utilise correctement les hooks pour optimiser la performance.
100.
101. ---
102.

103. #### Approfondissement - Récapitulatif des points essentiels sur les composants

104.
105. 1. Un composant Angular est encapsulé et isolé.
106. 2. Chaque composant possède sa propre logique de rendu.
107. 3. Les composants facilitent la division de l’application en parties indépendantes.
108. 4. Angular CLI peut générer automatiquement des composants avec la commande `ng generate component NomDuComposant`.
109.
110. **Exemples de commandes CLI :**
111.
112. - Créer un nouveau composant : `ng generate component mon-composant`
113. - Créer un service associé : `ng generate service mon-service`
114.
115. ---
116.

117. #### Détail : Communication entre composants parent et enfant

118.
119. - Pour envoyer des données du parent vers l’enfant, utilise le décorateur `@Input()`.
120. - Pour notifier le parent à partir de l’enfant, utilise `@Output()` associé à un `EventEmitter`.
121.
122. **Exemple de composant parent et enfant :**
123.
124. **Composant Enfant (enfant.component.ts) :**
125.

126. ```typescript
127. import { Component, Input, Output, EventEmitter } from '@angular/core';
128.
129. @Component({
130. selector: 'app-enfant',
131. template: `
132.     <div>
133.       <p>Message du parent: {{ parentMessage }}</p>
134.       <button (click)="notifierParent()">Notifier le parent</button>
135.     </div>
136. `
137. })
138. export class EnfantComponent {
139. @Input() parentMessage: string = '';
140. @Output() reponse = new EventEmitter<string>();
141.
142. notifierParent() {
143.     this.reponse.emit('L\'enfant a répondu !');
144. }
145. }

146. ```
147.
148. **Composant Parent (parent.component.ts) :**
149.

150. ```typescript
151. import { Component } from '@angular/core';
152.
153. @Component({
154. selector: 'app-parent',
155. template: `
156.     <div>
157.       <app-enfant [parentMessage]="messageParent" (reponse)="gérerRéponse($event)"></app-enfant>
158.       <p>{{ reponseEnfant }}</p>
159.     </div>
160. `
161. })
162. export class ParentComponent {
163. messageParent: string = 'Salut de la part du parent!';
164. reponseEnfant: string = '';
165.
166. gérerRéponse(event: string) {
167.     this.reponseEnfant = event;
168. }
169. }

170. ```
171.

172. #### Conseils supplémentaires sur les composants

173.
174. 1. Utilise les décorateurs Angular pour enrichir tes classes.
175. 2. Implémente les interfaces Angular pour bénéficier de la suggestion d’IDE.
176. 3. Teste chaque composant isolément.
177. 4. Structure ton application avec des modules pour éviter les dépendances circulaires.
178.
179. ----------------------------------------------------------------
180.

181. ## 3. Transfert de Données

182.
183. Le transfert de données en Angular se fait principalement grâce à :
184. - `@Input()` pour recevoir des données dans un composant enfant.
185. - `@Output()` et `EventEmitter` pour émettre des événements vers le composant parent.
186. - Les services, qui permettent de partager des données entre composants non liés.
187.

188. ### Transfert via @Input()

189.
190. Le décorateur `@Input()` permet à un composant parent de passer des données à un composant enfant.
191.
192. **Exemple d’utilisation :**
193.

194. ```typescript
195. export class EnfantComponent {
196. @Input() dataFromParent!: string;
197. }

198. ```
199.
200. Dans le template du composant parent, on utilise :
201.

202. ```html
203. <app-enfant [dataFromParent]="maVariable"></app-enfant>

204. ```
205.

206. ### Transfert via @Output() et EventEmitter

207.
208. Le décorateur `@Output()` couplé avec `EventEmitter` permet à un composant enfant de communiquer vers son parent.
209.
210. **Exemple d’utilisation :**
211.

212. ```typescript
213. export class EnfantComponent {
214. @Output() dataToParent = new EventEmitter<string>();
215.
216. envoyerDonnee() {
217.     this.dataToParent.emit('Voici la donnée envoyée par l\'enfant.');
218. }
219. }

220. ```
221.
222. Dans le composant parent, la réception se fait via un binding d’événement :
223.

224. ```html
225. <app-enfant (dataToParent)="recevoirDonnee($event)"></app-enfant>

226. ```
227.

228. ### Transfert via Services

229.
230. Les services Angular permettent de stocker et de partager des données entre de multiples composants.
231.
232. **Exemple de service :**
233.

234. ```typescript
235. import { Injectable } from '@angular/core';
236. import { BehaviorSubject } from 'rxjs';
237.
238. @Injectable({
239. providedIn: 'root'
240. })
241. export class DataService {
242. private dataSource = new BehaviorSubject<string>('valeur initiale');
243. currentData = this.dataSource.asObservable();
244.
245. changeData(newData: string) {
246.     this.dataSource.next(newData);
247. }
248. }

249. ```
250.
251. **Utilisation dans un composant :**
252.

253. ```typescript
254. export class ExempleComponent implements OnInit {
255. data: string = '';
256.
257. constructor(private dataService: DataService) { }
258.
259. ngOnInit(): void {
260.     this.dataService.currentData.subscribe(data => {
261.       this.data = data;
262.     });
263. }
264. }

265. ```
266.

267. ### Bonnes pratiques pour le transfert de données

268.
269. 1. Toujours valider les données avant transmission.
270. 2. Utiliser des services pour centraliser l’état de l’application.
271. 3. Employer `BehaviorSubject` lorsque tu souhaites avoir une valeur par défaut.
272. 4. Veiller à se désabonner des observables dans `ngOnDestroy()` pour éviter les fuites de mémoire.
273.
274. ----------------------------------------------------------------
275.

276. ## 4. Interpolation

277.
278. L'interpolation permet d’insérer des données dynamiques dans le template HTML.
279. On utilise la syntaxe `{{ expression }}` pour évaluer et afficher des variables.
280.

281. ### Exemples simples d'interpolation

282.
283. 1. Afficher une variable :
284.

285. ```html
286. <p>{{ titre }}</p>

287. ```
288.
289. 2. Afficher le résultat d'une expression :
290.

291. ```html
292. <p>{{ 5 + 3 }}</p>

293. ```
294.
295. 3. Afficher le résultat d'un appel de fonction :
296.

297. ```html
298. <p>{{ getMessage() }}</p>

299. ```
300.

301. ### Remarques importantes

302.
303. - L’interpolation est évaluée à chaque cycle de détection de changement.
304. - Elle fonctionne uniquement dans le contexte du template.
305. - Utile pour afficher des valeurs simples et pour le binding de texte.
306.

307. ### Cas pratiques

308.
309. 1. Afficher un objet JSON :
310.

311. ```html
312. <pre>{{ monObjet | json }}</pre>

313. ```
314.
315. 2. Utiliser l’interpolation dans des balises HTML personnalisées.
316.
317. 3. Combiner l’interpolation avec d’autres bindings pour enrichir l’affichage.
318.

319. #### Points à retenir

320.
321. - L'interpolation est la méthode la plus simple pour afficher des données.
322. - Elle ne permet pas de modifier les valeurs, seulement de les afficher.
323. - C'est une technique purement unidirectionnelle (du composant vers la vue).
324.
325. ----------------------------------------------------------------
326.

327. ## 5. Property Binding

328.
329. Le property binding permet de lier une propriété d’un élément DOM à une propriété du composant.
330.

331. ### Syntaxe du property binding

332.
333. On entoure la propriété HTML avec des crochets :
334.

335. ```html
336. <img [src]="urlImage">

337. ```
338.

339. ### Utilisation courante

340.
341. 1. Lier une source d’image :
342. - Si `urlImage` est une variable du composant, alors la source de l’image sera mise à jour dynamiquement.
343.
344. 2. Lier des attributs comme `disabled` ou `readonly` :
345.

346. ```html
347. <button [disabled]="estDesactive">Cliquez-moi</button>

348. ```
349.

350. ### Avantages du property binding

351.
352. - Il permet de changer dynamiquement l’état des éléments.
353. - Il assure que la vue reflète toujours la valeur la plus récente du composant.
354.

355. ### Bonnes pratiques

356.
357. 1. Préfère le property binding pour les attributs et non les interpolations.
358. 2. Utilise des expressions simples pour ne pas surcharger le cycle de détection de changement.
359. 3. Évite de manipuler le DOM directement.
360.

361. #### Exemple complet

362.
363. **Template :**
364.

365. ```html
366. <div>
367. <input [value]="nom" [disabled]="estEnLectureSeule">
368. <img [src]="urlImage" alt="Image dynamique">
369. </div>

370. ```
371.
372. **Composant :**
373.

374. ```typescript
375. export class MonComposant {
376. nom: string = 'Angular';
377. estEnLectureSeule: boolean = false;
378. urlImage: string = '<https://angular.io/assets/images/logos/angular/angular.png>';
379. }

380. ```
381.
382. ----------------------------------------------------------------
383.

384. ## 6. Data Binding

385.
386. Le data binding est un concept central qui regroupe plusieurs types de liaisons :
387.
388. - **Interpolation** : Pour afficher des données.
389. - **Property Binding** : Pour lier des propriétés d’éléments.
390. - **Event Binding** : Pour capter des actions utilisateurs.
391. - **Two-way Binding** : Combinaison d’un property binding et d’un event binding.
392.

393. ### Two-way Binding

394.
395. Syntaxe : `[(ngModel)]` (nécessite l’import du module `FormsModule`).
396.
397. **Exemple :**
398.

399. ```html
400. <input [(ngModel)]="pseudo" placeholder="Entrez votre pseudo">
401. <p>Votre pseudo : {{ pseudo }}</p>

402. ```
403.
404. **Composant :**
405.

406. ```typescript
407. export class ExempleBindingComponent {
408. pseudo: string = '';
409. }

410. ```
411.

412. ### Avantages du two-way binding

413.
414. 1. Synchronisation automatique entre modèle et vue.
415. 2. Réduction du code nécessaire pour la gestion des formulaires.
416. 3. Amélioration de la lisibilité du code.
417.

418. #### Conseils pour le data binding

419.
420. - Évitez d’utiliser des expressions compliquées directement dans le template.
421. - Privilégiez la séparation des préoccupations en déléguant la logique aux composants.
422. - Testez régulièrement le comportement du binding pour éviter les incohérences.
423.
424. ----------------------------------------------------------------
425.

426. ## 7. Event Binding

427.
428. Le event binding permet de capter et de gérer des événements du DOM.
429.

430. ### Syntaxe de l’event binding

431.
432. On utilise la syntaxe avec des parenthèses :
433.

434. ```html
435. <button (click)="executerAction()">Cliquez ici</button>

436. ```
437.

438. ### Exemples d’événements

439.
440. 1. **click** : Déclenché lors d’un clic sur un élément.
441. 2. **keyup** : Pour capter la frappe au clavier.
442. 3. **mouseover** : Pour détecter le passage de la souris.
443.

444. ### Exemple complet avec event binding

445.
446. **Template :**
447.

448. ```html
449. <div>
450. <button (click)="changerMessage()">Changer le message</button>
451. <p>{{ message }}</p>
452. </div>

453. ```
454.
455. **Composant :**
456.

457. ```typescript
458. export class ActionComponent {
459. message: string = 'Message initial';
460.
461. changerMessage() {
462.     this.message = 'Le message a été mis à jour !';
463. }
464. }

465. ```
466.

467. ### Bonnes pratiques pour l’event binding

468.
469. 1. Utilise des méthodes de composants pour gérer la logique des événements.
470. 2. Limite la logique directement dans le template pour plus de clarté.
471. 3. Vérifie que les événements n’entraînent pas des changements non prévus dans l’interface.
472.
473. ----------------------------------------------------------------
474.

475. ## 8. Directives

476.
477. Les directives sont des marqueurs sur un élément DOM qui indiquent à Angular de lui appliquer un comportement particulier.
478.

479. ### Types de directives

480.
481. 1. **Directives structurelles** : Modifient la structure du DOM.
482. - Exemples : `*ngIf`, `*ngFor`, `*ngSwitch`.
483. 2. **Directives attributs** : Modifient l’apparence ou le comportement d’un élément existant.
484. - Exemples : `[ngClass]`, `[ngStyle]`.
485. 3. **Directives personnalisées** : Créées par le développeur pour étendre les fonctionnalités.
486.

487. ### Exemples de directives structurelles

488.
489. **ngIf :**
490.

491. ```html
492. <p *ngIf="estVisible">Ce paragraphe est visible si estVisible est vrai.</p>

493. ```
494.
495. **ngFor :**
496.

497. ```html
498. <ul>
499. <li *ngFor="let item of items">{{ item }}</li>
500. </ul>

501. ```
502.

503. ### Exemple de directive d’attribut

504.

505. ```html
506. <div [ngClass]="{'alert-success': isSuccess, 'alert-danger': !isSuccess}">
507. Ce div change de style selon la condition.
508. </div>

509. ```
510.

511. ### Création d’une directive personnalisée

512.
513. **Exemple : Directive pour changer la couleur de fond au survol**
514.

515. ```typescript
516. import { Directive, ElementRef, HostListener, Input } from '@angular/core';
517.
518. @Directive({
519. selector: '[appSurvol]'
520. })
521. export class SurvolDirective {
522. @Input('appSurvol') couleurSurvol: string = 'yellow';
523.
524. constructor(private el: ElementRef) { }
525.
526. @HostListener('mouseenter') onMouseEnter() {
527.     this.changeBackground(this.couleurSurvol);
528. }
529.
530. @HostListener('mouseleave') onMouseLeave() {
531.     this.changeBackground('');
532. }
533.
534. private changeBackground(color: string) {
535.     this.el.nativeElement.style.backgroundColor = color;
536. }
537. }

538. ```
539.

540. ### Bonnes pratiques pour les directives

541.
542. - Crée des directives pour réutiliser du comportement sur plusieurs composants.
543. - Garde la logique au sein des directives simple et isolée.
544. - Teste tes directives de manière indépendante.
545.

546. #### Points supplémentaires sur les directives

547.
548. 1. Les directives structurelles modifient le DOM (ajout ou suppression d’éléments).
549. 2. Les directives attributs peuvent changer les styles, classes ou attributs.
550. 3. Pour les directives personnalisées, veille à bien documenter leur usage.
551. 4. Utilise le décorateur `@HostBinding` pour lier des propriétés d’un élément.
552. 5. Utilise le décorateur `@HostListener` pour écouter des événements sur l’élément hôte.
553.
554. ----------------------------------------------------------------
555.

556. ## 9. Pipes

557.
558. Les pipes servent à transformer l’affichage des données dans les templates.
559.

560. ### Pipes intégrés

561.
562. Quelques pipes standards :
563.
564. 1. `date` : Formate une date.
565. 2. `uppercase` et `lowercase` : Convertissent une chaîne en majuscules ou minuscules.
566. 3. `currency` : Formate un nombre en tant que devise.
567. 4. `percent` : Formate un nombre en pourcentage.
568. 5. `json` : Affiche un objet JSON sous forme de chaîne lisible.
569.
570. **Exemple d’utilisation :**
571.

572. ```html
573. <p>La date du jour : {{ aujourdHui | date:'fullDate' }}</p>
574. <p>{{ 'angular' | uppercase }}</p>
575. <p>{{ montant | currency:'EUR' }}</p>

576. ```
577.

578. ### Création d’un pipe personnalisé

579.
580. **Exemple : Pipe pour inverser une chaîne**
581.

582. ```typescript
583. import { Pipe, PipeTransform } from '@angular/core';
584.
585. @Pipe({
586. name: 'inverse'
587. })
588. export class InversePipe implements PipeTransform {
589. transform(value: string): string {
590.     return value.split('').reverse().join('');
591. }
592. }

593. ```
594.
595. **Utilisation dans un template :**
596.

597. ```html
598. <p>{{ 'Angular' | inverse }}</p>

599. ```
600.

601. ### Conseils pour les pipes

602.
603. 1. Les pipes doivent être sans effets de bord (pure functions) lorsqu’ils sont pure.
604. 2. Pour des transformations complexes, envisage de créer des pipes personnalisés.
605. 3. Attention aux performances : un pipe impure sera appelé à chaque détection de changement.
606. 4. Teste tes pipes via des tests unitaires pour assurer leur cohérence.
607.
608. ----------------------------------------------------------------
609.

610. ## 10. Services

611.
612. Les services sont des classes qui permettent de partager des fonctionnalités ou données entre composants.
613.

614. ### Création d’un service

615.
616. On utilise le décorateur `@Injectable()` pour déclarer un service.
617.
618. **Exemple simple :**
619.

620. ```typescript
621. import { Injectable } from '@angular/core';
622.
623. @Injectable({
624. providedIn: 'root'
625. })
626. export class LoggerService {
627. log(message: string) {
628.     console.log(`LoggerService: ${message}`);
629. }
630. }

631. ```
632.

633. ### Injection de dépendance

634.
635. Une fois un service créé, tu peux l’injecter dans n’importe quel composant via le constructeur.
636.
637. **Exemple dans un composant :**
638.

639. ```typescript
640. export class ExempleServiceComponent implements OnInit {
641. constructor(private logger: LoggerService) { }
642.
643. ngOnInit(): void {
644.     this.logger.log('Component initialisé');
645. }
646. }

647. ```
648.

649. ### Bonnes pratiques pour les services

650.
651. 1. Centralise la logique métier réutilisable dans des services.
652. 2. Utilise des Observables dans tes services pour un flux de données réactif.
653. 3. Implémente des tests unitaires pour valider le comportement du service.
654. 4. Organise tes services par domaines fonctionnels.
655. 5. Utilise `providedIn: 'root'` pour éviter des doublons et simplifier l’injection.
656.

657. #### Autres conseils

658.
659. - Sépare la logique métier et la logique de présentation.
660. - Évite les dépendances croisées entre services pour maintenir une architecture modulaire.
661. - Documente chaque service pour faciliter la maintenance.
662.
663. ----------------------------------------------------------------
664.

665. ## 11. Routing

666.
667. Le routing permet de naviguer entre différentes vues ou pages d’une application Angular.
668.

669. ### Configuration du Routing

670.
671. Le routing se configure en créant un module de routage (souvent `app-routing.module.ts`).
672.
673. **Exemple de configuration de base :**
674.

675. ```typescript
676. import { NgModule } from '@angular/core';
677. import { Routes, RouterModule } from '@angular/router';
678. import { AccueilComponent } from './accueil/accueil.component';
679. import { AproposComponent } from './apropos/apropos.component';
680.
681. const routes: Routes = [
682. { path: '', component: AccueilComponent },
683. { path: 'apropos', component: AproposComponent },
684. { path: '**', redirectTo: '' }
685. ];
686.
687. @NgModule({
688. imports: [RouterModule.forRoot(routes)],
689. exports: [RouterModule]
690. })
691. export class AppRoutingModule { }

692. ```
693.

694. ### Navigation dans l’application

695.
696. Tu utilises `<router-outlet></router-outlet>` dans ton template principal pour afficher les composants associés aux routes.
697.
698. **Exemple dans app.component.html :**
699.

700. ```html
701. <nav>
702. <a routerLink="/">Accueil</a>
703. <a routerLink="/apropos">À propos</a>
704. </nav>
705.
706. <router-outlet></router-outlet>

707. ```
708.

709. ### Paramètres de route et routeurs enfants

710.
711. - Pour passer des paramètres, utilise `:id` dans la configuration des routes.
712. - Les routes enfants permettent de créer des sous-vues dans une application.
713.
714. **Exemple de route avec paramètre :**
715.

716. ```typescript
717. { path: 'produit/:id', component: ProduitComponent }

718. ```
719.
720. Dans le composant, récupère le paramètre via `ActivatedRoute`.
721.

722. ```typescript
723. import { ActivatedRoute } from '@angular/router';
724.
725. export class ProduitComponent implements OnInit {
726. id: string | null = null;
727.
728. constructor(private route: ActivatedRoute) { }
729.
730. ngOnInit(): void {
731.     this.id = this.route.snapshot.paramMap.get('id');
732. }
733. }

734. ```
735.

736. ### Conseils pour le routing

737.
738. 1. Utilise des routes paresseuses (lazy-loading) pour améliorer les performances.
739. 2. Gère les erreurs de navigation (page 404) en configurant une route de redirection.
740. 3. Documente la configuration des routes pour une meilleure lecture.
741. 4. Organise les modules par fonctionnalité pour faciliter le lazy-loading.
742.
743. ----------------------------------------------------------------
744.

745. ## 12. Programmation Asynchrone et Observables

746.
747. Angular utilise RxJS pour la programmation asynchrone.
748.

749. ### Les Observables

750.
751. - Un Observable est un flux de données auquel on peut s’abonner.
752. - Il permet de gérer des événements asynchrones comme des requêtes HTTP.
753.
754. **Exemple basique :**
755.

756. ```typescript
757. import { Observable, of } from 'rxjs';
758.
759. const observable: Observable<number> = of(1, 2, 3, 4, 5);
760. observable.subscribe(val => console.log(val));

761. ```
762.

763. ### Utilisation avec HttpClient

764.
765. Le service `HttpClient` retourne des observables pour les opérations HTTP.
766.
767. **Exemple d’appel HTTP :**
768.

769. ```typescript
770. import { HttpClient } from '@angular/common/http';
771.
772. export class DataComponent implements OnInit {
773. data: any;
774.
775. constructor(private http: HttpClient) { }
776.
777. ngOnInit(): void {
778.     this.http.get('https://api.exemple.com/data')
779.       .subscribe(response => {
780.         this.data = response;
781.       });
782. }
783. }

784. ```
785.

786. ### Les opérateurs RxJS

787.
788. RxJS offre de nombreux opérateurs pour manipuler les observables :
789.
790. 1. **map** : Pour transformer des valeurs.
791. 2. **filter** : Pour filtrer les valeurs.
792. 3. **mergeMap** : Pour aplatir et combiner des observables.
793. 4. **debounceTime** : Pour réguler le flux d’événements.
794. 5. **switchMap** : Pour annuler d’anciennes souscriptions en cas de nouvel événement.
795.
796. **Exemple avec l’opérateur map :**
797.

798. ```typescript
799. import { map } from 'rxjs/operators';
800.
801. this.http.get('<https://api.exemple.com/data>')
802. .pipe(map((response: any) => response.data))
803. .subscribe(data => console.log(data));

804. ```
805.

806. ### Bonnes pratiques en programmation asynchrone

807.
808. 1. Toujours se désabonner dans `ngOnDestroy()` pour éviter les fuites de mémoire.
809. 2. Utiliser des opérateurs comme `takeUntil` pour gérer la durée de vie des abonnements.
810. 3. Préférer les observables pour les opérations pouvant émettre plusieurs valeurs.
811. 4. Gérer les erreurs avec les opérateurs `catchError` et `retry`.
812.

813. #### Exemple d’utilisation de takeUntil

814.

815. ```typescript
816. import { Subject } from 'rxjs';
817. import { takeUntil } from 'rxjs/operators';
818.
819. export class ExempleComponent implements OnDestroy {
820. private unsubscribe$ = new Subject<void>();
821.
822. constructor(private http: HttpClient) { }
823.
824. ngOnInit(): void {
825.     this.http.get('https://api.exemple.com/data')
826.       .pipe(takeUntil(this.unsubscribe$))
827.       .subscribe(data => console.log(data));
828. }
829.
830. ngOnDestroy(): void {
831.     this.unsubscribe$.next();
832.     this.unsubscribe$.complete();
833. }
834. }

835. ```
836.

837. #### Points supplémentaires sur les observables

838.
839. 1. Les observables facilitent la gestion des flux événementiels.
840. 2. Ils permettent une composition fluide des opérations asynchrones.
841. 3. L’utilisation combinée d’opérateurs permet d’optimiser les performances.
842. 4. Adopte une approche réactive pour construire des applications performantes.
843.
844. ----------------------------------------------------------------
845.

846. ## 13. Conclusion

847.
848. Cette fiche de révision couvre en profondeur les concepts fondamentaux d’Angular abordés durant la semaine 13 du cours Web02.
849.

850. ### Récapitulatif des points essentiels

851.
852. 1. **Composants** : La base de toute appli Angular, avec un cycle de vie riche.
853. 2. **Transfert de Données** : Utilisation de `@Input()`, `@Output()` et des services pour la communication inter-composants.
854. 3. **Interpolation** : Méthode simple pour insérer des données dans le template.
855. 4. **Property Binding** : Liaison dynamique des attributs HTML.
856. 5. **Data Binding** : Combinaison des différents types de binding pour synchroniser modèle et vue.
857. 6. **Event Binding** : Gestion des interactions utilisateurs.
858. 7. **Directives** : Extensions du comportement du DOM via des directives structurelles et attributs.
859. 8. **Pipes** : Transformation et formatage des données dans les templates.
860. 9. **Services** : Partage de logique métier et d’état via l’injection de dépendance.
861. 10. **Routing** : Navigation et gestion des vues avec le module de routage.
862. 11. **Programmation Asynchrone et Observables** : Utilisation d’RxJS pour gérer les flux de données asynchrones.
863.

864. ### Derniers conseils pour une maîtrise d’Angular

865.
866. - **Pratique régulière** : Expérimente chaque concept dans des projets réels ou des exercices.
867. - **Lire la documentation officielle** : Angular dispose d’une documentation riche et constamment mise à jour.
868. - **Participer à la communauté** : Les forums et GitHub sont d’excellents endroits pour échanger sur les meilleures pratiques.
869. - **Tester son code** : Utilise des tests unitaires et d’intégration pour assurer la robustesse de ton application.
870. - **Rester curieux** : Angular évolue régulièrement, donc reste informé des nouveautés.
871.

872. ### Quelques ressources supplémentaires

873.
874. 1. [Documentation Angular](https://angular.io/docs)
875. 2. [Tutoriel Angular sur Angular University](https://angular-university.io/)
876. 3. [Guide complet sur RxJS](https://rxjs-dev.firebaseapp.com/)
877. 4. [Angular CLI Documentation](https://angular.io/cli)
878.

879. ### Mot de la fin

880.
881. La compréhension de ces concepts te permettra de développer des applications web robustes et évolutives. Ne néglige aucun détail, car la maîtrise d’Angular passe par la compréhension de chaque petite pièce du puzzle.
882.
883. Merci d’avoir parcouru cette fiche de révision détaillée. N’oublie pas que la pratique et la révision régulière sont les clés de la réussite en développement.
884.
885. ---
886.

887. ## Annexes et Exercices Complémentaires

888.

889. ### Exercice 1 : Créer un composant interactif

890.
891. **Objectif :** Créer un composant affichant une liste de produits avec la possibilité de filtrer cette liste via un input.  
892. **Instructions :**  
893. a. Crée un composant `ProductListComponent`.  
894. b. Utilise l’interpolation pour afficher le nom de chaque produit.  
895. c. Ajoute un `@Input()` pour passer la liste des produits.  
896. d. Implémente un champ de recherche avec le two-way binding pour filtrer les produits.  
897. e. Affiche dynamiquement la liste filtrée en utilisant `*ngFor`.
898.

899. ### Exercice 2 : Communication entre Composants

900.
901. **Objectif :** Mettre en place une communication bidirectionnelle entre un composant parent et un composant enfant.  
902. **Instructions :**  
903. a. Crée un composant parent `DashboardComponent` et un composant enfant `NotificationComponent`.  
904. b. Utilise `@Input()` pour envoyer un message du parent à l’enfant.  
905. c. Dans le composant enfant, ajoute un bouton qui, via un `@Output()`, émet un événement lorsque l’utilisateur clique dessus.  
906. d. Dans le composant parent, récupère cet événement et affiche une alerte.
907.

908. ### Exercice 3 : Création d’une Directive Personnalisée

909.
910. **Objectif :** Créer une directive personnalisée qui change le style d’un élément lors du survol.  
911. **Instructions :**  
912. a. Crée une directive `HighlightDirective` à partir d’un `@Directive()`.  
913. b. Utilise `@HostListener` pour détecter les événements `mouseenter` et `mouseleave`.  
914. c. Applique la directive sur divers éléments de ton application pour tester son comportement.
915.

916. ### Exercice 4 : Utilisation de Pipes Personnalisés

917.
918. **Objectif :** Créer un pipe personnalisé permettant de formater une chaîne en inversant son ordre.  
919. **Instructions :**  
920. a. Crée un pipe `ReversePipe`.  
921. b. Implémente la fonction de transformation qui inverse la chaîne donnée.  
922. c. Teste le pipe dans un template sur différents textes.
923.

924. ### Exercice 5 : Configuration du Routing

925.
926. **Objectif :** Mettre en place un système de navigation entre plusieurs vues.  
927. **Instructions :**  
928. a. Configure les routes pour naviguer entre une page d’accueil, une page "À propos" et une page "Contact".  
929. b. Utilise `<router-outlet></router-outlet>` dans ton composant principal.  
930. c. Implémente des liens de navigation avec `routerLink`.
931.

932. ### Exercice 6 : Programmation Asynchrone avec Observables

933.
934. **Objectif :** Récupérer des données depuis une API et les afficher dans un composant.  
935. **Instructions :**  
936. a. Crée un service `DataService` qui utilise `HttpClient` pour faire une requête GET.  
937. b. Dans un composant, abonne-toi à cet observable pour afficher les données dans une liste.  
938. c. Utilise des opérateurs RxJS pour transformer les données avant l’affichage.
939.

940. ### Exercice 7 : Test Unitaire d’un Service

941.
942. **Objectif :** Écrire un test unitaire pour valider le fonctionnement d’un service.  
943. **Instructions :**  
944. a. Crée un service `MathService` avec une méthode `addition(a: number, b: number): number`.  
945. b. Écris un test unitaire avec Jasmine/Karma pour vérifier que la méthode retourne la somme correcte.  
946. c. Assure-toi que le service est correctement injecté dans le test.
947.

948. ### Exercice 8 : Gestion d’Erreur dans les Observables

949.
950. **Objectif :** Mettre en place une gestion d’erreur dans un appel HTTP.  
951. **Instructions :**  
952. a. Dans ton service `DataService`, utilise l’opérateur `catchError` pour gérer les erreurs.
953. b. Affiche un message d’erreur dans le composant si l’API renvoie une erreur.
954. c. Utilise `retry` pour retenter l’appel en cas d’échec.
955.

956. ### Exercice 9 : Optimisation avec Lazy-Loading

957.
958. **Objectif :** Implémenter le lazy-loading pour un module spécifique de ton application.  
959. **Instructions :**  
960. a. Crée un module `AdminModule` avec ses propres composants.
961. b. Configure le routing pour charger ce module de manière paresseuse.
962. c. Vérifie l’améli
