# Fiche de Révision - Semaine 8 Web

## 1. Contrôleur Spring MVC

### 1.1 Configuration de base

```java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {
    @Override
    public void addViewControllers(ViewControllerRegistry registry) {
        registry.addViewController("/").setViewName("home");
    }
    
    @Bean
    public ViewResolver viewResolver() {
        ThymeleafViewResolver resolver = new ThymeleafViewResolver();
        resolver.setTemplateEngine(templateEngine());
        resolver.setCharacterEncoding("UTF-8");
        return resolver;
    }
}
```

### 1.2 Structure du Contrôleur

```java
@Controller
@RequestMapping("/users")
public class UserController {
    private final UserService userService;
    
    @Autowired
    public UserController(UserService userService) {
        this.userService = userService;
    }
    
    // Afficher la liste des utilisateurs
    @GetMapping
    public String listUsers(Model model) {
        model.addAttribute("users", userService.findAll());
        return "users/list";
    }
    
    // Afficher le formulaire de création
    @GetMapping("/create")
    public String showCreateForm(Model model) {
        model.addAttribute("user", new User());
        return "users/form";
    }
    
    // Traiter la soumission du formulaire
    @PostMapping
    public String createUser(@Valid @ModelAttribute User user, 
                           BindingResult result) {
        if (result.hasErrors()) {
            return "users/form";
        }
        userService.save(user);
        return "redirect:/users";
    }
    
    // Gestionnaire d'exceptions
    @ExceptionHandler(UserNotFoundException.class)
    public String handleUserNotFound(Model model) {
        model.addAttribute("error", "Utilisateur non trouvé");
        return "error";
    }
}
```

## 2. Thymeleaf - Configuration et Utilisation

### 2.1 Configuration Thymeleaf

```java
@Configuration
public class ThymeleafConfig {
    @Bean
    public SpringTemplateEngine templateEngine() {
        SpringTemplateEngine engine = new SpringTemplateEngine();
        engine.setEnableSpringELCompiler(true);
        engine.setTemplateResolver(templateResolver());
        return engine;
    }
    
    @Bean
    public SpringResourceTemplateResolver templateResolver() {
        SpringResourceTemplateResolver resolver = 
            new SpringResourceTemplateResolver();
        resolver.setPrefix("classpath:/templates/");
        resolver.setSuffix(".html");
        resolver.setTemplateMode(TemplateMode.HTML);
        resolver.setCharacterEncoding("UTF-8");
        resolver.setCacheable(false); // Pour le développement
        return resolver;
    }
}
```

## 3. Pages Thymeleaf

### 3.1 Structure de base

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Mon Application</title>
    <link rel="stylesheet" th:href="@{/css/style.css}">
</head>
<body>
    <header th:replace="fragments/header :: header"></header>
    <main th:fragment="content">
        <!-- Contenu principal -->
    </main>
    <footer th:replace="fragments/footer :: footer"></footer>
</body>
</html>
```

### 3.2 Expressions Thymeleaf

```html
<!-- Variables et expressions -->
<p th:text="${user.name}">Nom par défaut</p>
<p th:utext="${htmlContent}">Contenu HTML</p>

<!-- Conditions -->
<div th:if="${not #lists.isEmpty(users)}">
    Liste non vide
</div>
<p th:unless="${user.isAdmin()}">
    Accès restreint
</p>

<!-- Boucles -->
<tr th:each="user : ${users}">
    <td th:text="${user.name}">Nom</td>
    <td th:text="${user.email}">Email</td>
</tr>

<!-- Switch/Case -->
<div th:switch="${user.role}">
    <p th:case="'ADMIN'">Administrateur</p>
    <p th:case="'USER'">Utilisateur</p>
    <p th:case="*">Rôle inconnu</p>
</div>
```

### 3.3 Formulaires

```html
<form th:action="@{/users}" th:object="${user}" method="post">
    <!-- Affichage des erreurs globales -->
    <div th:if="${#fields.hasErrors('*')}">
        <ul>
            <li th:each="err : ${#fields.errors('*')}" 
                th:text="${err}">Erreur</li>
        </ul>
    </div>
    
    <!-- Champs du formulaire -->
    <div>
        <label>Nom:</label>
        <input type="text" th:field="*{name}"/>
        <span th:if="${#fields.hasErrors('name')}" 
              th:errors="*{name}">Erreur nom</span>
    </div>
    
    <div>
        <label>Email:</label>
        <input type="email" th:field="*{email}"/>
        <span th:if="${#fields.hasErrors('email')}" 
              th:errors="*{email}">Erreur email</span>
    </div>
    
    <!-- Select -->
    <select th:field="*{role}">
        <option th:each="role : ${roles}"
                th:value="${role}"
                th:text="${role.label}">Rôle</option>
    </select>
    
    <button type="submit">Envoyer</button>
</form>
```

### 3.4 Fragments et Layout

```html
<!-- fragments/header.html -->
<header th:fragment="header">
    <nav>
        <a th:href="@{/}">Accueil</a>
        <a th:href="@{/users}">Utilisateurs</a>
    </nav>
</header>

<!-- Utilisation des fragments -->
<div th:replace="fragments/header :: header">
    <!-- Sera remplacé par le contenu du fragment -->
</div>

<!-- Passage de paramètres aux fragments -->
<div th:replace="fragments/alert :: alert(${message}, 'success')">
</div>
```

## Points à retenir

1. **Spring MVC**
   - Structure MVC claire
   - Gestion des routes avec @RequestMapping
   - Injection de dépendances
   - Validation des formulaires
   - Gestion des erreurs

2. **Thymeleaf Configuration**
   - Configuration du moteur de template
   - Résolution des vues
   - Gestion du cache
   - Encodage des caractères

3. **Thymeleaf Syntaxe**
   - Expression de variables ${...}
   - Expression d'URLs @{...}
   - Expression de sélection *{...}
   - Expression de messages #{...}
   - Fragments et layouts

4. **Bonnes Pratiques**
   - Séparation des préoccupations
   - Réutilisation des fragments
   - Validation côté client et serveur
   - Messages d'erreur clairs
   - Organisation des templates
