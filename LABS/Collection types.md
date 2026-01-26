This guide covers the essential Scala collection types: **List**, **Vector**, **ArrayBuffer**, **Map**, **Set**, and **Range**.

---

## 1. List

A **linear, immutable sequence**. It is implemented as a linked-list. Because it is immutable, adding or removing elements creates a new list.

### Creation and Types

```scala
val ints = List(1, 2, 3)
val names = List("Joel", "Chris", "Ed")

// Using the cons (::) operator
val namesAgain = "Joel" :: "Chris" :: "Ed" :: Nil

// Explicit type declaration
val ints: List[Int] = List(1, 2, 3)
val names: List[String] = List("Joel", "Chris", "Ed")

// Mixed types using Union types or Any
val things: List[String | Int | Double] = List(1, "two", 3.0) 
val thingsAny: List[Any] = List(1, "two", 3.0)

```

### Adding Elements (Prepending/Appending)

```scala
val a = List(1, 2, 3)

val b = 0 :: a               // List(0, 1, 2, 3) (Prepend one)
val c = List(-1, 0) ::: a    // List(-1, 0, 1, 2, 3) (Prepend another list)

```

### Iteration

```scala
val names = List("Joel", "Chris", "Ed")

for (name <- names) println(name)
for name <- names do println(name)

```

---

## 2. Vector

An **indexed, immutable sequence**. It provides "effectively constant time" random access and updates. Use this over `List` when you need to access elements by index (e.g., `vec(500)`).

### Creation and Operations

```scala
val nums = Vector(1, 2, 3, 4, 5)
val strings = Vector("one", "two")

val a = Vector(1, 2, 3)
val b = a :+ 4                // Append: Vector(1, 2, 3, 4)
val c = a ++ Vector(4, 5)     // Concatenate: Vector(1, 2, 3, 4, 5)

```

---

## 3. ArrayBuffer

The general-purpose **mutable indexed sequence**. Use this when you need to modify, resize, or update elements in place.

### Creation

```scala
import scala.collection.mutable.ArrayBuffer

var strings = ArrayBuffer[String]()
var ints = ArrayBuffer[Int]()

// Creating with initial capacity
val buf = new ArrayBuffer[Int](100_000)

// Creating with elements
val nums = ArrayBuffer(1, 2, 3)

```

### Modification (Add, Remove, Update)

```scala
val nums = ArrayBuffer(1, 2, 3)
nums += 4                          // Append 4
nums ++= List(5, 6)                // Append multiple

val a = ArrayBuffer.range('a', 'h') 
a -= 'a'                           // Remove 'a'
a --= Seq('b', 'c')                // Remove multiple

// Updating
val b = ArrayBuffer.range(1, 5)
b(2) = 50                          // Index 2 becomes 50
b.update(0, 10)                    // Index 0 becomes 10

```

---

## 4. Map

A collection of **key-value pairs**. Below is the immutable version.

### Creation and Access

```scala
val states = Map(
  "AK" -> "Alaska",
  "AL" -> "Alabama",
  "AZ" -> "Arizona"
)

val ak = states("AK") // "Alaska"

// Iteration
for (k, v) <- states do println(s"key: $k, value: $v")

```

### Adding, Removing, and Updating

```scala
val a = Map(1 -> "one")
val b = a + (2 -> "two")          // Add
val c = b ++ Seq(3 -> "three")    // Add multiple

val d = c - 3                     // Remove key 3

val e = a.updated(1, "ONE!")      // Update

```

---

## 5. Set

An iterable collection with **no duplicate elements**.

### Creation and Logic

```scala
val nums = Set(1, 2, 3, 3, 3)      // Result: Set(1, 2, 3)

val a = Set(1, 2)
val b = a + 3                     // Add
val c = b ++ Seq(4, 1, 5)         // Add multiple (1 is dropped)

val d = c - 5                     // Remove

```

---

## 6. Range

Used to generate sequences of numbers, often for loops or populating other collections.

```scala
1 to 5             // 1, 2, 3, 4, 5
1 until 5          // 1, 2, 3, 4
1 to 10 by 2       // 1, 3, 5, 7, 9

// Converting Ranges
val x = (1 to 5).toList
val y = (1 to 5).toBuffer

// Specialized range methods
Vector.range(1, 5)
List.range(1, 10, 2)

```

---

## 🧠 Knowledge Check

1. **Which collection** should you use if you need fast "random access" by index but want to keep the data immutable?
2. What is the difference between the `::` and `:::` operators in a `List`?
3. Why does `Set(1, 2, 2, 3)` result in `Set(1, 2, 3)`?
4. If you are building a list of items over time and performance is a priority, why might you use an `ArrayBuffer` instead of a `List`?

---

## 🛠 Practical Exercise

**Task:** Create a mini "Inventory System."

1. Create an **ArrayBuffer** of Strings containing: `"Apple"`, `"Banana"`, `"Orange"`.
2. Add `"Grape"` to the end of the list.
3. Update `"Banana"` to `"Golden Banana"`.
4. Remove `"Apple"` from the list.
5. Convert the final `ArrayBuffer` into an **immutable List**.
6. Print the final list using a **for-loop**.

**Would you like me to provide the solution to the exercise or explain the complexity differences between List and Vector?**
