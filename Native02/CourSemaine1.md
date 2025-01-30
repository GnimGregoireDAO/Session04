
# Fiche de Révision : Les Bases de Kotlin

## 1. Introduction à Kotlin
- **Kotlin** est un langage de programmation statiquement typé qui fonctionne sur la JVM (Java Virtual Machine).
- Il est conçu pour être entièrement interopérable avec Java.

## 2. Syntaxe de base
### Déclaration de variables
```kotlin
// Variable mutable
var mutVariable: String = "modifiable"

// Variable immuable
val immutVariable: String = "non modifiable"
```

### Types de base
- **Numbers** : `Int`, `Long`, `Float`, `Double`
- **Boolean** : `true` ou `false`
- **Characters** : `Char`
- **Strings** : `String`

### Boucles et conditions
```kotlin
// Condition
if (condition) {
    // code
} else {
    // code
}

// When (équivalent de switch)
when (variable) {
    1 -> print("Un")
    2 -> print("Deux")
    else -> print("Autre")
}

// Boucle for
for (i in 1..5) {
    println(i)
}

// Boucle while
var i = 1
while (i <= 5) {
    println(i)
    i++
}
```

## 3. Fonctions
### Définir une fonction
```kotlin
fun addition(a: Int, b: Int): Int {
    return a + b
}

// Fonction à expression unique
fun soustraction(a: Int, b: Int) = a - b
```

### Fonctions avec paramètres par défaut
```kotlin
fun saluer(nom: String = "Utilisateur") {
    println("Bonjour, $nom!")
}
```

## 4. Classes et Objets
### Déclaration d'une classe
```kotlin
class Personne(val nom: String, var age: Int) {
    fun afficherInfo() {
        println("Nom: $nom, Age: $age")
    }
}

// Instanciation d'un objet
val personne = Personne("Alice", 30)
personne.afficherInfo()
```

## 5. Collections
### Listes
```kotlin
val nombres = listOf(1, 2, 3, 4)
val nombresMutable = mutableListOf(1, 2, 3, 4)
```

### Maps
```kotlin
val map = mapOf("clé1" to "valeur1", "clé2" to "valeur2")
val mapMutable = mutableMapOf("clé1" to "valeur1", "clé2" to "valeur2")
```

### Boucles sur Collections
```kotlin
for (num in nombres) {
    println(num)
}

for ((clé, valeur) in map) {
    println("$clé -> $valeur")
}
```

## 6. Null Safety
### Gestion des valeurs nulles
```kotlin
var nom: String? = "Kotlin"
nom = null // Ceci est permis car nom est nullable

// Utilisation de l'opérateur safe call
val longueur = nom?.length

// Utilisation de l'opérateur Elvis
val longueur2 = nom?.length ?: 0
```

## 7. Extensions
### Fonctions d'extension
```kotlin
fun String.espacer(): String {
    return this.replace("", " ").trim()
}

val texte = "Kotlin"
println(texte.espacer()) // K o t l i n
``