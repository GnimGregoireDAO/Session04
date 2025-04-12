# Journal de Recherche - 11 Avril 2025

## Gestion des valeurs absentes avec Optional

La classe `Optional` en Java permet de gérer les valeurs absentes de manière élégante en fournissant plusieurs méthodes utiles :

- `isPresent()` - vérifie si une valeur existe
- `ifPresent()` - exécute une action si la valeur existe
- `orElse()` - fournit une valeur par défaut
- `orElseThrow()` - lance une exception si la valeur est absente

### Exemple d'implémentation

```java
public Optional<String> findUsernameById(int id) {
    if (id == 1) {
        return Optional.of("Grégoire");
    } else {
        return Optional.empty();
    }
}
```

### Utilisation

```java
Optional<String> username = findUsernameById(1);
username.ifPresent(System.out::println); // Affiche "Grégoire" si présent
System.out.println(username.orElse("Utilisateur inconnu")); // Valeur par défaut si absent
```

## Gestion des dates et fuseaux horaires avec ZonedDateTime

La classe `ZonedDateTime` en Java est utilisée pour représenter une **date et une heure spécifiques avec un fuseau horaire**. Elle est utile pour les applications où la gestion des différents fuseaux horaires est critique.

### Méthodes importantes
- `now()` : Obtenir la date et l'heure actuelles avec le fuseau par défaut.
- `of()` : Créer un objet `ZonedDateTime` avec des valeurs spécifiques.
- `withZoneSameInstant()` : Convertir l'objet vers un autre fuseau horaire tout en conservant l'instant précis.

### Exemple d'implémentation

```java
import java.time.ZonedDateTime;
import java.time.ZoneId;

public class ZonedDateTimeExample {
    public static void main(String[] args) {
        ZonedDateTime currentTime = ZonedDateTime.now(); // Date et heure actuelles avec fuseau par défaut
        System.out.println("Heure actuelle : " + currentTime);

        ZonedDateTime parisTime = currentTime.withZoneSameInstant(ZoneId.of("Europe/Paris"));
        System.out.println("Heure à Paris : " + parisTime);
    }
}
```

### Applications
- Conversion automatique des dates entre fuseaux horaires.
- Gestion des dates dans les systèmes distribués.
- Horodatage précis pour les bases de données.

## Gestion de la pagination avec Page et Pageable en Spring Boot

Les classes `Page` et `Pageable` sont utilisées en **Spring Boot** pour gérer la pagination, particulièrement dans les bases de données. Elles sont très utiles pour afficher de grandes quantités de données par "pages".

### Classe `Page`
La classe `Page` est une interface qui contient une partie d'une collection de données paginées. Elle fournit des informations comme :
- `getTotalPages()` : Nombre total de pages.
- `getTotalElements()` : Nombre total d'éléments.
- `getContent()` : Les données de la page actuelle.
- `map(Function)` : Permet de transformer les données dans un autre format.

### Classe `Pageable`
`Pageable` est une interface qui définit la taille de la page, le numéro de page actuel, et les critères de tri.

### Exemple d'utilisation
#### Repository
```java
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;

public interface ProductRepository extends JpaRepository<Product, Integer> {
    Page<Product> findAll(Pageable pageable);
}
```

#### Service
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.PageRequest;
import org.springframework.stereotype.Service;

@Service
public class ProductService {
    @Autowired
    private ProductRepository productRepository;

    public Page<Product> getPaginatedProducts(int page, int size) {
        return productRepository.findAll(PageRequest.of(page, size));
    }
}
```

#### Contrôleur
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.domain.Page;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/products")
public class ProductController {
    @Autowired
    private ProductService productService;

    @GetMapping
    public Page<Product> getProducts(@RequestParam(defaultValue = "0") int page,
                                      @RequestParam(defaultValue = "10") int size) {
        return productService.getPaginatedProducts(page, size);
    }
}
```

### Vue Thymeleaf (HTML)
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Produits paginés</title>
</head>
<body>
    <h1>Liste des produits</h1>
    <ul>
        <li th:each="product : ${products}">
            <p th:text="${product.name}">Nom</p>
            <p th:text="${product.description}">Description</p>
        </li>
    </ul>

    <!-- Navigation entre les pages -->
    <div>
        <a th:if="${currentPage > 0}" th:href="@{/products(page=${currentPage - 1}, size=10)}">Précédent</a>
        <a th:if="${currentPage < totalPages - 1}" th:href="@{/products(page=${currentPage + 1}, size=10)}">Suivant</a>
    </div>
</body>
</html>
```

## Conclusion
- **`Optional`** permet de gérer les valeurs nulles de manière élégante.
- **`ZonedDateTime`** est idéal pour manipuler les dates avec fuseaux horaires dans des applications globales.
- **`Page` et `Pageable`** rendent la pagination simple et performante, particulièrement en combinaison avec Spring Boot et des vues comme Thymeleaf.
