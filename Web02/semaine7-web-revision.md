# Fiche de Révision - Semaine 7 Web

## 1. JPA (Java Persistence API)

### 1.1 Concepts Fondamentaux

- **Définition** : Framework ORM (Object-Relational Mapping) pour Java
- **Objectif** : Mapper des objets Java vers des tables de base de données
- **Avantages** :
  - Réduction du code boilerplate
  - Abstraction de la base de données
  - Gestion automatique des relations
  - Cache de premier niveau

### 1.2 Configuration

```xml
<!-- persistence.xml -->
<persistence>
    <persistence-unit name="myPU">
        <provider>org.hibernate.jpa.HibernatePersistenceProvider</provider>
        <properties>
            <property name="javax.persistence.jdbc.url" 
                      value="jdbc:mysql://localhost:3306/db"/>
            <property name="javax.persistence.jdbc.user" value="user"/>
            <property name="javax.persistence.jdbc.password" value="pass"/>
            <property name="hibernate.hbm2ddl.auto" value="update"/>
        </properties>
    </persistence-unit>
</persistence>
```

### 1.3 Annotations JPA

```java
@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(nullable = false, length = 50)
    private String name;
    
    @Email
    @Column(unique = true)
    private String email;
    
    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL)
    private List<Order> orders;
    
    @ManyToMany
    @JoinTable(
        name = "user_roles",
        joinColumns = @JoinColumn(name = "user_id"),
        inverseJoinColumns = @JoinColumn(name = "role_id")
    )
    private Set<Role> roles;
}
```

### 1.4 EntityManager et Transactions

```java
@PersistenceContext
private EntityManager em;

public User saveUser(User user) {
    try {
        em.getTransaction().begin();
        em.persist(user);
        em.getTransaction().commit();
        return user;
    } catch (Exception e) {
        em.getTransaction().rollback();
        throw e;
    }
}

public User findUser(Long id) {
    return em.find(User.class, id);
}

public List<User> findUsersByName(String name) {
    return em.createQuery(
        "SELECT u FROM User u WHERE u.name LIKE :name", 
        User.class)
        .setParameter("name", "%" + name + "%")
        .getResultList();
}
```

## 2. Spring Data JPA

### 2.1 Configuration Spring Boot

```yaml
# application.yml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/db
    username: user
    password: pass
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
    properties:
      hibernate:
        format_sql: true
```

### 2.2 Repositories

```java
// Interface de base avec méthodes CRUD
public interface UserRepository 
    extends JpaRepository<User, Long> {
    
    // Méthodes dérivées (Query Methods)
    List<User> findByNameContaining(String name);
    Optional<User> findByEmail(String email);
    boolean existsByEmail(String email);
    
    // Query personnalisée avec JPQL
    @Query("SELECT u FROM User u WHERE u.active = true")
    List<User> findActiveUsers();
    
    // Query native SQL
    @Query(
        value = "SELECT * FROM users WHERE created_at > ?1",
        nativeQuery = true
    )
    List<User> findRecentUsers(LocalDateTime date);
    
    // Modification avec @Modifying
    @Modifying
    @Transactional
    @Query("UPDATE User u SET u.active = false WHERE u.lastLogin < ?1")
    int deactivateInactiveUsers(LocalDateTime date);
}
```

### 2.3 Services avec Spring Data JPA

```java
@Service
@Transactional
public class UserService {
    private final UserRepository userRepository;
    
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }
    
    public User createUser(User user) {
        if (userRepository.existsByEmail(user.getEmail())) {
            throw new DuplicateEmailException();
        }
        return userRepository.save(user);
    }
    
    public Page<User> findUsers(Pageable pageable) {
        return userRepository.findAll(pageable);
    }
    
    public List<User> searchUsers(String name) {
        return userRepository.findByNameContaining(name);
    }
}
```

### 2.4 Pagination et Tri

```java
// Dans le contrôleur
@GetMapping("/users")
public Page<User> getUsers(
    @RequestParam(defaultValue = "0") int page,
    @RequestParam(defaultValue = "10") int size,
    @RequestParam(defaultValue = "name") String sort
) {
    return userService.findUsers(
        PageRequest.of(page, size, Sort.by(sort))
    );
}

// Utilisation de Specifications
public interface UserRepository extends 
    JpaRepository<User, Long>,
    JpaSpecificationExecutor<User> {
}

// Création de spécifications
public class UserSpecs {
    public static Specification<User> hasName(String name) {
        return (root, query, cb) -> 
            cb.like(root.get("name"), "%" + name + "%");
    }
    
    public static Specification<User> isActive() {
        return (root, query, cb) -> 
            cb.equal(root.get("active"), true);
    }
}
```

## Points à retenir

1. **JPA**
   - Annotations de mapping (@Entity, @Id, etc.)
   - Relations entre entités (OneToMany, ManyToMany)
   - Gestion des transactions
   - JPQL vs SQL natif

2. **Spring Data JPA**
   - Repositories préconfigurés
   - Query Methods
   - @Query pour requêtes personnalisées
   - Pagination et tri

3. **Bonnes Pratiques**
   - Utiliser les transactions appropriées
   - Gérer les relations avec précaution
   - Optimiser les requêtes N+1
   - Utiliser le cache quand approprié
   - Valider les données avant persistance

4. **Points de vigilance**
   - Performance des requêtes
   - Gestion de la mémoire
   - Chargement lazy vs eager
   - Transactions imbriquées
