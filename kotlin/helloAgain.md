./[curric](/curric)/[kotlin](/curric/kotlin)/[Hello_World](/curric/kotlin/helloAgain)/
# Hello World, the Re-run
Similar to Java, Kotlin has an entry point. This entry point is denoted as the main method
```kotlin
fun main() {
    println("Hello World")
}
```
All statements no longer require a semicolon to be at the end, a new line will suffice enough for the compiler to recognize it is a new statement.
Comments are still created with `//` before the comment.
Instead of `System.out.print` and `System.out.println`, Koltin shortened these methods to just `print` and `println`.
the `fun` keyword is Kotlin's way to define a method.
- Compile the application using the Kotlin compiler 
  - `kotlinc demo.kt -include-runtime -d demo.jar`
  - The -d option indicates the output path for generated class files which may be either a directory or a .jar file. The -include-runtime option makes the resulting .jar file self-contained and runnable by including the Kotlin runtime library in it. If you want to see all available options run

- Run the application.
    - `java -jar demo.jar`