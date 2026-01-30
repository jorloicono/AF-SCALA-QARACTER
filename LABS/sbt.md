## Setup Instructions

1. **Open Scastie:** Go to [scastie.scala-lang.org](https://scastie.scala-lang.org).
2. **Configure Build Settings:**
* Click on **Build Settings** (the gear icon ⚙️ on the left).
* Ensure **Worksheet Mode** is **OFF** (ScalaTest needs to run as a standard program).
* In the **Extra sbt Configuration** or **Libraries** section, add the ScalaTest dependency:
```scala
libraryDependencies += "org.scalatest" %% "scalatest" % "3.2.18" % "test"

```




3. **The "Scastie Trick":** Since Scastie doesn't have a "Terminal" to run `sbt test`, you must trigger the test suite manually in the code using a `main` method.

---

## 📝 Practice Template

Copy this entire block into the Scastie editor. It includes a simple calculator to test and a `FunSuite` style test.

```scala
import org.scalatest.funsuite.AnyFunSuite

// 1. The code we want to test
object Calculator {
  def add(a: Int, b: Int): Int = a + b
  def multiply(a: Int, b: Int): Int = a * b
}

// 2. The Test Suite
class CalculatorTest extends AnyFunSuite {
  
  test("Addition: 2 + 3 should be 5") {
    assert(Calculator.add(2, 3) == 5)
  }

  test("Multiplication: 10 * 0 should be 0") {
    val result = Calculator.multiply(10, 0)
    assert(result == 0)
  }

  test("This test will fail intentionally") {
    assert(Calculator.add(1, 1) == 3)
  }
}

// 3. TRIGGER: Scastie needs this to actually run the tests
object Main {
  def main(args: Array[String]): Unit = {
    (new CalculatorTest).execute()
  }
}

```

---

## 🛠️ Testing Styles to Try

ScalaTest is famous for having multiple "styles." You can swap the `AnyFunSuite` above with these common alternatives to see which you prefer:

### 1. FlatSpec (BDD Style - "X should Y")

Great for readable, English-like requirements.

```scala
import org.scalatest.flatspec.AnyFlatSpec
import org.scalatest.matchers.should.Matchers

class CalcSpec extends AnyFlatSpec with Matchers {
  "A Calculator" should "add numbers correctly" in {
    Calculator.add(1, 2) should be (3)
  }
}

```

### 2. WordSpec (Nested BDD Style)

Useful for complex logic with many "if/when" scenarios.

```scala
import org.scalatest.wordspec.AnyWordSpec

class CalcWordSpec extends AnyWordSpec {
  "A Calculator" when {
    "adding numbers" should {
      "return a positive sum for positive inputs" in {
        assert(Calculator.add(1, 1) > 0)
      }
    }
  }
}

```

---

## 💡 Pro-Tips for Scastie

* **Console Output:** Watch the bottom panel (Console). ScalaTest will print a color-coded report showing which tests passed (green) and which failed (red).
* **Assertions:** Use `assert(a == b)` for basics, or mix in `Matchers` to use `a shouldBe b`.
* **Errors:** If you see `not found: type AnyFunSuite`, double-check that your `libraryDependencies` in Build Settings is correct and that you clicked **Save/Run** to let Scastie fetch the jar.


### Exercise 1: The String Manipulator (Beginner)

**Goal:** Implement a utility to handle string transformations.

1. **The Code:** Create an object `StringHelper`.
* `reverse(s: String)`: Returns the string reversed.
* `isPalindrome(s: String)`: Returns `true` if the string reads the same forward and backward (case-insensitive).


2. **The Test:** Use `AnyFunSuite`.
* Test that "scala" reversed becomes "alacs".
* Test that "Level" is identified as a palindrome.
* Test that "Hello" is **not** a palindrome.



---

### Exercise 2: The Shopping Cart (Intermediate)

**Goal:** Use TDD to build a simple cart logic. Write the tests *before* the implementation.

1. **The Code:** Create a class `ShoppingCart`.
* It should hold a `List` of prices (Doubles).
* `add(price: Double)`: Adds a price to the list.
* `total`: Returns the sum of all prices.
* `discountedTotal(percent: Double)`: Returns the total minus the percentage (e.g., 0.10 for 10%).


2. **The Test:** Use `AnyFlatSpec` with `Matchers`.
* "A ShoppingCart" should "start with a total of 0.0".
* "A ShoppingCart" should "correctly calculate the total after adding items".
* "A ShoppingCart" should "apply a 20% discount correctly".



---

### Exercise 3: The FizzBuzz Challenge (Logic & Edge Cases)

**Goal:** Practice handling multiple conditions and edge cases.

1. **The Code:** Create an object `FizzBuzz`.
* `process(n: Int)`: Returns "Fizz" if divisible by 3, "Buzz" if divisible by 5, "FizzBuzz" if divisible by both, and the number as a String otherwise.


2. **The Test:** Use `AnyWordSpec`.
* `"FizzBuzz processing"` when `"given a multiple of 3"` should `"return Fizz"`.
* `"FizzBuzz processing"` when `"given a multiple of 5"` should `"return Buzz"`.
* `"FizzBuzz processing"` when `"given 15"` should `"return FizzBuzz"`.
* `"FizzBuzz processing"` when `"given a negative number"` should (decide your behavior—perhaps throw an `IllegalArgumentException` and test it using `intercept[IllegalArgumentException]`).



---

### How to run these in Scastie:

Remember to wrap your test execution in the `Main` object so Scastie triggers it:

```scala
object Main {
  def main(args: Array[String]): Unit = {
    // Run your suites here
    (new StringHelperTest).execute()
    (new ShoppingCartSpec).execute()
    (new FizzBuzzWordSpec).execute()
  }
}
