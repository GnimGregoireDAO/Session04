# Semaine 12 - Révision Web02

## Programmation asynchrone dans Angular

### Concepts fondamentaux

- **Opérations asynchrones** : Exécution de code sans bloquer le thread principal
- **Event loop** : Mécanisme qui permet à JavaScript de gérer les opérations asynchrones
- **Callbacks** : Fonctions passées en paramètre et exécutées ultérieurement
- **Single-threaded** : JavaScript s'exécute sur un seul thread mais peut gérer plusieurs opérations grâce à l'asynchronicité
- **Non-bloquant** : Les opérations longues sont déléguées à l'environnement d'exécution (navigateur, Node.js)

### Promesses (Promise)

- Objet représentant une valeur qui pourrait être disponible maintenant, dans le futur, ou jamais
- États: **pending**, **fulfilled**, **rejected**
- Méthodes: `.then()`, `.catch()`, `.finally()`
- **Promise.all()** : Attend que toutes les promesses soient résolues
- **Promise.race()** : Retourne la première promesse résolue
- **Promise.allSettled()** : Attend que toutes les promesses soient résolues ou rejetées
- Exemple:

  ```typescript
  const promesse = new Promise<string>((resolve, reject) => {
    // Opération asynchrone
    setTimeout(() => resolve('Données reçues'), 1000);
  });
  
  promesse
    .then(resultat => console.log(resultat))
    .catch(erreur => console.error(erreur));
  ```

### async/await

- Syntaxe permettant d'écrire du code asynchrone de manière synchrone
- Une fonction async retourne toujours une Promise
- await permet d'attendre la résolution d'une Promise
- Gestion des erreurs avec try/catch
- Exemple:

  ```typescript
  async function chargerDonnees(): Promise<string> {
    try {
      const response = await fetch('https://api.exemple.com/data');
      const data = await response.json();
      return data;
    } catch (error) {
      console.error('Erreur lors du chargement:', error);
      throw error;
    }
  }
  
  // Utilisation
  async function afficherDonnees() {
    try {
      const donnees = await chargerDonnees();
      console.log(donnees);
    } catch (error) {
      // Gestion d'erreur
    }
  }
  ```

### Observables (RxJS)

- **Observable** : Flux de données sur lequel on peut s'abonner
- Plus puissants que les Promesses: peuvent émettre plusieurs valeurs au fil du temps
- Méthodes importantes: `subscribe()`, `pipe()`, `map()`, `filter()`
- **Lazy** : Un Observable ne s'exécute que lorsqu'on y souscrit
- **Cold Observable** : Émet les mêmes valeurs pour chaque souscripteur
- **Hot Observable** : Émet les mêmes valeurs pour tous les souscripteurs en même temps
- Exemple:

  ```typescript
  import { Observable, of } from 'rxjs';
  import { map } from 'rxjs/operators';
  
  const observable = of(1, 2, 3).pipe(
    map(x => x * 2)
  );
  
  observable.subscribe({
    next: valeur => console.log(valeur), // 2, 4, 6
    error: err => console.error(err),
    complete: () => console.log('Terminé')
  });
  ```

### Types de Subjects dans RxJS

- **Subject** : À la fois Observable et Observer, permet de diffuser des valeurs à plusieurs souscripteurs
- **BehaviorSubject** : Stocke la dernière valeur émise et la fournit aux nouveaux souscripteurs
- **ReplaySubject** : Stocke un nombre défini de valeurs et les retransmet aux nouveaux souscripteurs
- **AsyncSubject** : N'émet que la dernière valeur lorsque l'Observable est complété
- Exemple:

  ```typescript
  import { BehaviorSubject } from 'rxjs';
  
  // Initialisation avec une valeur par défaut
  const dataSubject = new BehaviorSubject<string[]>([]);
  
  // Émission de nouvelles valeurs
  dataSubject.next(['valeur1', 'valeur2']);
  
  // Souscription
  dataSubject.subscribe(data => {
    console.log('Données actuelles:', data);
  });
  
  // Obtenir la valeur actuelle sans souscription
  const valeurCourante = dataSubject.value;
  ```

