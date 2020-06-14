./[curric](/curric)/[basics](/curric/basics)/
# Basics of Java
Java is a language originally developed by Sun Microsystems, and now by Oracle, which bought out Sun. Java has some advantages and some disadvantages when compared to other languages. All Java programs are compiled from source code (for humans to understand and write) into bytecode (for computers to understand), using the `javac` compiler. Most compiled languages must produce distinct binary files for each type of computer it may run on. With Java and its derived languages like Kotlin, the output of the compiler is made to run on an imaginary computer architecture that doesn't exist physically in any processor.

In order to run a Java program on your computer, you need[^1] to install a JVM, or Java Virtual Machine. As the name sounds, the JVM emulates this imaginary architecture by translating code into architecture-specific instructions as it is running. Unfortunately, this live translation of bytecode, paired with the storage of often irrelevant metadata, gives Java rather slow execution metrics. 

With only one program, a JVM doesn't make much sense. You still have to install an architecture and OS-specific executable for the JVM, even if there is only one version of the program written in Java. However, since Java is an immensely popular programming language, there are likely several applications on your device that all use the same JVM, each of those programs as a result had only one version to install across computers. This is not only more consumer-friendly, but also much simpler to write and maintain as a developer.

[^1]: Some ARM processors have a technology called Thumb, which basically integrates a low level JVM to allow "native" execution of Java bytecode.

## [Syntax](./syntax)
## [Hello, World!](./helloworld)
## [Operators](./operators)
## [Type](./type)
## [Functions](./function)
## [Loops](./loop)
## [If-Else Statements](./ifelse)