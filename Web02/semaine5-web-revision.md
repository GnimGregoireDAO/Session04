# Fiche de Révision - Semaine 5 Web

## 1. Collaboration et Architecture MVC Model 2

### 1.1 Architecture MVC Model 2

- **Définition** : Evolution du MVC classique adapté au web
- **Composants** :

  ```plaintext
  [Navigateur] <---> [Contrôleur (Servlet)] <---> [Modèle (JavaBeans)]
                              ↓
                        [Vue (JSP)]
  ```

### 1.2 Flux de données

```java
// Contrôleur central (FrontController)
public class FrontController extends HttpServlet {
    private Map<String, Command> commands = new HashMap<>();
    
    @Override
    public void init() {
        commands.put("users", new UserCommand());
        commands.put("products", new ProductCommand());
    }
    
    protected void doGet(HttpServletRequest request, 
                        HttpServletResponse response) {
        String path = request.getPathInfo();
        Command command = commands.get(path);
        
        String view = command.execute(request, response);
        request.getRequestDispatcher(view).forward(request, response);
    }
}
```

## 2. Injection de Dépendances

### 2.1 Principe

- **Définition** : Pattern permettant de découpler les composants
- **Types d'injection** :
  - Par constructeur
  - Par setter
  - Par champ (annotation)

### 2.2 Implémentation

```java
// Sans injection (couplage fort)
public class UserService {
    private UserDao userDao = new UserDaoImpl(); // 👎
}

// Avec injection par constructeur (couplage faible)
public class UserService {
    private final UserDao userDao;
    
    public UserService(UserDao userDao) { // 👍
        this.userDao = userDao;
    }
}

// Avec injection par annotation
@Injectable
public class UserService {
    @Autowired
    private UserDao userDao;
}
```

### 2.3 Configuration

```java
// Configuration de l'injection
public class DependencyInjector {
    private static Map<Class<?>, Object> container = new HashMap<>();
    
    static {
        container.put(UserDao.class, new UserDaoImpl());
        container.put(UserService.class, 
            new UserService(container.get(UserDao.class)));
    }
    
    public static <T> T get(Class<T> type) {
        return type.cast(container.get(type));
    }
}
```

## 3. Contenu Statique

### 3.1 Configuration (web.xml)

```xml
<servlet-mapping>
    <servlet-name>default</servlet-name>
    <url-pattern>/static/*</url-pattern>
</servlet-mapping>

<resource-ref>
    <res-ref-name>images</res-ref-name>
    <res-type>java.net.URL</res-type>
    <res-auth>Container</res-auth>
</resource-ref>
```

### 3.2 Organisation

```plaintext
webapp/
├── static/
│   ├── css/
│   ├── js/
│   └── images/
├── WEB-INF/
│   └── ...
```

### 3.3 Utilisation

```jsp
<!-- Dans les JSP -->
<link href="${pageContext.request.contextPath}/static/css/style.css" 
      rel="stylesheet">
<img src="${pageContext.request.contextPath}/static/images/logo.png" 
     alt="Logo">
```

## 4. Couche Métier

### 4.1 Services

```java
public interface BusinessService<T> {
    T create(T entity);
    T update(T entity);
    void delete(Long id);
    T findById(Long id);
    List<T> findAll();
}

public class UserBusinessService implements BusinessService<User> {
    private final UserDao userDao;
    private final ValidationService validationService;
    
    public UserBusinessService(UserDao userDao, 
                             ValidationService validationService) {
        this.userDao = userDao;
        this.validationService = validationService;
    }
    
    @Override
    public User create(User user) {
        // Validation
        validationService.validateUser(user);
        
        // Logique métier
        if (userDao.findByEmail(user.getEmail()) != null) {
            throw new BusinessException("Email already exists");
        }
        
        // Persistance
        return userDao.save(user);
    }
}
```

### 4.2 Validation

```java
public class ValidationService {
    public void validateUser(User user) {
        List<String> errors = new ArrayList<>();
        
        if (user.getName() == null || user.getName().trim().isEmpty()) {
            errors.add("Name is required");
        }
        
        if (!isValidEmail(user.getEmail())) {
            errors.add("Invalid email format");
        }
        
        if (!errors.isEmpty()) {
            throw new ValidationException(errors);
        }
    }
}
```

## Points à retenir

1. **Architecture MVC Model 2**
   - Contrôleur central (Front Controller)
   - Séparation claire des responsabilités
   - Configuration dans web.xml
   - Routing flexible

2. **Injection de Dépendances**
   - Réduction du couplage
   - Facilite les tests
   - Configuration centralisée
   - Différents types d'injection

3. **Contenu Statique**
   - Organisation claire des ressources
   - Configuration appropriée
   - Sécurité des ressources
   - Performance (cache, compression)

4. **Couche Métier**
   - Validation des données
   - Règles métier centralisées
   - Gestion des transactions
   - Séparation des préoccupations

5. **Bonnes Pratiques**
   - Logger les opérations importantes
   - Gérer les exceptions de manière appropriée
   - Documentation du code
   - Tests unitaires
