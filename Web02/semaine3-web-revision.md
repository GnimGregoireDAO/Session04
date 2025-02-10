# Fiche de Révision - Semaine 3 Web

## 1. Gestion des Sessions

### 1.1 Concept de Session

- **Définition** : Mécanisme permettant de maintenir l'état entre plusieurs requêtes HTTP
- **Fonctionnement** :
  - Création d'un identifiant unique (JSESSIONID)
  - Stockage côté serveur
  - Transmission via cookie ou URL rewriting

### 1.2 Utilisation dans Java EE

```java
// Récupération ou création de session
HttpSession session = request.getSession();
HttpSession session = request.getSession(true); // Force création

// Stockage de données
session.setAttribute("user", userObject);
session.setAttribute("panier", basketItems);

// Récupération de données
User user = (User) session.getAttribute("user");

// Gestion du timeout
session.setMaxInactiveInterval(1800); // 30 minutes

// Suppression de données
session.removeAttribute("user");
session.invalidate(); // Détruit la session
```

### 1.3 Bonnes Pratiques

- Limiter la taille des données en session
- Gérer la synchronisation (sessions concurrentes)
- Nettoyer les sessions obsolètes
- Sécuriser les données sensibles

## 2. Gestion des Cookies

### 2.1 Concept de Cookie

- **Définition** : Petit fichier texte stocké côté client
- **Types** :
  - Cookies de session
  - Cookies persistants
  - Cookies sécurisés

### 2.2 Manipulation en Java

```java
// Création d'un cookie
Cookie cookie = new Cookie("nom", "valeur");
cookie.setMaxAge(24 * 60 * 60); // 1 jour
cookie.setPath("/");
cookie.setSecure(true); // HTTPS uniquement
response.addCookie(cookie);

// Lecture des cookies
Cookie[] cookies = request.getCookies();
for (Cookie cookie : cookies) {
    if (cookie.getName().equals("nom")) {
        String value = cookie.getValue();
    }
}

// Suppression d'un cookie
Cookie cookie = new Cookie("nom", "");
cookie.setMaxAge(0);
response.addCookie(cookie);
```

## 3. Actions et JavaBeans

### 3.1 JavaBeans

```java
public class UserBean implements Serializable {
    private String name;
    private String email;
    
    // Constructeur sans argument obligatoire
    public UserBean() {}
    
    // Getters et Setters
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    public String getEmail() { return email; }
    public void setEmail(String email) { this.email = email; }
}
```

### 3.2 Actions JSP

```jsp
<!-- Utilisation de JavaBean -->
<jsp:useBean id="user" class="com.example.UserBean" scope="session" />
<jsp:setProperty name="user" property="name" value="John" />
<jsp:getProperty name="user" property="name" />

<!-- Forward -->
<jsp:forward page="destination.jsp" />

<!-- Include -->
<jsp:include page="header.jsp" />
```

## 4. EL (Expression Language) et JSTL

### 4.1 Expression Language

```jsp
<!-- Accès aux objets -->
${pageScope.variable}
${requestScope.message}
${sessionScope.user.name}
${applicationScope.config}

<!-- Opérateurs -->
${empty list}
${user.age > 18}
${param.id + 1}
${header["user-agent"]}

<!-- Collections -->
${myList[0]}
${myMap.key}
${myArray[1]}
```

### 4.2 JSTL (JSP Standard Tag Library)

#### Core Tags

```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>

<!-- Conditions -->
<c:if test="${user.age >= 18}">
    Majeur
</c:if>

<c:choose>
    <c:when test="${score >= 90}">A</c:when>
    <c:when test="${score >= 80}">B</c:when>
    <c:otherwise>C</c:otherwise>
</c:choose>

<!-- Boucles -->
<c:forEach items="${users}" var="user">
    ${user.name}
</c:forEach>

<c:forEach var="i" begin="1" end="5">
    Numéro ${i}
</c:forEach>

<!-- Variables -->
<c:set var="name" value="John" scope="session"/>
<c:remove var="name" scope="session"/>

<!-- URL -->
<c:url value="/user" var="userUrl">
    <c:param name="id" value="123"/>
</c:url>
```

#### Formatting Tags

```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt" %>

<!-- Dates -->
<fmt:formatDate value="${date}" pattern="dd/MM/yyyy"/>

<!-- Nombres -->
<fmt:formatNumber value="${price}" type="currency"/>
```

#### Functions

```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/functions" prefix="fn" %>

${fn:length(list)}
${fn:toUpperCase(text)}
${fn:contains(string, "search")}
```

## Points à retenir

1. **Sessions**
   - Gestion de l'état entre requêtes
   - Stockage côté serveur
   - Attention à la mémoire
   - Sécurité des données

2. **Cookies**
   - Stockage côté client
   - Limitations de taille
   - Considérations de sécurité
   - GDPR/Conformité

3. **JavaBeans**
   - Convention de nommage
   - Constructeur sans argument
   - Serializable
   - Encapsulation

4. **EL et JSTL**
   - Simplicité d'utilisation
   - Réduction du code Java dans JSP
   - Tags standardisés
   - Fonctions utilitaires

5. **Bonnes Pratiques**
   - Séparer la logique métier des vues
   - Utiliser JSTL plutôt que les scriptlets
   - Gérer correctement les sessions
   - Sécuriser les cookies
