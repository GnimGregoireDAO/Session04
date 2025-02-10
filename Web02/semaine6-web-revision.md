# Fiche de Révision - Semaine 6 Web

## 1. Pourquoi des Frameworks ?

### 1.1 Avantages

- **Productivité** :
  - Réutilisation du code
  - Solutions préconçues pour problèmes communs
  - Génération automatique de code
  - Outils de développement intégrés

- **Qualité** :
  - Code testé et éprouvé
  - Bonnes pratiques intégrées
  - Patterns de conception standardisés
  - Sécurité renforcée

- **Maintenance** :
  - Structure cohérente
  - Documentation extensive
  - Communauté active
  - Mises à jour régulières

### 1.2 Inconvénients

- Courbe d'apprentissage
- Overhead potentiel
- Dépendance au framework
- Contraintes architecturales

## 2. Types de Frameworks

### 2.1 Frameworks Web Full-Stack

- **Exemples** :
  - Spring (Boot)
  - Jakarta EE
  - Play Framework

- **Caractéristiques** :
  - Solution complète
  - Tous les composants intégrés
  - Configuration importante
  - Forte modularité

### 2.2 Micro-Frameworks

- **Exemples** :
  - Spark Java
  - Javalin
  - Micronaut

- **Caractéristiques** :
  - Légers
  - Rapides à démarrer
  - Peu de configuration
  - Focalisés sur des tâches spécifiques

## 3. Framework Spring

### 3.1 Caractéristiques Principales

```plaintext
Spring Framework
├── Core Container
│   ├── Beans
│   ├── Core
│   └── Context
├── Infrastructure
│   ├── AOP
│   └── Transactions
└── Modules
    ├── Web MVC
    ├── Security
    ├── Data
    └── Cloud
```

### 3.2 Principes Fondamentaux

- **Inversion of Control (IoC)**

```java
// Sans IoC
public class UserService {
    private UserRepository repository = new UserRepositoryImpl();
}

// Avec IoC
@Service
public class UserService {
    private final UserRepository repository;
    
    @Autowired
    public UserService(UserRepository repository) {
        this.repository = repository;
    }
}
```

- **Dependency Injection (DI)**

```java
// Types d'injection
@Component
public class MyComponent {
    // Constructor Injection
    private final Service service;
    
    @Autowired
    public MyComponent(Service service) {
        this.service = service;
    }
    
    // Setter Injection
    private OtherService otherService;
    
    @Autowired
    public void setOtherService(OtherService service) {
        this.otherService = service;
    }
    
    // Field Injection (déconseillé)
    @Autowired
    private ThirdService thirdService;
}
```

## 4. Spring Boot

### 4.1 Installation et Configuration

```xml
<!-- pom.xml -->
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.7.0</version>
</parent>

<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
</dependencies>
```

### 4.2 Configuration Application

```yaml
# application.yml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
    username: user
    password: pass
  jpa:
    hibernate:
      ddl-auto: update
server:
  port: 8080
```

### 4.3 Création Application Spring Boot

```java
@SpringBootApplication
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}

@RestController
@RequestMapping("/api")
public class UserController {
    private final UserService userService;
    
    @Autowired
    public UserController(UserService userService) {
        this.userService = userService;
    }
    
    @GetMapping("/users")
    public List<User> getAllUsers() {
        return userService.findAll();
    }
    
    @PostMapping("/users")
    public User createUser(@RequestBody User user) {
        return userService.save(user);
    }
}
```

### 4.4 Structure Projet

```plaintext
src/
├── main/
│   ├── java/
│   │   └── com/example/
│   │       ├── controllers/
│   │       ├── services/
│   │       ├── repositories/
│   │       ├── models/
│   │       └── MyApplication.java
│   └── resources/
│       └── application.yml
└── test/
    └── java/
```

## Points à retenir

1. **Choix d'un Framework**
   - Besoins du projet
   - Taille de l'équipe
   - Expérience existante
   - Support communautaire

2. **Spring Framework**
   - IoC et DI
   - Configuration modulaire
   - Écosystème riche
   - Sécurité intégrée

3. **Spring Boot**
   - Auto-configuration
   - Serveur embarqué
   - Gestion des dépendances
   - Profils de configuration

4. **Bonnes Pratiques**
   - Utiliser Constructor Injection
   - Suivre les conventions
   - Tests automatisés
   - Documentation claire