### Opérateurs RxJS essentiels

1. **Transformation**
   - `map`: Transforme chaque valeur émise
   - `mergeMap`/`flatMap`: Mapping puis fusion des Observables résultants
   - `switchMap`: Passe à un nouvel Observable, annulant l'ancien
   - `concatMap`: Garde l'ordre des Observables
   - `exhaustMap`: Ignore les nouvelles émissions pendant le traitement de l'Observable actuel

2. **Filtrage**
   - `filter`: Ne laisse passer que les valeurs respectant un prédicat
   - `take`: Prend un nombre limité de valeurs
   - `skip`: Saute un nombre défini de valeurs
   - `debounceTime`: Émet une valeur après un délai sans nouvelle émission
   - `throttleTime`: Limite le nombre d'émissions par unité de temps
   - `distinctUntilChanged`: N'émet que si la valeur est différente de la précédente

3. **Combinaison**
   - `combineLatest`: Combine les dernières valeurs de plusieurs Observables
   - `merge`: Fusionne plusieurs Observables
   - `concat`: Concatène des Observables en séquence
   - `forkJoin`: Similaire à Promise.all(), attend que tous les Observables complètent
   - `zip`: Combine les valeurs correspondantes de plusieurs Observables

4. **Erreurs**
   - `catchError`: Gère les erreurs
   - `retry`: Réessaye en cas d'erreur
   - `retryWhen`: Contrôle fin des tentatives

5. **Utilitaires**
   - `tap`: Exécute des effets secondaires sans modifier le flux
   - `finalize`: Exécute du code à la fin de l'Observable
   - `delay`: Retarde les émissions

## AJAX et JSON dans Angular

### HttpClient

- Service intégré à Angular pour effectuer des requêtes HTTP
- Retourne des Observables, facilitant les opérations asynchrones
- Gère automatiquement la transformation JSON
- Support pour le typage générique

### Méthodes principales

- `get<T>()`: Récupérer des données
- `post<T>()`: Envoyer des données
- `put<T>()`: Mettre à jour des données existantes
- `delete<T>()`: Supprimer des données
- `patch<T>()`: Mise à jour partielle

### Options des requêtes HTTP

```typescript
// Paramètres d'URL
this.http.get<T>(url, {
  params: new HttpParams()
    .set('page', '1')
    .set('limit', '10')
});

// En-têtes personnalisés
this.http.get<T>(url, {
  headers: new HttpHeaders()
    .set('Authorization', 'Bearer ' + token)
    .set('Content-Type', 'application/json')
});

// Gestion des réponses complètes
this.http.get<T>(url, {
  observe: 'response'
}).subscribe(response => {
  // Accès aux en-têtes, status, etc.
  console.log(response.headers);
  console.log(response.status);
  // Corps de la réponse
  console.log(response.body);
});
```

### Intercepteurs HTTP

- Permettent d'intercepter et modifier les requêtes/réponses HTTP
- Utiles pour l'authentification, la gestion d'erreurs, etc.
- Exemple d'intercepteur d'authentification:

```typescript
@Injectable()
export class AuthInterceptor implements HttpInterceptor {
  constructor(private authService: AuthService) {}

  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    // Ajoute le token d'authentification si disponible
    const token = this.authService.getToken();
    if (token) {
      const authReq = req.clone({
        headers: req.headers.set('Authorization', `Bearer ${token}`)
      });
      return next.handle(authReq);
    }
    return next.handle(req);
  }
}

// Dans le module:
@NgModule({
  providers: [
    { provide: HTTP_INTERCEPTORS, useClass: AuthInterceptor, multi: true }
  ]
})
```

### Gestion des erreurs HTTP

