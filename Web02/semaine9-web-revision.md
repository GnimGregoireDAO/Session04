# Fiche de Révision - Semaine 9 Web

## 1. Création d'une API REST

### 1.1 Principes REST

- **Caractéristiques** :
  - Stateless (Sans état)
  - Interface uniforme
  - Ressources identifiables
  - Manipulations via représentations
  - Messages auto-descriptifs
  - HATEOAS (Hypermedia)

### 1.2 Implementation avec Spring Boot

```java
@RestController
@RequestMapping("/api/v1")
public class UserRestController {
    private final UserService userService;

    @GetMapping("/users")
    public ResponseEntity<List<User>> getAllUsers() {
        return ResponseEntity.ok(userService.findAll());
    }

    @GetMapping("/users/{id}")
    public ResponseEntity<User> getUser(@PathVariable Long id) {
        return userService.findById(id)
            .map(ResponseEntity::ok)
            .orElse(ResponseEntity.notFound().build());
    }

    @PostMapping("/users")
    public ResponseEntity<User> createUser(@Valid @RequestBody UserDTO userDTO) {
        User user = userService.save(userDTO.toUser());
        URI location = ServletUriComponentsBuilder
            .fromCurrentRequest()
            .path("/{id}")
            .buildAndExpand(user.getId())
            .toUri();
        return ResponseEntity.created(location).body(user);
    }

    @PutMapping("/users/{id}")
    public ResponseEntity<User> updateUser(
            @PathVariable Long id, 
            @Valid @RequestBody UserDTO userDTO) {
        return userService.update(id, userDTO.toUser())
            .map(ResponseEntity::ok)
            .orElse(ResponseEntity.notFound().build());
    }

    @DeleteMapping("/users/{id}")
    public ResponseEntity<Void> deleteUser(@PathVariable Long id) {
        if (userService.delete(id)) {
            return ResponseEntity.noContent().build();
        }
        return ResponseEntity.notFound().build();
    }
}
```

### 1.3 DTOs et Validation

```java
@Data
public class UserDTO {
    @NotBlank(message = "Le nom est obligatoire")
    private String name;

    @Email(message = "Email invalide")
    private String email;

    @Size(min = 8, message = "Le mot de passe doit contenir au moins 8 caractères")
    private String password;

    public User toUser() {
        User user = new User();
        user.setName(this.name);
        user.setEmail(this.email);
        user.setPassword(this.password);
        return user;
    }
}
```

### 1.4 Gestion des Erreurs

```java
@RestControllerAdvice
public class RestExceptionHandler {
    
    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<Map<String, List<String>>> handleValidationErrors(
            MethodArgumentNotValidException ex) {
        List<String> errors = ex.getBindingResult()
            .getFieldErrors()
            .stream()
            .map(FieldError::getDefaultMessage)
            .collect(Collectors.toList());
        return ResponseEntity
            .badRequest()
            .body(Collections.singletonMap("errors", errors));
    }

    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<Map<String, String>> handleNotFound(
            ResourceNotFoundException ex) {
        return ResponseEntity
            .status(HttpStatus.NOT_FOUND)
            .body(Collections.singletonMap("error", ex.getMessage()));
    }
}
```

## 2. Test avec Postman

### 2.1 Configuration des Collections

```json
{
  "info": {
    "name": "API Users",
    "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
  },
  "item": [
    {
      "name": "Get All Users",
      "request": {
        "method": "GET",
        "url": "http://localhost:8080/api/v1/users",
        "headers": {
          "Accept": "application/json"
        }
      }
    },
    {
      "name": "Create User",
      "request": {
        "method": "POST",
        "url": "http://localhost:8080/api/v1/users",
        "headers": {
          "Content-Type": "application/json"
        },
        "body": {
          "mode": "raw",
          "raw": "{\"name\":\"John\",\"email\":\"john@example.com\"}"
        }
      }
    }
  ]
}
```

### 2.2 Tests Automatisés dans Postman

```javascript
// Test après création d'utilisateur
pm.test("Status code is 201", () => {
    pm.response.to.have.status(201);
});

pm.test("User is created", () => {
    const response = pm.response.json();
    pm.expect(response.name).to.eql("John");
    pm.expect(response.email).to.eql("john@example.com");
});

// Variables d'environnement
pm.environment.set("user_id", response.id);
```

## 3. Communication avec Applications Externes

### 3.1 RestTemplate

```java
@Service
public class ExternalServiceClient {
    private final RestTemplate restTemplate;
    private final String baseUrl;

    public ExternalServiceClient(RestTemplate restTemplate, 
                               @Value("${api.base-url}") String baseUrl) {
        this.restTemplate = restTemplate;
        this.baseUrl = baseUrl;
    }

    public User getExternalUser(Long id) {
        return restTemplate.getForObject(
            baseUrl + "/users/{id}", 
            User.class, 
            id
        );
    }

    public List<User> getAllExternalUsers() {
        ResponseEntity<List<User>> response = restTemplate.exchange(
            baseUrl + "/users",
            HttpMethod.GET,
            null,
            new ParameterizedTypeReference<List<User>>() {}
        );
        return response.getBody();
    }
}
```

### 3.2 WebClient (Reactive)

```java
@Service
public class ReactiveExternalService {
    private final WebClient webClient;

    public ReactiveExternalService(WebClient.Builder webClientBuilder, 
                                 @Value("${api.base-url}") String baseUrl) {
        this.webClient = webClientBuilder.baseUrl(baseUrl).build();
    }

    public Mono<User> getUser(Long id) {
        return webClient.get()
            .uri("/users/{id}", id)
            .retrieve()
            .bodyToMono(User.class);
    }

    public Flux<User> getAllUsers() {
        return webClient.get()
            .uri("/users")
            .retrieve()
            .bodyToFlux(User.class);
    }
}
```

## Points à retenir

1. **API REST**
   - Utiliser les bons verbes HTTP
   - Structurer les URLs de manière logique
   - Implémenter la validation
   - Gérer les erreurs correctement
   - Utiliser les codes HTTP appropriés

2. **Postman**
   - Organiser les collections
   - Utiliser les environnements
   - Écrire des tests automatisés
   - Documenter les requêtes
   - Partager les collections

3. **Communication externe**
   - Gérer les timeouts
   - Implémenter la résilience
   - Utiliser le circuit breaker pattern
   - Logger les appels externes
   - Gérer les erreurs de communication
