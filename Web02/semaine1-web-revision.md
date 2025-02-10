# Fiche de Révision - Semaine 1 Web

## 1. Conception du Modèle des Données

- **Définition** : Organisation logique des données dans la base de données
- **Points clés** :
  - Identification des entités et leurs attributs
  - Définition des relations (1-1, 1-N, N-N)
  - Normalisation des tables (1NF, 2NF, 3NF)
  - Choix des types de données appropriés
  - Définition des clés primaires et étrangères
  - Contraintes d'intégrité

- **Bonnes pratiques** :
  - Éviter la redondance des données
  - Utiliser des noms de tables et colonnes significatifs
  - Définir les contraintes appropriées (NOT NULL, UNIQUE, etc.)
  - Documenter le schéma de la base de données

## 2. JDBC (Java Database Connectivity)

### 2.1 Présentation

- **Définition** : API Java permettant d'interagir avec des bases de données relationnelles
- **Composants principaux** :
  - DriverManager : Gestion des pilotes de base de données
  - Connection : Représente une connexion à la base
  - Statement/PreparedStatement : Exécution des requêtes
  - ResultSet : Stockage des résultats de requêtes

### 2.2 Étapes d'utilisation

```java
// 1. Chargement du driver
Class.forName("com.mysql.jdbc.Driver");

// 2. Établissement de la connexion
String url = "jdbc:mysql://localhost:3306/mabase";
Connection conn = DriverManager.getConnection(url, "user", "password");

// 3. Création et exécution des requêtes
// a. Requête simple
Statement stmt = conn.createStatement();
ResultSet rs = stmt.executeQuery("SELECT * FROM users");

// b. Requête préparée (recommandée)
PreparedStatement pstmt = conn.prepareStatement(
    "SELECT * FROM users WHERE age > ? AND city = ?"
);
pstmt.setInt(1, 18);
pstmt.setString(2, "Paris");
ResultSet rs = pstmt.executeQuery();

// 4. Traitement des résultats
while (rs.next()) {
    String nom = rs.getString("nom");
    int age = rs.getInt("age");
}

// 5. Gestion des ressources avec try-with-resources
try (Connection conn = DriverManager.getConnection(url, user, password);
     PreparedStatement pstmt = conn.prepareStatement(sql)) {
    // Code
}
```

### 2.3 Bonnes pratiques JDBC

- Utiliser des PreparedStatement pour prévenir les injections SQL
- Toujours fermer les ressources dans l'ordre inverse de leur création
- Gérer correctement les exceptions
- Utiliser le try-with-resources
- Externaliser les paramètres de connexion

## 3. Pattern DAO (Data Access Object)

### 3.1 Présentation

- **Définition** : Pattern de conception qui isole la logique d'accès aux données
- **Avantages** :
  - Séparation des préoccupations
  - Code plus maintenable
  - Facilite les tests
  - Permet de changer l'implémentation sans modifier le code client

### 3.2 Structure complète

```java
// Interface DAO
public interface UserDao {
    User findById(int id);
    List<User> findAll();
    void save(User user);
    void update(User user);
    void delete(int id);
    List<User> findByAge(int age);
}

// Implémentation
public class UserDaoImpl implements UserDao {
    private Connection getConnection() {
        return DatabaseConnection.getInstance().getConnection();
    }
    
    @Override
    public User findById(int id) {
        try (Connection conn = getConnection();
             PreparedStatement pstmt = conn.prepareStatement(
                 "SELECT * FROM users WHERE id = ?"
             )) {
            pstmt.setInt(1, id);
            try (ResultSet rs = pstmt.executeQuery()) {
                if (rs.next()) {
                    return new User(
                        rs.getInt("id"),
                        rs.getString("name"),
                        rs.getString("email")
                    );
                }
            }
        } catch (SQLException e) {
            throw new DaoException("Error finding user", e);
        }
        return null;
    }
    // Autres implémentations...
}
```

## 4. Pattern Singleton

### 4.1 Présentation

- **Définition** : Pattern garantissant une instance unique d'une classe
- **Cas d'utilisation** :
  - Connexions à la base de données
  - Configuration d'application
  - Caches

### 4.2 Implémentations

```java
// Version thread-safe avec double-checked locking
public class DatabaseConnection {
    private static volatile DatabaseConnection instance;
    private Connection connection;
    
    private DatabaseConnection() {
        // Configuration de la connexion
    }
    
    public static DatabaseConnection getInstance() {
        if (instance == null) {
            synchronized (DatabaseConnection.class) {
                if (instance == null) {
                    instance = new DatabaseConnection();
                }
            }
        }
        return instance;
    }
    
    public Connection getConnection() {
        if (connection == null) {
            // Initialiser la connexion
        }
        return connection;
    }
}

// Version avec initialization holder
public class DatabaseConnection {
    private DatabaseConnection() {}
    
    private static class SingletonHolder {
        private static final DatabaseConnection INSTANCE = 
            new DatabaseConnection();
    }
    
    public static DatabaseConnection getInstance() {
        return SingletonHolder.INSTANCE;
    }
}
```

## 5. Tests DAO

### 5.1 Types de tests

- **Tests unitaires** : Tester chaque méthode DAO isolément
- **Tests d'intégration** : Tester l'interaction avec la base de données
- **Tests de performance** : Vérifier les temps de réponse

### 5.2 Bonnes pratiques

- Utiliser une base de données de test dédiée
- Réinitialiser les données entre les tests
- Utiliser des transactions pour le rollback
- Mocker les connexions quand nécessaire

### 5.3 Exemples de tests

```java
@Test
public void testCRUDOperations() {
    // Arrange
    UserDao dao = new UserDaoImpl();
    User user = new User("test", "test@email.com");
    
    // Act & Assert - Create
    int id = dao.save(user);
    assertNotNull(id);
    
    // Act & Assert - Read
    User found = dao.findById(id);
    assertEquals(user.getName(), found.getName());
    
    // Act & Assert - Update
    user.setName("updated");
    dao.update(user);
    found = dao.findById(id);
    assertEquals("updated", found.getName());
    
    // Act & Assert - Delete
    dao.delete(id);
    assertNull(dao.findById(id));
}

@Test
public void testFindByAgeWithMock() {
    // Utilisation de Mockito
    Connection mockConn = mock(Connection.class);
    PreparedStatement mockPstmt = mock(PreparedStatement.class);
    ResultSet mockRs = mock(ResultSet.class);
    
    // Configuration des mocks
    when(mockConn.prepareStatement(anyString()))
        .thenReturn(mockPstmt);
    // ... autres configurations
}
```

## Points à retenir et bonnes pratiques

1. **Base de données**
   - Concevoir le modèle avant l'implémentation
   - Normaliser les tables
   - Documenter le schéma

2. **JDBC**
   - Toujours utiliser PreparedStatement
   - Gérer correctement les ressources
   - Utiliser try-with-resources
   - Centraliser la gestion des connexions

3. **DAO**
   - Une interface par entité
   - Exceptions spécifiques
   - Méthodes CRUD de base
   - Documentation claire

4. **Singleton**
   - Thread-safety si nécessaire
   - Initialisation paresseuse
   - Gestion des ressources

5. **Tests**
   - Couverture de code complète
   - Tests unitaires et d'intégration
   - Données de test isolées
   - Mock quand nécessaire