```typescript
getItems(): Observable<Item[]> {
  return this.http.get<Item[]>(this.apiUrl).pipe(
    retry(3), // Réessaie jusqu'à 3 fois
    catchError(this.handleError)
  );
}

private handleError(error: HttpErrorResponse): Observable<never> {
  if (error.error instanceof ErrorEvent) {
    // Erreur côté client
    console.error('Erreur client:', error.error.message);
  } else {
    // Erreur côté serveur
    console.error(
      `Code d'erreur ${error.status}, ` +
      `Message: ${error.error.message}`
    );
  }
  return throwError(() => new Error('Quelque chose a mal tourné; veuillez réessayer plus tard.'));
}
```

### Exemple de service Angular complet

```typescript
import { Injectable } from '@angular/core';
import { HttpClient, HttpParams, HttpErrorResponse } from '@angular/common/http';
import { Observable, throwError, BehaviorSubject } from 'rxjs';
import { catchError, retry, tap, map, switchMap, shareReplay } from 'rxjs/operators';

interface PaginationParams {
  page: number;
  limit: number;
  sort?: string;
}

interface ApiResponse<T> {
  data: T[];
  total: number;
  page: number;
  limit: number;
}

@Injectable({
  providedIn: 'root'
})
export class ProduitService {
  private apiUrl = 'https://api.exemple.com/produits';
  private cacheTimeout = 60000; // 1 minute en millisecondes
  private produitCache = new Map<string, {data: Observable<Produit[]>, timestamp: number}>();
  private produitsSubject = new BehaviorSubject<Produit[]>([]);
  
  // Observable public pour les composants
  produits$ = this.produitsSubject.asObservable();

  constructor(private http: HttpClient) { }

  getProduits(params?: PaginationParams): Observable<Produit[]> {
    // Création de la clé de cache
    const cacheKey = this.createCacheKey(params);
    const currentTime = Date.now();
    
    // Vérification du cache
    if (this.produitCache.has(cacheKey)) {
      const cachedData = this.produitCache.get(cacheKey);
      if (cachedData && currentTime - cachedData.timestamp < this.cacheTimeout) {
        return cachedData.data;
      }
      // Cache expiré, suppression
      this.produitCache.delete(cacheKey);
    }

    // Construction des paramètres HTTP
    let httpParams = new HttpParams();
    if (params) {
      httpParams = httpParams
        .set('page', params.page.toString())
        .set('limit', params.limit.toString());
      
      if (params.sort) {
        httpParams = httpParams.set('sort', params.sort);
      }
    }

    // Requête HTTP avec gestion de cache
    const request = this.http.get<ApiResponse<Produit>>(this.apiUrl, { params: httpParams }).pipe(
      retry(2),
      map(response => response.data),
      tap(produits => this.produitsSubject.next(produits)),
      catchError(this.handleError),
      shareReplay(1)
    );

    // Mise en cache
    this.produitCache.set(cacheKey, {
      data: request,
      timestamp: currentTime
    });

    return request;
  }

  getProduitById(id: number): Observable<Produit> {
    return this.http.get<Produit>(`${this.apiUrl}/${id}`).pipe(
      catchError(this.handleError)
    );
  }

  ajouterProduit(produit: Produit): Observable<Produit> {
    return this.http.post<Produit>(this.apiUrl, produit).pipe(
      tap(nouveauProduit => {
        // Mise à jour du BehaviorSubject
        const produitsCourants = this.produitsSubject.value;
        this.produitsSubject.next([...produitsCourants, nouveauProduit]);
        // Invalidation du cache
        this.invalidateCache();
      }),
      catchError(this.handleError)
    );
  }

  mettreAJourProduit(id: number, produit: Produit): Observable<Produit> {
    return this.http.put<Produit>(`${this.apiUrl}/${id}`, produit).pipe(
      tap(produitMaj => {
        // Mise à jour du BehaviorSubject
        const produitsCourants = this.produitsSubject.value;
        const index = produitsCourants.findIndex(p => p.id === id);
        if (index !== -1) {
          produitsCourants[index] = produitMaj;
          this.produitsSubject.next([...produitsCourants]);
        }
        // Invalidation du cache
        this.invalidateCache();
      }),
      catchError(this.handleError)
    );
  }

