./[curric](/curric)/[kotlin](/curric/kotlin)/
# Kotlin ( Java 2.0 )
This section will be a little different, instead of all of the content being written by us (Luke Early and Jaran Chao), a majority of the content in this section will be linking you to the Kotlin Language Official Docs as most topics we need to cover are explained very well in the Official Documentation.

## About Kotlin
Kotlin is a language developed by JetBrains and is open sourced at the [Kotlin Github](https://github.com/JetBrains/kotlin) under the Apache License (Version 2.0). Kotlin was created to address the many criticisms of Java. Many of which were already addressed by the JVM targetting language called Scala, however Scala's long compilation time was a trade off. One of the stated goals of Kotlin is to compile as quickly as Java. All Kotlin programs are compiled from source code (for humans to understand and write) into bytecode (for computers to understand), using the `kotlinc` compiler. The kotlin compiler hierarchy is changing all `.kt` (kotlin files) and `.kts` (kotlin script files) into `.class` file types which by the Java compiler can be compiled into `.jar` files which can be run on the JVM.

### What does Kotlin bring to the table?
- Kotlin is concise. Being concise means less code to read and write, increasing development speed.
- Kotlin has type inference. This plays in part to Kotlin being concise as it is not required to always state the type of the variable as the compiler is able to infer the type.
- Kotlin has built in null safety into its type system. This was to combat the tediousness of nullability checks in Java. We will go more in depth later on.
- Functional Programming. Kotlin brings many aspects of Functional Programming to the table. Functions are first class citizens of the global namespace. Higher Order functions and Lambdas are their own type, called Function Types. Many helper functions such as `map`, `filter`, `fold`, and `flatMap` are now member functions of Collections instead of being wrapped inside the Java Stream API. We will dive deeper into Function Programming later on.

#### Language Conventions
Kotlin Docs for: [Migrating to new a Code Style](https://kotlinlang.org/docs/reference/code-style-migration-guide.html)

## [Hello World the Re-run](./helloAgain)
## [Back to Basics](./basics)
## [OOP is BACK](./oop)
## [Functional Programming, but it is better](./func)
## [More Language Constructs](./more)
## [Concurrency Returns](./conc)