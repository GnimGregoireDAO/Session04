# Programmation Orientée Objet en Kotlin

## 1. Concepts de base de la POO

- **Classes et Objets :**
  - Une **classe** est un modèle qui définit les propriétés et les comportements (méthodes) des objets.
  - Un **objet** est une instance d'une classe.

```kotlin
class Person(val name: String, var age: Int)

val person1 = Person("Alice", 25)
```

## 2. Héritage

Permet à une classe de dériver d'une autre classe.

La classe dérivée hérite des propriétés et méthodes de la classe de base.

```kotlin
open class Animal(val name: String) {
    fun eat() {
        println("$name is eating")
    }
}

class Dog(name: String) : Animal(name)

val dog = Dog("Buddy")
dog.eat() // Buddy is eating
```

## 3. Encapsulation

Restreindre l'accès aux composants internes d'un objet et ne permettre l'accès qu'à travers des méthodes spécifiées.

```kotlin
class BankAccount(private var balance: Double) {
    fun deposit(amount: Double) {
        if (amount > 0) balance += amount
    }

    fun getBalance(): Double = balance
}

val account = BankAccount(100.0)
account.deposit(50.0)
println(account.getBalance()) // 150.0
```

## 3. Polymorphisme

Permet d'utiliser une méthode ou une classe de plusieurs façons.

Méthodes surchargées : plusieurs méthodes avec le même nom mais des paramètres différents.

```kotlin
class MathOperations {
    fun add(a: Int, b: Int): Int = a + b
    fun add(a: Double, b: Double): Double = a + b
}

val math = MathOperations()
println(math.add(1, 2)) // 3
println(math.add(1.5, 2.5)) // 4.0
```

## 5. Abstraction

Masquer les détails complexes et ne montrer que l'essentiel.

Utilisation des classes abstraites et des interfaces.

```kotlin
abstract class Vehicle {
    abstract fun drive()
}

class Car : Vehicle() {
    override fun drive() {
        println("Driving a car")
    }
}

val car = Car()
car.drive() // Driving a car
```

## 6. Interfaces

Les interfaces peuvent contenir des déclarations de méthodes abstraites et concrètes.

Une classe peut implémenter plusieurs interfaces.

```kotlin
interface Drivable {
    fun drive()
}

class Bicycle : Drivable {
    override fun drive() {
        println("Riding a bicycle")
    }
}

val bike = Bicycle()
bike.drive() // Riding a bicycle
```

## 7. Propriétés et Méthodes

Propriétés : Variables définies dans une classe.

Méthodes : Fonctions définies dans une classe.

```kotlin
class Rectangle(val width: Int, val height: Int) {
    val area: Int
        get() = width * height

    fun perimeter(): Int = 2 * (width + height)
}

val rect = Rectangle(5, 10)
println("Area: ${rect.area}") // Area: 50
println("Perimeter: ${rect.perimeter()}") // Perimeter: 30
```

## 8. Visibilité

```html

public (par défaut) : accessible partout.

private : accessible uniquement dans la classe où elle est définie.

protected : accessible dans la classe et ses sous-classes.

internal : accessible dans le même module.
```

## 9. Singleton

Kotlin fournit un moyen simple de créer des singletons à l'aide du mot clé object.

```kotlin
object DatabaseConnection {
    fun connect() {
        println("Connected to database")
    }
}

DatabaseConnection.connect() // Connected to database
```