  supprimerProduit(id: number): Observable<void> {
    return this.http.delete<void>(`${this.apiUrl}/${id}`).pipe(
      tap(() => {
        // Mise à jour du BehaviorSubject
        const produitsCourants = this.produitsSubject.value;
        const produitsFiltres = produitsCourants.filter(p => p.id !== id);
        this.produitsSubject.next(produitsFiltres);
        // Invalidation du cache
        this.invalidateCache();
      }),
      catchError(this.handleError)
    );
  }

  // Méthodes privées
  private createCacheKey(params?: PaginationParams): string {
    if (!params) return 'default';
    return `page=${params.page}-limit=${params.limit}-sort=${params.sort || 'default'}`;
  }

  private invalidateCache(): void {
    this.produitCache.clear();
  }

  private handleError(error: HttpErrorResponse): Observable<never> {
    let errorMessage = 'Une erreur inconnue est survenue';
    
    if (error.error instanceof ErrorEvent) {
      // Erreur côté client
      errorMessage = `Erreur: ${error.error.message}`;
    } else {
      // Erreur côté serveur
      switch(error.status) {
        case 404:
          errorMessage = 'Ressource non trouvée';
          break;
        case 403:
          errorMessage = 'Accès interdit';
          break;
        case 401:
          errorMessage = 'Non autorisé';
          break;
        case 400:
          errorMessage = `Requête incorrecte: ${error.error.message || error.message}`;
          break;
        case 500:
          errorMessage = 'Erreur serveur';
          break;
      }
    }
    
    console.error('Erreur dans le service produit:', errorMessage);
    return throwError(() => new Error(errorMessage));
  }
}
```

### Exemple complet: Component utilisant un service

```typescript
import { Component, OnInit, OnDestroy } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';
import { Subscription, Observable, combineLatest, Subject, of } from 'rxjs';
import { ProduitService } from './produit.service';
import { CategorieService } from './categorie.service';
import { debounceTime, distinctUntilChanged, switchMap, map, catchError, startWith, takeUntil } from 'rxjs/operators';

interface ProduitFiltre {
  terme: string;
  categorie: string;
  prixMin: number;
  prixMax: number;
  disponible: boolean | null;
}

