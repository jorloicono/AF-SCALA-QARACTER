This guide covers how to set up, build, and test projects using **sbt** (the standard build tool for Scala) and **ScalaTest**.

---

## 1. Setting Up a Basic "Hello, World" Project

You can create a minimal Scala project with just a few files without needing a complex directory structure.

### Steps:

1. 
**Preparation**: Ensure you have **Java 8 JDK** or higher installed.


2. 
**Initialize Folders**: Create a project directory and a subfolder named `project`.


```bash
mkdir hello
cd hello
mkdir project

```


3. 
**Configure sbt**: Inside the `project/` folder, create `build.properties`:


```scala
sbt.version = 1.6.1

```


4. 
**Configure Scala**: In the root directory, create `build.sbt`:


```scala
scalaVersion := "3.4.0"

```


5. 
**Write Code**: Create `Hello.scala`:


```scala
@main def helloWorld = println("Hello, world")

```


6. 
**Run**: Use the command `sbt run` to compile and execute.



---

## 2. Standard Directory Structure for Larger Projects

For professional or larger projects, sbt follows a standard directory structure similar to Maven.

* 
**`src/main/scala`**: Your application source code.


* 
**`src/test/scala`**: Your test files.


* 
**`project/`**: Contains `build.properties` (the sbt version).


* 
**`target/`**: Used by sbt for compiled files and working data.


* 
**`build.sbt`**: The main configuration file in the root directory.



---

## 3. Using ScalaTest for Project Testing

**ScalaTest** is a primary library for testing Scala applications. To use it, you must add it as a dependency in your `build.sbt` file.

### Adding Dependencies

In your `build.sbt`, add the following line to include the ScalaTest JAR files:

```scala
libraryDependencies ++= Seq(
  "org.scalatest" %% "scalatest" % "3.2.9" % Test
)

```

### Writing a Test (AnyFunSuite)

To write tests, your test class should extend `AnyFunSuite`.

**Example Test File (`src/test/scala/math/MathUtilsTests.scala`):**

```scala
package math
import org.scalatest.funsuite.AnyFunSuite

class MathUtilsTests extends AnyFunSuite:
  test("'double' should handle 0") {
    val result = MathUtils.double(0)
    assert(result == 0) // Check if condition is met
  }

  test("test with Int.MaxValue") (pending) // Use (pending) to finish later
end MathUtilsTests

```



---

## 4. Useful sbt Commands

* 
**`sbt run`**: Compiles and runs the main method in your project.


* 
**`sbt test`**: Executes all tests in the `src/test/scala` directory.


* 
**`sbt`**: Starts sbt in **interactive mode**, which is much faster for repeated commands.


* 
**`sbt new scala/scala3.g8`**: Creates a new project structure automatically from a template.



