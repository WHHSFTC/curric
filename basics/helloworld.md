./[curric](/curric)/[basics](/curric/basics)/[Hello-World](/curric/basics/helloworld)/
# Hello, World

A famous program often used to illustrate the syntax of languages is the "hello, world" program. When run, it does nothing but print the phrase "hello, world" out on the screen. Before we do this, you must learn two more things. First, the entry point of a simple Java program is contained in a block of code called a class, and within that a static function. It is not necessary to understand them at this point, but the boilerplate entry point looks like this:
```java
class Example {
    public static void main(String args[]) {
        // code goes here
    }
}
```
The second important piece of information are the functions `print()` and `println()` accessed by calling `System.out.print()` and `System.out.println()`. `print()` prints a parameter to the terminal output, while `println()` does the same but appends a `\n` character, which starts a new line. We will use the latter as it works better with the terminal:
```java
class HelloWorld {
    public static void main(String args[]) {
        System.out.println("hello, world");
     
}
```
Save this file as `HelloWorld.java`, then run `javac HelloWorld.java` in the terminal. This should produce the file `HelloWorld.class`, which you can run with the JVM via `java HelloWorld.class`.