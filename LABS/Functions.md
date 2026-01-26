In Scala, functions are **first-class citizens**, meaning they can be treated like any other value (assigned to variables, passed as arguments, or returned).

---

## 1. Lambda Functions (Anonymous Functions)

Lambdas are functions that don't have a name. They are commonly passed to **Higher-Order Functions** like `map`, `filter`, or `foreach`.

### Syntax Styles

```scala
val ints = List(1, 2, 3)

// 1. Placeholder syntax (shortest)
val doubled = ints.map(_ * 2)

// 2. Explicit syntax (similar to Python's lambda)
val doubled2 = ints.map((i: Int) => i * 2)

// 3. Printing elements
ints.foreach(println(_))
// or even shorter:
ints.foreach(println)

```

---

## 2. Function Variables

You can store a function in a variable. This makes the logic reusable.

```scala
val double = (i: Int) => i * 2

val x = double(2)             // Invocation: 4
val list = ints.map(double)    // Passing as argument

```

---

## 3. Methods vs. Functions: Eta Expansion

A common question arises: Why can we pass a **method** (defined with `def`) into a function that expects a **Function object**?

### The Difference

* **Methods (`def`):** Members of a class or object. They are not objects themselves.
* **Functions (`val`):** Full-blown objects (instances of `FunctionN` traits).

### Eta Expansion

When you pass a method where a function is expected, Scala performs **Eta Expansion**. It "wraps" the method in a function object automatically.

```scala
def times10(i: Int) = i * 10       // This is a Method
val times10Func = (i: Int) => i * 10 // This is a Function

// In Scala 3, both work seamlessly in collections:
val methodsList = List(times10)    // Automatic conversion!

```

---

## 4. Higher-Order Functions (HOF)

An HOF is a function that takes another function as a parameter or returns one.

### Filter Example

```scala
val numbers = List(1, 2, 3, 4, 5, 6)
val evenNumbers = numbers.filter(_ % 2 == 0) // List(2, 4, 6)

```

### Passing Functions as Parameters

You can define your own HOFs by specifying the function signature in the parameters: `(InputType) => ReturnType`.

```scala
// Takes a function with no parameters and no return (Unit)
def sayHello(f: () => Unit): Unit = f()

def helloJoe(): Unit = println("Hello, Joe")
sayHello(helloJoe)

// Takes a function and an Int
def executeNTimes(f: () => Unit, n: Int): Unit =
  for i <- 1 to n do f()

executeNTimes(() => println("Hello"), 3)

```

### Complex Signatures

```scala
// Takes a function that accepts two Ints and returns an Int
def executeAndPrint(f: (Int, Int) => Int, i: Int, j: Int): Unit =
  println(f(i, j))

def sum(x: Int, y: Int) = x + y
def multiply(x: Int, y: Int) = x * y

executeAndPrint(sum, 3, 11)      // 14
executeAndPrint(multiply, 3, 9)   // 27

```

---

## 🧠 Knowledge Check

1. **What is the "Placeholder Syntax" in Scala?**
2. **Explain the difference in one sentence between a Method (`def`) and a Function (`val`).**
3. **What does "Eta Expansion" do when you pass `def myMethod` into `list.map(...)`?**

---

## 🛠 Practical Exercise

**Task: The "Math Operation" Runner**

1. Define a method called `subtract` that takes two `Int`s and returns the result.
2. Define a function variable (lambda) called `divide` that takes two `Int`s.
3. Create an HOF called `safeExecutor`. It should take:
* A function `f: (Int, Int) => Int`
* Two integers `a` and `b`.


4. The `safeExecutor` should check: **if b is 0** (for division), print a warning; otherwise, execute and print the result.
5. Test it with both your `subtract` method and `divide` function.

