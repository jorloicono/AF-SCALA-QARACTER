## 🛠 Scala Collections: The Power of Built-in Methods

Scala provides a consistent API across both **mutable** and **immutable** collections. This standardizes how developers manipulate data, making code more readable and maintainable.

### 1. Basic Navigation & Selection

These methods allow you to pick specific elements or slices of a list.

| Method | Description | Example |
| --- | --- | --- |
| `head` | Returns the first element. | `List(1, 2).head // 1` |
| `tail` | Returns everything *except* the first element. | `List(1, 2, 3).tail // List(2, 3)` |
| `last` | Returns the very last element. | `List(1, 2, 3).last // 3` |
| `init` | Returns everything *except* the last element. | `List(1, 2, 3).init // List(1, 2)` |
| `slice(from, until)` | Extracts a range based on indices. | `a.slice(2, 4)` |
| `distinct` | Removes duplicate values. | `List(1, 1, 2).distinct // List(1, 2)` |

---

### 2. Filtering: Extracting Data

Filtering creates a new collection containing only the elements that satisfy a specific condition (predicate).

```scala
val a = List(10, 20, 30, 40, 10)

// Syntax variations (all return List(10, 20, 10))
a.filter((i: Int) => i < 25) // 1. Explicit
a.filter(i => i < 25)        // 2. Inferred type
a.filter(_ < 25)             // 3. Wildcard (most common)

// Specialized filters
a.filterNot(_ < 25)          // List(30, 40)
a.find(_ > 20)               // Some(30) (returns Option)

```

---

### 3. Taking & Dropping

These are powerful tools for "trimming" your collections.

* **Take**: Keeps elements from the start/end or while a condition is met.
* **Drop**: Discards elements from the start/end or while a condition is met.

```scala
val oneToTen = (1 to 10).toList

oneToTen.take(2)          // List(1, 2)
oneToTen.takeRight(2)     // List(9, 10)
oneToTen.takeWhile(_ < 5) // List(1, 2, 3, 4)

oneToTen.drop(5)          // List(6, 7, 8, 9, 10)
oneToTen.dropWhile(_ < 5) // List(5, 6, 7, 8, 9, 10)

```

---

### 4. Transformation: `map`

`map` transforms every element in a collection using a function, returning a new collection of the same size.

```scala
val names = List("adam", "brandy", "chris", "david")

// Capitalize names
val capNames = names.map(_.capitalize) 

// Transform to a Map of (Name -> Length)
val nameLengthsMap = names.map(s => (s, s.length)).toMap 

// Chaining methods
// Filter numbers < 4, then multiply by 10
oneToTen.filter(_ < 4).map(_ * 10) // List(10, 20, 30)

```

---

### 5. Aggregation: `reduce`

The "Reduce" part of MapReduce. it combines all elements in a collection into a single value using a binary operation.

```scala
val a = List(1, 2, 3, 4)

// Using a named function for clarity
def add(x: Int, y: Int): Int = x + y
a.reduce(add) // 10

// Short forms
a.reduce(_ + _) // Sum: 10
a.reduce(_ * _) // Product: 24

```

---

## 🚀 Final Practice Exercise

**Scenario:** You have a list of prices. You need to:

1. Remove any prices higher than **$500**.
2. Apply a **10% discount** to the remaining prices.
3. Calculate the **total sum** of the discounted prices.

**Your Task:** Complete the code below using method chaining.

```scala
val prices = List(100.0, 50.0, 600.0, 250.0, 1000.0, 40.0)

// TODO: Filter prices <= 500, multiply by 0.90, and reduce with +
val total = prices
  .filter(______)
  .map(______)
  .reduce(______)

println(s"The total is: $$total") 
// Expected Result: The total is: 396.0

```

