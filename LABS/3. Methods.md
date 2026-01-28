## 🛠️ Defining and Using Methods

In Scala, you define a method using the `def` keyword. Scala is expression-based, meaning the last line of a method is automatically the return value—the `return` keyword is rarely used.

```scala
// Define a simple method
def add(a: Int, b: Int): Int = a + b

val x = add(1, 2) // 3

// Methods can span multiple lines
def addThenDouble(a: Int, b: Int): Int =
  val sum = a + b
  sum * 2 // The result of this expression is returned

addThenDouble(1, 1) // 4

```

---

## ⚙️ Default Parameters & Logic

You can make your methods more flexible by providing default values for parameters and using control structures like `if` directly in the method body.

```scala
// Methods with default parameters
def makeConnection(timeout: Int = 5_000, protocol: String = "http") =
  println(f"timeout = ${timeout}%d, protocol = ${protocol}%s")

makeConnection()                // Uses both defaults
makeConnection(2_000)           // Overrides timeout
makeConnection(3_000, "https")  // Overrides both

// Using 'if' as an expression inside a method
def isTruthy(a: Any): Boolean =
  if a == 0 || a == "" || a == false then
    false
  else
    true

```

---

## 🔒 Method Visibility & Scope

Scala provides three main levels of access control to manage how methods are shared between classes and subclasses.

| Modifier | Description |
| --- | --- |
| **Public** | The default state. Methods are accessible from anywhere. |
| **Private** | Accessible only within the current class. Hidden from subclasses. |
| **Protected** | Accessible within the current class and by any subclasses. |

### Practical Example:

```scala
class Animal:
  private def breathe() = println("I’m breathing") // Only for Animal
  
  def walk() =
    breathe() // Internal call is okay
    println("I’m walking")
    
  protected def speak() = println("Hello?") // Subclasses can use this

class Cat extends Animal:
  override def speak() = println("Meow") // Overriding protected method
  // override def breathe() // Error: breathe is private to Animal

```

---

## 🧬 Extension Methods

One of Scala 3's most powerful features is the ability to add new methods to existing classes (even those you didn't write, like `String` or `Int`) without using inheritance.

```scala
case class Circle(x: Double, y: Double, radius: Double)

// Adding functionality to Circle "from the outside"
extension (c: Circle)
  def circumference: Double = c.radius * math.Pi * 2
  def diameter: Double = c.radius * 2
  def area: Double = math.Pi * c.radius * c.radius

val aCircle = Circle(0, 0, 10)
println(aCircle.area) // Now Circle acts as if it always had an .area method!

```

---

## 🚀 Final Practice Exercise

**Scenario:** You are building a simple banking system.

1. Create a `case class Account(id: String, balance: Double)`.
2. Use an **extension** to add a method `withdraw(amount: Double)` that returns a new `Account` with the reduced balance.
3. Add a **protected** method in a base class `BankEmployee` called `audit` that simply prints "Auditing account...".
4. Create a subclass `Manager` that overrides `audit` to print "Manager is auditing carefully".

**Your Task:** Write the code to create a Manager, create an Account, and use the extension method to withdraw money.
