## 1. Data Interchange: JSON with Circe

In Scala, we use **case classes** to represent data and **semi-automatic derivation** to convert them to/from JSON strings.

### The Practice Code

Copy this into Scastie (ensure you add `io.circe` dependencies in the "Build Settings" if not using a library preset).

```scala
import io.circe._, io.circe.generic.auto._, io.circe.parser._, io.circe.syntax._

// 1. Define your data model
case class User(id: Int, name: String, email: String, isActive: Boolean)

// 2. Serialization (Object -> JSON)
val user = User(1, "Alice", "alice@example.com", true)
val jsonString = user.asJson.spaces2 
println(s"Serialized JSON:\n$jsonString")

// 3. Deserialization (JSON -> Object)
val rawJson = """{"id": 2, "name": "Bob", "email": "bob@work.com", "isActive": false}"""
val decodedUser = decode[User](rawJson)

decodedUser match {
  case Right(user) => println(s"Decoded User Name: ${user.name}")
  case Left(error) => println(s"Error decoding: $error")
}

```

---

## 2. Persistence: File I/O

Since Scastie runs in a restricted sandbox, you can't always write to a permanent disk, but you can practice the **java.nio** or **scala.io** logic used in real applications.

### The Practice Code

```scala
import java.nio.file.{Paths, Files}
import java.nio.charset.StandardCharsets

val fileName = "user_data.json"
val content = jsonString // Using the JSON from the previous step

// Writing to a file
def saveFile(path: String, data: String): Unit = {
  Files.write(Paths.get(path), data.getBytes(StandardCharsets.UTF_8))
  println(f"File saved to $path")
}

// Reading from a file
def readFile(path: String): String = {
  val source = scala.io.Source.fromFile(path)
  try source.mkString finally source.close()
}

// Note: In Scastie, this might throw a SecurityException. 
// In a local project, this is how you persist your JSON.

```

---

## 3. Web Services: HTTP Client (sttp)

`sttp` is highly recommended because it is "The Scala Way"—typesafe and very readable.

### The Practice Code

```scala
// This requires the sttp dependency: "com.softwaremill.sttp.client3" %% "core" % "3.x.x"
import sttp.client3._

val backend = HttpURLConnectionBackend()
val request = basicRequest.get(uri"https://jsonplaceholder.typicode.com/users/1")

val response = request.send(backend)

response.body match {
  case Right(json) => 
    println("API Success!")
    // Here you would pipe this 'json' into your Circe decoder!
    val user = decode[User](json)
    println(user)
  case Left(error) => 
    println(s"API Error: $error")
}

```

---

## The "Final Boss" Challenge

To truly master this, try to combine all three in one Scastie worksheet:

1. **Fetch** a JSON list of "Todos" from `https://jsonplaceholder.typicode.com/todos`.
2. **Map** the JSON into a `List[Todo]` case class using **Circe**.
3. **Filter** the list to only include completed tasks.
4. **Write** that filtered list back into a string (JSON format) and "save" it.

### Recommended Libraries for your `build.sbt`:

If you move from Scastie to a local project, add these:

```scala
libraryDependencies ++= Seq(
  "com.softwaremill.sttp.client3" %% "core" % "3.8.15",
  "io.circe" %% "circe-core" % "0.14.5",
  "io.circe" %% "circe-generic" % "0.14.5",
  "io.circe" %% "circe-parser" % "0.14.5"
)

```

