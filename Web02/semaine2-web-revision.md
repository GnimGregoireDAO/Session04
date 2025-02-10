# Fiche de Révision - Semaine 2 Web

## 1. Applications Distribuées

### 1.1 Concepts Fondamentaux

- **Définition** : Application dont les composants s'exécutent sur différentes machines
- **Caractéristiques** :
  - Distribution des ressources
  - Scalabilité
  - Tolérance aux pannes
  - Communication réseau

### 1.2 Avantages et Inconvénients

- **Avantages** :
  - Meilleure utilisation des ressources
  - Haute disponibilité
  - Facilité de mise à l'échelle
  - Partage des charges

- **Inconvénients** :
  - Complexité accrue
  - Gestion de la sécurité
  - Dépendance au réseau
  - Maintenance plus complexe

## 2. Architecture Client-Serveur

### 2.1 Principes

- **Client** : Demandeur de services
  - Interface utilisateur
  - Validation locale
  - Gestion des requêtes

- **Serveur** : Fournisseur de services
  - Traitement des requêtes
  - Gestion des données
  - Logique métier

### 2.2 Types d'Architecture

```plaintext
1. Architecture 2-tiers
   [Client] <---> [Serveur]

2. Architecture 3-tiers
   [Client] <---> [Serveur d'application] <---> [Serveur de données]

3. Architecture n-tiers
   [Client] <---> [Présentation] <---> [Métier] <---> [Données] <---> [Services externes]
```

## 3. Java EE (Enterprise Edition)

### 3.1 Vue d'ensemble

- **Définition** : Platform pour applications d'entreprise en Java
- **Composants principaux** :
  - Servlets
  - JSP
  - EJB
  - JPA
  - WebServices

### 3.2 Conteneur Web

```plaintext
Conteneur Web (Tomcat, JBoss, etc.)
├── webapps/
│   ├── MonApplication/
│   │   ├── WEB-INF/
│   │   │   ├── web.xml
│   │   │   ├── classes/
│   │   │   └── lib/
│   │   ├── index.jsp
│   │   └── resources/
```

## 4. Servlets

### 4.1 Cycle de vie

```java
public class MonServlet extends HttpServlet {
    @Override
    public void init() throws ServletException {
        // Initialisation (une seule fois)
    }

    @Override
    protected void doGet(HttpServletRequest request, 
                        HttpServletResponse response) {
        // Traitement des requêtes GET
    }

    @Override
    protected void doPost(HttpServletRequest request, 
                         HttpServletResponse response) {
        // Traitement des requêtes POST
    }

    @Override
    public void destroy() {
        // Nettoyage final
    }
}
```

### 4.2 Configuration (web.xml)

```xml
<servlet>
    <servlet-name>MonServlet</servlet-name>
    <servlet-class>com.example.MonServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>MonServlet</servlet-name>
    <url-pattern>/maservlet</url-pattern>
</servlet-mapping>
```

### 4.3 Gestion des requêtes

- **HttpServletRequest** :

  ```java
  // Récupération des paramètres
  String param = request.getParameter("nom");
  
  // Gestion des sessions
  HttpSession session = request.getSession();
  session.setAttribute("user", userObject);
  
  // Attributs de requête
  request.setAttribute("message", "Hello");
  ```

- **HttpServletResponse** :

  ```java
  // Configuration de la réponse
  response.setContentType("text/html");
  response.setCharacterEncoding("UTF-8");
  
  // Écriture de la réponse
  PrintWriter out = response.getWriter();
  out.println("<html><body>Hello</body></html>");
  ```

## 5. Pages JSP (JavaServer Pages)

### 5.1 Syntaxe de base

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>

<!DOCTYPE html>
<html>
<head>
    <title>Ma Page JSP</title>
</head>
<body>
    <!-- Scriptlet -->
    <% String message = "Hello"; %>
    
    <!-- Expression -->
    <%= message %>
    
    <!-- Déclaration -->
    <%! int compteur = 0; %>
    
    <!-- JSTL -->
    <c:if test="${not empty user}">
        Bienvenue ${user.name}
    </c:if>
</body>
</html>
```

### 5.2 Objets implicites

- **request** : HttpServletRequest
- **response** : HttpServletResponse
- **session** : HttpSession
- **application** : ServletContext
- **out** : JspWriter

### 5.3 Expression Language (EL)

```jsp
<!-- Accès aux attributs -->
${requestScope.message}
${sessionScope.user.name}
${param.id}

<!-- Opérations -->
${1 + 2}
${empty list}
${user.age > 18 ? 'Majeur' : 'Mineur'}
```

## Points à retenir

1. **Architecture**
   - Comprendre les différentes couches
   - Séparation des responsabilités
   - Importance de la scalabilité

2. **Java EE**
   - Structure des applications
   - Rôle du conteneur web
   - Configuration (web.xml)

3. **Servlets**
   - Cycle de vie
   - Gestion des requêtes/réponses
   - Configuration et mapping

4. **JSP**
   - Séparation vue/logique
   - Syntaxe et balises
   - Objects implicites et EL

5. **Bonnes pratiques**
   - Ne pas mélanger logique et présentation
   - Gérer correctement les ressources
   - Utiliser les patterns MVC
   - Sécuriser les applications
