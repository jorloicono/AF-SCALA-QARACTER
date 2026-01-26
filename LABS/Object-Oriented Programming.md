## 🏛️ Classes: Modeling Data and Behavior

A **Class** is a blueprint. In Scala, class parameters (like `name`) automatically become fields. If you use `var`, they are mutable; if you use `val` (or no prefix), they are immutable by default.

```scala
// Define a class with mutable fields
class Person(var name: String, var vocation: String)

val p = Person("Robert Allen Zimmerman", "Harmonica Player")

// Accessing and modifying attributes
p.name = "Bob Dylan"
p.vocation = "Musician"

```

### Class Logic and Constructors

The entire body of a class in Scala is part of its **primary constructor**. Any code not inside a method runs during initialization.

```scala
class Person2(var firstName: String, var lastName: String):
  println("initialization begins")
  val fullName = firstName + " " + lastName

  def printFullName: Unit = println(fullName)

  printFullName // Called during instantiation
  println("initialization ends")

val john = Person2("John", "Doe")

```

### Default Parameters

Just like methods, constructors can have default values, making object creation very flexible.

```scala
class Socket(val timeout: Int = 5_000, val linger: Int = 5_000):
  override def toString = s"timeout: $timeout, linger: $linger"

val s1 = Socket()                   // timeout: 5000, linger: 5000
val s2 = Socket(linger = 10_000)    // Named parameter usage

```

---

## 📦 Objects: Singletons and Companions

An **Object** is a singleton—a class that has exactly one instance. They are often used for utility methods or constants.

```scala
object StringUtils:
  def truncate(s: String, length: Int): String = s.take(length)
  def isNullOrEmpty(s: String): Boolean = s == null || s.trim.isEmpty

// Usage
StringUtils.truncate("Chuck Bartowski", 5) // "Chuck"

// Storing values/constants
object MathConstants:
  val PI = 3.14159

```

### Companion Objects

When a `class` and an `object` share the same name in the same file, the object is a **Companion Object**. They can access each other's private members.

```scala
class Circle(val radius: Double):
  def area: Double = Circle.calculateArea(radius)

object Circle:
  private def calculateArea(radius: Double): Double = math.Pi * math.pow(radius, 2.0)

```

---

## 🧬 Traits: Interfaces on Steroids

**Traits** are like Java interfaces but more powerful; they can contain both abstract and concrete (implemented) methods. Classes can inherit from multiple traits.

```scala
trait HasLegs:
  def numLegs: Int
  def walk(): Unit
  def stop() = println("Stopped walking") // Concrete method

trait HasTail:
  def tailColor: String
  def wagTail() = println("Tail is wagging")

class IrishSetter(name: String) extends HasLegs, HasTail:
  val numLegs = 4
  val tailColor = "Red"
  def walk() = println("I’m walking")

```

---

## 🔢 Enums: Enumerated Types

**Enums** define a type with a finite set of values. In Scala 3, enums are very powerful and can even take parameters.

```scala
enum Color:
  case Red, Green, Blue

val red = Color.Red
println(red.ordinal) // 0

// Enums with parameters (Planets example)
enum Planet(mass: Double, radius: Double):
  private final val G = 6.67300E-11
  def surfaceGravity = G * mass / (radius * radius)
  
  case Earth extends Planet(5.976e+24, 6.37814e6)
  case Mars  extends Planet(6.421e+23, 3.3972e6)

val earthGravity = Planet.Earth.surfaceGravity

```

---

## 💎 Case Classes: Immutable Data Carriers

**Case Classes** are ideal for modeling immutable data. They automatically provide `equals`, `hashCode`, and `toString` methods.

```scala
case class Person(name: String, relation: String)

val christina = Person("Christina", "niece")

// christina.name = "Fred" // Error: reassignment to val (Case classes are immutable)

```

---

## 🚀 Final Practice Exercise

**Challenge:** Create a mini-ecosystem.

1. Create a `trait Flyable` with a method `fly()` that prints "I am flying!".
2. Create a `case class Bird(name: String, species: String)` that extends `Flyable`.
3. Create a `companion object Bird` with a method `createParrot(name: String)` that returns a `Bird` with the species "Parrot".

**Test it:** Create a parrot using the companion object and make it fly!

