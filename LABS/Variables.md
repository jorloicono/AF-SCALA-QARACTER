In Scala, variables are categorized by their mutability. Understanding the difference between `val` and `var` is the first step toward writing clean, idiomatic code.

---

## 1. Mutability: `val` vs `var`

The rule of thumb in Scala is: **Always use `val` unless you have a specific reason to use `var`.**

### Immutable (`val`)

Once a `val` is assigned, it can **never** be changed. It is a constant.

```scala
val a = 0
val msg = "Hello, world"

// msg = "Aloha"  // ERROR: reassignment to val. This won't compile!

```

### Mutable (`var`)

A `var` can be reassigned to a new value throughout its lifecycle.

```scala
var b = 1
var msg2 = "Hello, world"

msg2 = "Aloha"   // This works perfectly

```

---

## 2. User Input

To interact with the user via the console, use `readLine` from the `scala.io.StdIn` package.

```scala
import scala.io.StdIn.readLine

println("Please enter your name:")
val name = readLine()

println("Hello, " + name + "!")

```

---

## 3. String Interpolation

Instead of messy string concatenation (using `+`), Scala uses **String Interpolators**. The most common is the `s` interpolator, which allows you to embed variables directly using the `$` symbol.

```scala
val firstName = "John"
val mi = 'C'
val lastName = "Doe"

// Using the 's' prefix before the quotes
println(s"Name: $firstName $mi $lastName") // Output: "Name: John C Doe"

// You can also evaluate expressions using curly braces
println(s"2 + 2 = ${2 + 2}")               // Output: "2 + 2 = 4"

```

---

## 🧠 Quick Knowledge Check

1. **Which keyword** should you use for a variable that will store a user's ID that never changes?
2. If you try to run `val x = 10; x = 11`, **what happens?**
3. How do you print a variable named `age` inside a string using **interpolation**?

---

## 🛠 Practical Exercise

**Task: The Profile Generator**

1. Ask the user for their **favorite city** using `readLine`.
2. Store the current **temperature** (as a number) in a `var`.
3. Use string interpolation to print: `"It is currently [temp] degrees in [city]."`
4. Update the temperature variable to a new number.
5. Print the updated status.

