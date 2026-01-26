## 🍃 Transforming Collections

In FP, you don't mutate the original collection. Instead, you apply functions to create a new one.

```scala
val a = List("jane", "jon", "mary", "joe")

// Transform 'a' into 'b' without touching 'a'
val b = a.filter(_.startsWith("j"))
         .map(_.capitalize)

// a: List("jane", "jon", "mary", "joe")
// b: List("Jane", "Jon", "Joe")

```

---

## 💎 Immutability & Case Classes

In FP, we avoid `var` in constructors. Instead, we use **Case Classes**, which are immutable by default (`val`). To "change" a value, we create a copy with the updated field.

```scala
// The FP Way: Case classes are immutable
case class Person(firstName: String, lastName: String)

val reginald = Person("Reginald", "Dwight")

// To "update," create a copy with new values
val elton = reginald.copy(
  firstName = "Elton",
  lastName = "John"
)

```

---

## 🛡️ Functional Error Handling: `Option`

Instead of throwing exceptions or returning `null` (which causes crashes), Scala uses the `Option` type. An `Option[T]` is a container that holds either **`Some(value)`** or **`None`**.

### Handling Exceptions with Option

```scala
def makeInt(s: String): Option[Int] =
  try {
    Some(Integer.parseInt(s.trim))
  } catch {
    case e: Exception => None
  }

val a = makeInt("1")   // Some(1)
val b = makeInt("one") // None

```

### Consuming Option Values

There are two primary ways to extract data from an `Option`:

#### 1. Using Pattern Matching

```scala
makeInt(x) match {
  case Some(i) => println(i)
  case None    => println("That didn’t work.")
}

```

#### 2. Using For-Expressions

This is perfect when you need to combine multiple optional values. If **any** value is `None`, the whole result becomes `None`.

```scala
val y = for {
  a <- makeInt("1")
  b <- makeInt("2")
  c <- makeInt("3")
} yield a + b + c

// y = Some(6)
// If any input were "abc", y would be None.

```

---

## 🚫 Replacing `null` with `Option`

Using `null` is often considered a "billion-dollar mistake" because it leads to `NullPointerException`. In Scala, we use `Option` to explicitly mark fields that might be missing.

### The "Old" Problem (Mutable & Nullable)

```scala
class Address(
  var street1: String,
  var street2: String, // Might be null!
  var city: String,
  var state: String,
  var zip: String
)

```

### The "Functional" Solution (Safe & Explicit)

By declaring `street2` as an `Option[String]`, the compiler forces you to handle the case where the data is missing.

```scala
class Address(
  var street1: String,
  var street2: Option[String], // Explicitly optional
  var city: String,
  var state: String,
  var zip: String
)

// No value
val santa = Address("1 Main St", None, "North Pole", "AK", "99705")

// With value
val apartment = Address("123 Main St", Some("Apt. 2B"), "Talkeetna", "AK", "99676")

```

---

## 🚀 Final Practice Exercise

**Scenario:** You have a `Map` of user IDs to names: `val users = Map(1 -> "alice", 2 -> "bob")`.

1. Create a method `getUserName(id: Int): Option[String]` that looks up the ID in the map (Maps return an `Option` automatically when using `.get(id)`).
2. Create a list of IDs: `List(1, 2, 3)`.
3. Use `map` and `getUserName` to transform the list of IDs into a list of `Option[String]`.
4. **Bonus:** Use `.flatten` on that list to remove all the `None` values and extract the strings from `Some`.

