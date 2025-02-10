# Fiche de Révision - Semaine 4 Web

## 1. Architecture MVC (Modèle-Vue-Contrôleur)

### 1.1 Principes Fondamentaux

- **Modèle** : Données et logique métier
- **Vue** : Présentation des données
- **Contrôleur** : Gestion des requêtes et coordination

### 1.2 Implémentation en Java EE

```java
// Contrôleur (Servlet)
public class UserController extends HttpServlet {
    private UserService userService;
    
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) {
        String action = request.getParameter("action");
        
        switch(action) {
            case "list":
                List<User> users = userService.getAllUsers();
                request.setAttribute("users", users);
                request.getRequestDispatcher("/WEB-INF/views/users.jsp")
                       .forward(request, response);
                break;
            // Autres cas...
        }
    }
}

// Modèle (Service)
public class UserService {
    private UserDao userDao;
    
    public List<User> getAllUsers() {
        return userDao.findAll();
    }
}
```

### 1.3 Organisation des fichiers

```plaintext
webapp/
├── WEB-INF/
│   ├── views/           # JSP (Vues)
│   │   ├── users/
│   │   └── common/
│   ├── classes/         # Java (Contrôleurs, Modèles)
│   │   ├── controllers/
│   │   ├── models/
│   │   └── services/
│   └── web.xml
```

## 2. Gestion de la Persistance

### 2.1 Couche DAO avec Pattern Factory

```java
// Factory pour création des DAOs
public class DaoFactory {
    private static final DaoFactory instance = new DaoFactory();
    
    public static DaoFactory getInstance() {
        return instance;
    }
    
    public UserDao getUserDao() {
        return new UserDaoImpl(getConnection());
    }
    
    private Connection getConnection() {
        // Configuration et création de la connexion
    }
}

// Utilisation dans le service
public class UserService {
    private UserDao userDao;
    
    public UserService() {
        this.userDao = DaoFactory.getInstance().getUserDao();
    }
}
```

### 2.2 Transaction Management

```java
public class TransactionManager {
    public void executeInTransaction(Connection conn, 
                                   TransactionCode code) 
            throws SQLException {
        boolean autoCommit = conn.getAutoCommit();
        try {
            conn.setAutoCommit(false);
            code.execute(conn);
            conn.commit();
        } catch (SQLException e) {
            conn.rollback();
            throw e;
        } finally {
            conn.setAutoCommit(autoCommit);
        }
    }
}

// Usage
public void transferMoney(Account from, Account to, double amount) {
    TransactionManager.executeInTransaction(conn, (connection) -> {
        accountDao.withdraw(from, amount);
        accountDao.deposit(to, amount);
    });
}
```

## 3. Integration MVC-DAO

### 3.1 Structure Complète

```java
// Contrôleur
public class UserController extends HttpServlet {
    private UserService userService;
    
    @Override
    public void init() {
        userService = new UserService();
    }
    
    protected void doGet(HttpServletRequest request, 
                        HttpServletResponse response) {
        try {
            String action = request.getParameter("action");
            switch(action) {
                case "list":
                    listUsers(request, response);
                    break;
                case "edit":
                    editUser(request, response);
                    break;
            }
        } catch (Exception e) {
            request.setAttribute("error", e.getMessage());
            // Gestion d'erreur
        }
    }
    
    private void listUsers(HttpServletRequest request, 
                         HttpServletResponse response) 
            throws ServletException, IOException {
        List<User> users = userService.getAllUsers();
        request.setAttribute("users", users);
        request.getRequestDispatcher("/WEB-INF/views/users/list.jsp")
               .forward(request, response);
    }
}
```

### 3.2 Vue avec JSTL et EL

```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<html>
<body>
    <c:if test="${not empty error}">
        <div class="error">${error}</div>
    </c:if>
    
    <table>
        <c:forEach items="${users}" var="user">
            <tr>
                <td>${user.name}</td>
                <td>
                    <c:url value="/users" var="editUrl">
                        <c:param name="action" value="edit"/>
                        <c:param name="id" value="${user.id}"/>
                    </c:url>
                    <a href="${editUrl}">Éditer</a>
                </td>
            </tr>
        </c:forEach>
    </table>
</body>
</html>
```

## Points à retenir

1. **Architecture MVC**
   - Séparation claire des responsabilités
   - Facilite la maintenance et les tests
   - Réutilisation des composants
   - Organisation claire du code

2. **Persistance**
   - Pattern Factory pour création des DAOs
   - Gestion des transactions
   - Connection pooling
   - Gestion des erreurs

3. **Integration**
   - Communication entre couches
   - Gestion des exceptions
   - Validation des données
   - Sécurité des données

4. **Bonnes Pratiques**
   - Utiliser des interfaces pour les services et DAOs
   - Centraliser la gestion des erreurs
   - Logger les opérations importantes
   - Documenter l'architecture
   - Tests unitaires pour chaque couche
