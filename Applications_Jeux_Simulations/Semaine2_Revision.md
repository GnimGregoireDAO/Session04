# Fiche de Révision - Semaine 2

## 1. Level Design 2D

### 1.1 Principes fondamentaux
- **Flow** : Rythme et progression du niveau
- **Pacing** : Alternance entre action et repos
- **Difficulté progressive** : Courbe d'apprentissage
- **Points d'intérêt** : Éléments attirant l'attention du joueur

### 1.2 Éléments de level design 2D
- **Plateformes**
  - Types (mobiles, destructibles, rebondissantes)
  - Espacement et hauteur
  - Timing des sauts
  
- **Obstacles**
  - Pièges
  - Ennemis
  - Zones dangereuses

### 1.3 Patterns de conception
- **Tutoriel intégré**
- **Points de contrôle**
- **Chemins alternatifs**
- **Secrets et collectibles**

## 2. Système de Tuiles (Tilemap)

### 2.1 Concepts de base
- **Tile** : Unité de base du level design 2D
- **Tileset** : Collection de tuiles thématiques
- **Grid** : Système de coordonnées pour les tuiles
- **Layers** : Organisation en couches des tilemaps

### 2.2 Types de Tiles dans Unity
- **Normal tiles** : Tuiles standards
- **Animated tiles** : Tuiles animées
- **Rule tiles** : Tuiles avec règles d'auto-placement
- **Random tiles** : Tuiles à placement aléatoire

### 2.3 Organisation des Tilemaps
```csharp
// Structure recommandée
- Grid
  |- Background Layer
  |- Ground Layer
  |- Decoration Layer
  |- Collision Layer
```

## 3. Programmation des Contrôleurs

### 3.1 Input System
- **Input Manager (Legacy)**
  ```csharp
  float horizontal = Input.GetAxis("Horizontal");
  float vertical = Input.GetAxis("Vertical");
  bool isJumping = Input.GetButtonDown("Jump");
  ```

- **New Input System**
  ```csharp
  public class PlayerController : MonoBehaviour
  {
      private PlayerInput playerInput;
      private InputAction moveAction;
      
      void Awake()
      {
          playerInput = GetComponent<PlayerInput>();
          moveAction = playerInput.actions["Move"];
      }
  }
  ```

### 3.2 Mouvement 2D
```csharp
public class PlayerMovement : MonoBehaviour
{
    [SerializeField] private float speed = 5f;
    [SerializeField] private float jumpForce = 10f;
    private Rigidbody2D rb;
    
    void FixedUpdate()
    {
        float moveInput = Input.GetAxisRaw("Horizontal");
        rb.velocity = new Vector2(moveInput * speed, rb.velocity.y);
    }
}
```

### 3.3 États du personnage
- **Idle**
- **Running**
- **Jumping**
- **Falling**
- **Attacking**

## 4. Gestion de la Caméra

### 4.1 Types de caméras 2D
- **Fixed Camera** : Statique
- **Following Camera** : Suit le joueur
- **Platform Camera** : Défilement horizontal/vertical
- **Room-based Camera** : Changement par zone

### 4.2 Cinemachine dans Unity
```csharp
// Configuration de base Cinemachine
- Virtual Camera
  |- Body
     |- Damping
     |- Screen X/Y
  |- Lens
     |- Orthographic Size
     |- Near/Far Clip Plane
```

### 4.3 Suivi de cible
```csharp
public class CameraFollow : MonoBehaviour
{
    [SerializeField] private Transform target;
    [SerializeField] private float smoothSpeed = 0.125f;
    [SerializeField] private Vector3 offset;

    void LateUpdate()
    {
        Vector3 desiredPosition = target.position + offset;
        Vector3 smoothedPosition = Vector3.Lerp(
            transform.position, 
            desiredPosition, 
            smoothSpeed
        );
        transform.position = smoothedPosition;
    }
}
```

### 4.4 Zones de contraintes
- **Confiner Camera** : Limites de la zone de jeu
- **Dead Zone** : Zone sans mouvement de caméra
- **Soft Zone** : Zone de transition douce

## Points clés à retenir
1. Un bon level design guide naturellement le joueur
2. Les tilemaps permettent une création rapide de niveaux
3. Les contrôles doivent être réactifs et prévisibles
4. La caméra doit servir le gameplay

## Exercices pratiques suggérés
1. Créer un niveau simple avec tilemap
2. Implémenter un contrôleur de personnage basique
3. Configurer une caméra qui suit le joueur
4. Ajouter des animations de base au personnage
5. Créer des zones de déclenchement pour la caméra

## Ressources complémentaires
- Documentation Unity sur les Tilemaps
- Guide Cinemachine
- Tutoriels sur le New Input System
- Exemples de patterns de level design 2D