@Component({
  selector: 'app-liste-produits',
  template: `
    <div class="container">
      <h2>Liste des produits</h2>
      
      <!-- Formulaire de filtrage -->
      <form [formGroup]="filtreForm" class="filtre-form">
        <div class="row">
          <div class="col">
            <input 
              type="text" 
              formControlName="terme" 
              class="form-control" 
              placeholder="Rechercher..."
            />
          </div>
          <div class="col">
            <select formControlName="categorie" class="form-control">
              <option value="">Toutes les catégories</option>
              <option *ngFor="let cat of categories$ | async" [value]="cat.id">
                {{cat.nom}}
              </option>
            </select>
          </div>
          <div class="col">
            <input 
              type="number" 
              formControlName="prixMin" 
              class="form-control" 
              placeholder="Prix min"
            />
          </div>
          <div class="col">
            <input 
              type="number" 
              formControlName="prixMax" 
              class="form-control" 
              placeholder="Prix max"
            />
          </div>
          <div class="col form-check">
            <input 
              type="checkbox" 
              formControlName="disponible" 
              class="form-check-input" 
              id="disponibleCheck"
            />
            <label class="form-check-label" for="disponibleCheck">
              En stock uniquement
            </label>
          </div>
          <div class="col">
            <button 
              type="button" 
              class="btn btn-secondary" 
              (click)="reinitialiserFiltres()"
            >
              Réinitialiser
            </button>
          </div>
        </div>
      </form>
      
      <!-- Indicateur de chargement -->
      <div *ngIf="chargement$ | async" class="spinner-border" role="status">
        <span class="sr-only">Chargement...</span>
      </div>
      
      <!-- Message d'erreur -->
      <div *ngIf="erreur$ | async as erreur" class="alert alert-danger">
        Erreur: {{erreur}}
      </div>
      
      <!-- Liste des produits -->
      <div class="row row-cols-1 row-cols-md-3 g-4">
        <div class="col" *ngFor="let produit of produitsFiltres$ | async">
          <div class="card h-100">
            <div class="card-body">
              <h5 class="card-title">{{produit.nom}}</h5>
              <p class="card-text">{{produit.description}}</p>
              <p class="prix">{{produit.prix | currency:'EUR'}}</p>
              <p *ngIf="produit.enStock" class="badge bg-success">En stock</p>
              <p *ngIf="!produit.enStock" class="badge bg-danger">Rupture de stock</p>
            </div>
            <div class="card-footer">
              <button 
                class="btn btn-primary" 
                [disabled]="!produit.enStock"
                (click)="ajouterAuPanier(produit)"
              >
                Ajouter au panier
              </button>
              <button 
                class="btn btn-info ms-2" 
                (click)="voirDetails(produit.id)"
              >
                Détails
              </button>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Pagination -->
      <div class="d-flex justify-content-center mt-4">
        <nav>
          <ul class="pagination">
            <li class="page-item" [class.disabled]="currentPage === 1">
              <button class="page-link" (click)="changerPage(currentPage - 1)">Précédent</button>
            </li>
            <li class="page-item" *ngFor="let page of pages" [class.active]="page === currentPage">
              <button class="page-link" (click)="changerPage(page)">{{page}}</button>
            </li>
            <li class="page-item" [class.disabled]="currentPage === totalPages">
              <button class="page-link" (click)="changerPage(currentPage + 1)">Suivant</button>
            </li>
          </ul>
        </nav>
      </div>
    </div>
  `,
  styles: [`
    .filtre-form {
      margin-bottom: 2rem;
      padding: 1rem;
      background-color: #f8f9fa;
      border-radius: 0.25rem;
    }
    .prix {
      font-weight: bold;
      font-size: 1.2rem;
      color: #dc3545;
    }
  `]
})
export class ListeProduitsComponent implements OnInit, OnDestroy {
  filtreForm: FormGroup;
  produits: Produit[] = [];
  
  // Streams
  private destroy$ = new Subject<void>();
  private filtreChange$ = new Subject<ProduitFiltre>();
  private pageChange$ = new Subject<number>();
  private chargementSubject = new Subject<boolean>();
  private erreurSubject = new Subject<string | null>();
  
  // Exposés au template
  chargement$ = this.chargementSubject.asObservable();
  erreur$ = this.erreurSubject.asObservable();
  categories$: Observable<Categorie[]>;
  produitsFiltres$: Observable<Produit[]>;
  
  // Pagination
  currentPage = 1;
  itemsPerPage = 10;
  totalItems = 0;
  totalPages = 0;
  pages: number[] = [];

  constructor(
    private produitService: ProduitService,
    private categorieService: CategorieService,
    private fb: FormBuilder
  ) {
    // Initialisation du formulaire de filtrage
    this.filtreForm = this.fb.group({
      terme: [''],
      categorie: [''],
      prixMin: [null],
      prixMax: [null],
      disponible: [null]
    });
    
    // Observable des catégories
    this.categories$ = this.categorieService.getCategories().pipe(
      catchError(err => {
        this.erreurSubject.next('Impossible de charger les catégories');
        return of([]);
      })
    );
    
    // Combinaison des changements de filtre et de page
    this.produitsFiltres$ = combineLatest([
      this.filtreChange$.pipe(startWith(this.getFiltreActuel())),
      this.pageChange$.pipe(startWith(1))
    ]).pipe(
      debounceTime(300),
      distinctUntilChanged((prev, curr) => 
        JSON.stringify(prev) === JSON.stringify(curr)
      ),
      switchMap(([filtres, page]) => {
        this.chargementSubject.next(true);
        this.erreurSubject.next(null);
        return this.produitService.getProduits({
          page: page,
          limit: this.itemsPerPage,
          ...this.construireParamsAPI(filtres)
        }).pipe(
          map(response => {
            this.totalItems = response.total;
            this.totalPages = Math.ceil(this.totalItems / this.itemsPerPage);
            this.pages = this.genererPages(this.currentPage, this.totalPages);
            return response.data;
          }),
          catchError(err => {
            this.erreurSubject.next('Impossible de charger les produits');
            return of([]);
          }),
          finalize(() => this.chargementSubject.next(false))
        );
      }),
      takeUntil(this.destroy$)
    );
  }

