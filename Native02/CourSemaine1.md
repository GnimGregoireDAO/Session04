# Fiche de Révision : Les Bases de Kotlin Simplifiées

## 1. Introduction à Kotlin

- Langage moderne et simple à apprendre
- Compatible avec Java
- Sécurisé contre les erreurs de null
- Utilisé principalement pour le développement Android

## 2. Les Variables

### Types de Variables

```kotlin
// Variable qu'on peut modifier
var age = 25
age = 26 // OK

// Variable qu'on ne peut pas modifier
val nom = "Pierre"
// nom = "Paul" // Erreur!

// Variables avec type explicite
var compteur: Int = 0
var message: String = "Bonjour"
var actif: Boolean = true
var prix: Double = 19.99
```

### Null Safety

```kotlin
// Variable qui peut être null
var texte: String? = "Hello"
texte = null // OK

// Variable qui ne peut pas être null
var nom: String = "Pierre"
// nom = null // Erreur!
```

## 3. Structures de Base

### Les Conditions

```kotlin
// If simple
var age = 18
if (age >= 18) {
    println("Majeur")
} else {
    println("Mineur")
}

// When (remplace switch)
var note = 15
when (note) {
    20 -> println("Parfait!")
    in 16..19 -> println("Très bien!")
    in 10..15 -> println("Passable")
    else -> println("À améliorer")
}
```

### Les Boucles

```kotlin

for (i in 1..5) {
    println(i)  // Affiche 1, 2, 3, 4, 5
}

// Boucle while
var compteur = 0
while (compteur < 3) {
    println("Tour $compteur")
    compteur++
}
```

## 4. Les Fonctions

### Fonctions

```kotlin
// Fonction basique
fun direBonjour() {
    println("Bonjour!")
}

// Fonction avec paramètres
fun saluer(nom: String) {
    println("Bonjour $nom!")
}

// Fonction qui retourne une valeur
fun additionner(a: Int, b: Int): Int {
    return a + b
}

// Fonction en une ligne
fun multiplier(x: Int, y: Int) = x * y
```

## 5. Les Collections

### Listes

```kotlin
// Liste non modifiable
val fruits = listOf("pomme", "banane", "orange")
println(fruits[0]) // pomme

// Liste modifiable
val nombres = mutableListOf(1, 2, 3)
nombres.add(4)
nombres.remove(1)
```

### Tableaux

```kotlin
// Tableau simple
val notes = arrayOf(15, 17, 12, 19)
for (note in notes) {
    println(note)
}
```

## 6. Les Classes

### Classe Simple

```kotlin
// Définition d'une classe
class Personne(val nom: String, var age: Int) {
    fun sePresenter() {
        println("Je m'appelle $nom et j'ai $age ans")
    }
}

// Utilisation de la classe
val pierre = Personne("Pierre", 25)
pierre.sePresenter()
pierre.age = 26 // On peut modifier l'âge
```

## 7. Les String Templates

### Utilisation Simple

```kotlin
val prenom = "Marie"
val age = 30

// Template simple
println("Je m'appelle $prenom")

// Template avec expression
println("L'année prochaine, j'aurai ${age + 1} ans")
```

## 8. Manipulation des Chaînes

```kotlin
val texte = "Kotlin"

// Opérations de base
println(texte.length) // 6
println(texte.uppercase()) // KOTLIN
println(texte.lowercase()) // kotlin

// Concatenation
val nom = "Pierre"
val message = "Bonjour " + nom
val messageTemplate = "Bonjour $nom"
```

## 9. Exercices Pratiques

```kotlin
// Exercice 1: Calculer la moyenne
fun calculerMoyenne(notes: List<Int>): Double {
    return notes.sum().toDouble() / notes.size
}

// Exercice 2: Vérifier si un nombre est pair
fun estPair(nombre: Int): Boolean {
    return nombre % 2 == 0
}

// Utilisation
val notes = listOf(15, 12, 18, 10)
println("Moyenne: ${calculerMoyenne(notes)}")
println("Est pair: ${estPair(4)}")
```