  ngOnInit(): void {
    // Réagir aux changements de formulaire
    this.filtreForm.valueChanges.pipe(
      debounceTime(500),
      takeUntil(this.destroy$)
    ).subscribe(valeurs => {
      this.currentPage = 1; // Retour à la première page lors d'un changement de filtre
      this.filtreChange$.next(valeurs as ProduitFiltre);
    });
    
    // Charger les données initiales
    this.pageChange$.next(1);
  }

  ngOnDestroy(): void {
    // Signaler la destruction pour terminer tous les observables
    this.destroy$.next();
    this.destroy$.complete();
  }
  
  changerPage(page: number): void {
    if (page < 1 || page > this.totalPages) return;
    this.currentPage = page;
    this.pageChange$.next(page);
  }
  
  reinitialiserFiltres(): void {
    this.filtreForm.reset({
      terme: '',
      categorie: '',
      prixMin: null,
      prixMax: null,
      disponible: null
    });
  }
  
  ajouterAuPanier(produit: Produit): void {
    // Implémenter la logique d'ajout au panier
    console.log('Ajout au panier:', produit);
  }
  
  voirDetails(id: number): void {
    // Navigation vers la page de détails (à implémenter)
    console.log('Voir détails du produit:', id);
  }
  
  // Méthodes privées
  private getFiltreActuel(): ProduitFiltre {
    return this.filtreForm.value as ProduitFiltre;
  }
  
  private construireParamsAPI(filtres: ProduitFiltre): any {
    const params: any = {};
    
    if (filtres.terme) {
      params.q = filtres.terme;
    }
    
    if (filtres.categorie) {
      params.categorie = filtres.categorie;
    }
    
    if (filtres.prixMin !== null) {
      params.prixMin = filtres.prixMin;
    }
    
    if (filtres.prixMax !== null) {
      params.prixMax = filtres.prixMax;
    }
    
    if (filtres.disponible !== null) {
      params.enStock = filtres.disponible;
    }
    
    return params;
  }
  
  private genererPages(current: number, total: number): number[] {
    const pages: number[] = [];
    const maxPagesToShow = 5;
    
    if (total <= maxPagesToShow) {
      // Afficher toutes les pages si le nombre total est petit
      for (let i = 1; i <= total; i++) {
        pages.push(i);
      }
    } else {
      // Stratégie pour les grands nombres de pages
      if (current <= 3) {
        // Près du début
        for (let i = 1; i <= 5; i++) {
          pages.push(i);
        }
      } else if (current >= total - 2) {
        // Près de la fin
        for (let i = total - 4; i <= total; i++) {
          pages.push(i);
        }
      } else {
        // Au milieu
        for (let i = current - 2; i <= current + 2; i++) {
          pages.push(i);
        }
      }
    }
    
    return pages;
  }
}
```

### Bonnes pratiques pour les opérations asynchrones dans Angular

1. Toujours typer les réponses HTTP avec des interfaces
2. Utiliser les opérateurs RxJS pour manipuler les données
3. Centraliser les appels API dans des services
4. Gérer les erreurs avec catchError
5. Unsubscribe des Observables avec takeUntil ou utiliser le pipe async
6. Utiliser les intercepteurs HTTP pour la gestion des tokens, des erreurs globales, etc.
7. Implémenter des mécanismes de cache pour réduire les appels serveur
8. Utiliser les Subject/BehaviorSubject pour gérer l'état de l'application
9. Préférer l'approche réactive (Observable) à l'approche impérative
10. Utiliser le pattern Container/Presentational Components pour séparer la logique des vues
