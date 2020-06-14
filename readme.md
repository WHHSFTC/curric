# Programming Curriculum
In FTC, we primarily use two programming languages: Java and Kotlin. We will start with Java, as it is the basis for Kotlin. If you've taken CSA with Dr. Gordon, then this should be review.

## Functional Programming

### Anonymous Classes
- Anonymous Classes are inner classes without a name and for which only a single object is created. An anonymous inner class can be useful when making an instance of an object with certain “extras” such as overloading methods of a class or interface, without having to actually subclass a class.
  For example:
  If you had a interface Age
  ```java=
  interface Age {
      int a = 21;
      int getAge();
  }
  ```
  and you had a class Person that implements the Age interface
  ```java=
  class Person implements Age {
      @Override
      public int getAge() {
          return a;
      }
  }
  ```
  and you were creating a new Person object
  ```java=
  class Main {
      public static void main(String[] args) {
          Person me = new Person();
          System.out.println(me.getAge());
      }
  }
  ```
  instead of having to create a class that implements the Age interface, you could use an anonymous class instead
  ```java=
  class Main {
      public static void main(String[] args) {
          Age me = new Age() {
              @Override
              public int getAge() {
                  return a;
              }
          };
          System.out.println(me.getAge());
      }
  }
  ```
  this will act the same as the example with the Person class, but in this is example, the "Person" class is now an anonymous inner class of Age
### Functional Interfaces
- Thanks to Java 8 ( which is the version of Java you will be using ), functional interfaces were introduced, which replaced the need for anonymouse classes.
- A functional interface is an interface that contains only one abstract method. They can have only one functionality to exhibit. From Java 8 onwards, lambda expressions can be used to represent the instance of a functional interface. A functional interface can have any number of default methods.
  To use Functional Interfaces, put the @FunctionalInterface annotation above the interface and make sure that the interface only has one abstract method
  For example
  ```java=
  @FunctionalInterface
  interface Calculator {
      int calculate(int x, int y);
  }
  ```
  this is now a functional interface that can be called with lambda syntax.
### Lambdas ( The better Anonymous class )
- Lambda expressions basically express instances of functional interfaces. Lambda expressions implement the only abstract function and therefore implement functional interfaces
  Lets say, for example if we had the functional interface:
  ```java=
  @FunctionalInterface
  interface Calculator {
      int calculate(int x, int y);
  }
  ```
  we could use lambdas to express instances of Calculator
  ```java=
  class Main {
      public static void main(String[] args) {
          int a = 5;
          int b = 6;
          
          Calculator add = (int x, int y) -> x + y;
          
          int result = add.calculate(a, b); // 11
      }
  }
  ```
  In this example, we are using a lambda expression to define the calculate method from the interface calculator. In this case, we said that the calculate function would do addition of the two int parameters passed in.
- The java.util.function package in Java 8 contains many builtin functional interfaces like
- Predicate: The Predicate interface has an abstract method test which gives a Boolean value as a result for the specified argument. Its prototype is
  ```java=
  public interface Predicate<T>{
      public boolean test(T t);
  }
  ```
- BinaryOperator: The BinaryOperator interface has an abstract method apply which takes two argument and returns a result of same type. Its prototype is
  ```java=
  public interface BinaryOperator<T> {
      public T apply(T x, T y);
  }
  ```
- Function: The Function interface has an abstract method apply which takes argument of type T and returns a result of type R. Its prototype is
  ```java=
  public interface Function<T, R> {
      public R apply(T t);
  }
  ```
### Method References ( The less anonymous lambdas )
- You use lambda expressions to create anonymous methods. Sometimes, however, a lambda expression does nothing but call an existing method. In those cases, it's often clearer to refer to the existing method by name. Method references enable you to do this; they are compact, easy-to-read lambda expressions for methods that already have a name.
  For example, using the Arrays.sort method
  using Lambda and compareTo
  ```java=
  String[] arr = new String[] { "a", "b", "c", "d"};
  
  Arrays.sort(arr,
      (a, b) -> a.compareTo(b)
  );
  ```
  however, the lambda is really only just calling the String.compareTo(String other) method, so we can just use a method reference instead, since the method called by the lambda already exists.
  ```java=
  String[] arr = new String[] { "a", "b", "c", "d"};
  
  Arrays.sort(arr, String::compareTo);
  ```
### Java Streams ( the functional API for Java Collections )
- Java Streams is an API that applies a specific action (filter, map, or reduce) over the entire collection. After applying the specific action, a new modified collection is returned, allowing for method chaining (do operators one after another)
  ```java=
  // Example of Chaining
  originalCollection.firstMethod().secondMethod().finalMethod()
  
  // syntax guidelines state to put a newline 
  // before every new method call for readability 
  originalCollection
      .firstMethod()
      .secondMethod()
      .finalMethod()
  ```
- Types of Streams
    - `Stream<T>`
        - Generic Stream of type T where T extends Object
    - `IntStream`
        - Stream of type int wrapped in Integer object, and also adding specific syntactic sugar methods such as sum, average, and count
    - `LongStream`
        - Stream of type long wrapped in Long object, and also adding specific syntactic sugar methods such as sum, average, and count
    - `DoubleStream`
        - Stream of type double wrapped in Double object, and also adding specific syntactic sugar methods such as sum, average, and count
- Essential Stream Functions
    - `map`
        - Returns a stream consisting of the results of applying the given function to the elements of this stream.
        - `mapToInt`
            - applies map and specifically returns IntStream
        - `mapToDouble`
            - applies map and specifically return DoubleStream
        - `mapToLong`
            - applies map and specifically return LongStream
    - `filter`
        - Returns a stream consisting of the elements of this stream that match the given predicate.
    - `forEach`
        - Performs an action for each element of this stream.
    - `reduce`
        - Performs a reduction on the elements of this stream, using an associative accumulation function, and returns an Optional describing the reduced value, if any.
    - `collect`
        - Performs a mutable reduction operation on the elements of this stream using a Collector.

## Concurrency
Concurrency, in the context of computer science, is the ability for a program to be decomposed into parts that can run independently of each other. This means that tasks can be executed out of order and the result would still be the same as if they are executed in order. It is the ability of an algorithm or program to run more than one task at a time. The concept is similar to parallel processing, but with the possibility of many independent jobs doing different things at once rather than executing the same job.

### Synchronous vs Asynchronous Code
- Synchronous Code
    - Synchronous Code is code that is executed sequentially, and if a section of code is considered "blocking" then the entire sequence of code will stop and wait until the "blocking" section finishes.
    :::info
    Blocking Code is code that stops the rest of the program until the sequence of blocking code is complete. Most common examples of blocking code are loops and sleep statements.
    :::
- Asynchronous Code
    - Asynchronous Code is code that is executed concurrently with the rest of the code. Asynchronous code eliminates the need to wait for previous blocking calls to complete. This allows for greater time optimizations and allows for multiple tasks to run in parallel. A rule of thumb with asynchronous code is that every separate _thread_ doesn't affect another.

### Threads (The Java Approach)
Multithreading is a Java feature that allows concurrent execution of two or more parts of a program for maximum utilization of CPU. Each part of such program is called a thread.

There are three different types of Threads.

- Native Threads
    - Native Threads are Threads that, once created, are handled by the underlying operating system (OS) more commonly known as Kernel Threads. An upside to Kernel Threads is that when a Kernel Thread is blocked, other Kernel Threads can continue execution. 
- Green Threads
    - Green Threads are threads that are scheduled by a runtime library or virtual machine (VM) instead of natively by the underlying OS. Green threads emulate multithreaded environments without relying on any native OS abilities, and they are managed in user space instead of kernel space, enabling them to work in environments that do not have native thread support. In Java 1.1, green threads were the only threading model used by the Java virtual machine (JVM), at least on Solaris. As green threads have some limitations compared to native threads, subsequent Java versions dropped them in favor of native threads.
- Daemon Threads
    - Daemon thread is a low priority thread that runs in background to perform tasks such as garbage collection. They can not prevent the JVM from exiting when all the user threads finish their execution. JVM terminates itself when all user threads finish their execution. If JVM finds running daemon thread, it terminates the thread and after that shutdown itself. JVM does not care whether Daemon thread is running or not. It is an utmost low priority thread. An example of a Daemon Thread is Java Garbage Collection.

#### Creating and Starting Threads in Java
Threads are apart of the Java Standard Library in java.lang. To import threads, use `import java.lang.Thread;`

To create Threads, invoke the Thread constructor with the new keyword. There are 8 different Thread constructors.

- `Thread()`
    - Allocates a new Thread object with an empty Runnable target.
- `Thread(Runnable target)`
    - Allocates a new Thread object with a target Runnable.
- `Thread(Runnable target, String name)`
    - Allocates a new Thread object with a target Runnable and with the replacement name.
- `Thread(String name)`
    - Allocates a new Thread object with an empty Runnable target with the replacement name.
- `Thread(ThreadGroup group, Runnable target)`
    - Allocates a new Thread object and ties it to the ThreadGroup with a target Runnable.
- `Thread(ThreadGroup group, Runnable target, String name)`
    - Allocates a new Thread object so that it has target as its run object, has the specified name as its name, and belongs to the thread group referred to by group.
- `Thread(ThreadGroup group, Runnable target, String name, long stackSize)`
    - Allocates a new Thread object so that it has target as its run object, has the specified name as its name, and belongs to the thread group referred to by group, and has the specified stack size.
- `Thread(ThreadGroup group, String name)`
    - Allocates a new Thread object and belongs to the ThreadGroup and with the replacement name.

The most common Thread constructor that you will use it the `Thread(Runnable Thread)`

In these next example, we will create a new thread that will print the current Thread's name and ID.

Here we extend the Thread class to create our custom Thread.
```java=
import java.lang.Thread;

class ThreadDemo extends Thread {
  public void run() {
    System.out.println("Name: " + Thread.currentThread().getName() + ", ID: " + Thread.currentThread().getId());
  }
}

class Main {
  public static void main(String[] args) {
    int n = 8; // number of threads
    for (int i = 0; i < n; i++) {
      ThreadDemo t = new ThreadDemo();
      // we call the default constructor 
      // we dont need to supply a Runnable object as
      // run function is already defined inside ThreadDemo
      // and that function will be the target function
      // that will be called when the Thread starts
      t.start();
    }
  }
}
```
Output (all will look relatively like this)
```
Name: Thread-6, ID: 16
Name: Thread-4, ID: 14
Name: Thread-2, ID: 12
Name: Thread-5, ID: 15
Name: Thread-1, ID: 11
Name: Thread-7, ID: 17
Name: Thread-3, ID: 13
Name: Thread-0, ID: 10
```

Here we implement the Runnable Interface to achieve the same output
```java=
import java.lang.Thread;
import java.lang.Runnable;

class RunnableDemo implements Runnable {
  public void run() {
    System.out.println("Name: " + Thread.currentThread().getName() + ", ID: " + Thread.currentThread().getId());
  }
}

class Main {
  public static void main(String[] args) {
    int n = 8; // number of threads
    for (int i = 0; i < n; i++) {
      Thread t = new Thread(new RunnableDemo());
      // here we supply a Runnable in the one args constructor
      // the run function defined in the RunnableDemo class
      // will be used as the target run function called
      // when the thread is started
      t.start();
    }
  }
}
```

We can also use an anonymous class
```java=
import java.lang.Thread;

class Main {
  public static void main(String[] args) {
    int n = 8; // number of threads
    for (int i = 0; i < n; i++) {
      Thread t = new Thread() {
        public void run() {
          System.out.println("Name: " + Thread.currentThread().getName() + ", ID: " + Thread.currentThread().getId());
        }
      };
      // here we create an anonymous thread class that 
      // overrides the run function
      // this run function will be used as the target function
      // when the Thread is started
      t.start();
    }
  }
}
```

Lastly, we can also use lambda syntax to create a new Thread
```java=
import java.lang.Thread;

class Main {
  public static void main(String[] args) {
    int n = 8; // number of threads
    for (int i = 0; i < n; i++) {
      Thread t = new Thread(
        () -> System.out.println("Name: " + Thread.currentThread().getName() + ", ID: " + Thread.currentThread().getId())
      );
      // the lambda supplied is a SAM type 
      // of the functional interface Runnable
      // and the lambda function is the run function
      // that will be used as the target function by the thread when started
      t.start();
    }
  }
}
```

All of these examples are valid methods of creating new threads. However, some are sytactically easier than others. (_cough cough ~~lambda~~ cough cough_)

## Kotlin ( Java 2.0 )
This section will be a little different, instead of all of the content being written by us (Luke Early and Jaran Chao), a majority of the content in this section will be linking you to the Kotlin Language Official Docs as most topics we need to cover are explained very well in the Official Documentation.

### About Kotlin
Kotlin is a language developed by JetBrains and is open sourced at the [Kotlin Github](https://github.com/JetBrains/kotlin) under the Apache License (Version 2.0). Kotlin was created to address the many criticisms of Java. Many of which were already addressed by the JVM targetting language called Scala, however Scala's long compilation time was a trade off. One of the stated goals of Kotlin is to compile as quickly as Java. All Kotlin programs are compiled from source code (for humans to understand and write) into bytecode (for computers to understand), using the `kotlinc` compiler. The kotlin compiler hierarchy is changing all `.kt` (kotlin files) and `.kts` (kotlin script files) into `.class` file types which by the Java compiler can be compiled into `.jar` files which can be run on the JVM.

#### What does Kotlin bring to the table?
- Kotlin is concise. Being concise means less code to read and write, increasing development speed.
- Kotlin has type inference. This plays in part to Kotlin being concise as it is not required to always state the type of the variable as the compiler is able to infer the type.
- Kotlin has built in null safety into its type system. This was to combat the tediousness of nullability checks in Java. We will go more in depth later on.
- Functional Programming. Kotlin brings many aspects of Functional Programming to the table. Functions are first class citizens of the global namespace. Higher Order functions and Lambdas are their own type, called Function Types. Many helper functions such as `map`, `filter`, `fold`, and `flatMap` are now member functions of Collections instead of being wrapped inside the Java Stream API. We will dive deeper into Function Programming later on.

### Hello World, the Re-run
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

#### Language Conventions
Kotlin Docs for: [Migrating to new a Code Style](https://kotlinlang.org/docs/reference/code-style-migration-guide.html)

### Back to Basics
#### Variables
Variables can be declared two different ways. val or var. Depending on if the variable is val or var, the variable will behave differently.

The type of the variable in Kotlin can be either explicitly given or the type can be inferred. To explicitly define the type, place a `:` after the variable name and then the type.
```kotlin=
var name: Type
```
##### Val vs Var
- Val
    - Defining a variable with the `val` keyword makes the variable read-only.
    :::info
    Read-only variables are variables that can only be assigned a value once.
    :::
    ```kotlin=
    val a: Int = 9 // explicit typing, immediate assignment of value
    val b = 2 // Type 'Int' is inferred
    val c: Int // Type is required when no initializer is provided
    c = 3
    ```
- Var
    - Defining a variable with the `var` keyword allows the variable to be reassigned.
    ```kotlin=
    var x = 5 // Type 'Int' is inferred
    x += 1
    ```
#### Basic Types
##### Numbers
In Kotlin, everything is an object in the sense that we can call member functions and properties on any variable. Some of the types can have a special internal representation - for example, numbers, characters and booleans can be represented as primitive values at runtime - but to the user they look like ordinary classes. In this section we describe the basic types used in Kotlin: numbers, characters, booleans, arrays, and strings.
- Byte, Short, Int, Long
    - All variables initialized with integer values not exceeding the maximum value of Int have the inferred type Int. If the initial value exceeds this value, then the type is Long. To specify the Long value explicitly, append the suffix L to the value.

    | Type | Size (bits) | Min value | Max value |
    |------|-------------|-----------|-----------|
    | Byte |8            |-128       |127        |
    | Short|16           |-32768     |32767      |
    |Int   |32           |-2,147,483,648 (-2^31)|	2,147,483,647 (2^31 - 1)|
    |Long  |64           |-9,223,372,036,854,775,808 (-2^63)|9,223,372,036,854,775,807 (2^63 - 1)|
    ```kotlin=
    val one = 1 // Int
    val threeBillion = 3000000000 // Long
    val oneLong = 1L // Long
    val oneByte: Byte = 1
    ```
- Float, Double
    - For floating-point numbers, Kotlin provides types Float and Double. According to the IEEE 754 standard, floating point types differ by their decimal place, that is, how many decimal digits they can store. Float reflects the IEEE 754 single precision, while Double provides double precision.

    | Type | Size (bits) | Significant bits | Exponent bits | Decimal Digits |
    | -------- | -------- | -------- | -------- | -------- |
    | Float    | 32  | 24     |   8       |  6-7         |
    | Float    | 64  | 53     |   11      |  15-16       |
    
    - For variables initialized with fractional numbers, the compiler infers the Double type. To explicitly specify the Float type for a value, add the suffix f or F. If such a value contains more than 6-7 decimal digits, it will be rounded.
    ```kotlin=
    val pi = 3.14 // Double
    val e = 2.7182818284 // Double
    val eFloat = 2.7182818284f // Float, actual value is 2.7182817
    ```
    - Note that unlike some other languages (Java in particular), there are no implicit widening conversions for numbers in Kotlin. For example, a function with a Double parameter can be called only on Double values, but not Float, Int, or other numeric values.
    ```kotlin=
    fun main() {
        fun printDouble(d: Double) { print(d) }

        val i = 1    
        val d = 1.1
        val f = 1.1f 

        printDouble(d)
        //    printDouble(i) // Error: Type mismatch
        //    printDouble(f) // Error: Type mismatch
    }
    ```
    - To convert numeric values to different types, use Explicit conversions.

##### Explicit Conversion
Due to different representations, smaller types are not subtypes of bigger ones. If they were, we would have troubles of the following sort:
```kotlin=
// Hypothetical code, does not actually compile:
val a: Int? = 1 // A boxed Int (java.lang.Integer)
val b: Long? = a // implicit conversion yields a boxed Long (java.lang.Long)
print(b == a) // Surprise! 
/* This prints "false" as Long's equals() 
 * checks whether the other is Long as well
 */
```
So equality would have been lost silently all over the place, not to mention identity.

As a consequence, smaller types are NOT implicitly converted to bigger types. This means that we cannot assign a value of type Byte to an Int variable without an explicit conversion
```kotlin=
val b: Byte = 1 // OK, literals are checked statically
val i: Int = b // ERROR
```
We can use explicit conversions to widen numbers
```kotlin=
val i: Int = b.toInt() // OK: explicitly widened
print(i)
```
Every number type supports the following conversions:

- `toByte(): Byte`
- `toShort(): Short`
- `toInt(): Int`
- `toLong(): Long`
- `toFloat(): Float`
- `toDouble(): Double`
- `toChar(): Char`

Absence of implicit conversions is rarely noticeable because the type is inferred from the context, and arithmetical operations are overloaded for appropriate conversions, for example
```kotlin=
val l = 1L + 3 // Long + Int => Long
```
- Operations
    Kotlin supports the standard set of arithmetical operations over numbers (`+` `-` `*` `/` `%`), which are declared as members of appropriate classes (but the compiler optimizes the calls down to the corresponding instructions)
    
:::info
Division of Integers
- Note that division between integers always returns an integer. Any fractional part is discarded. For example:
```kotlin=
val x = 5 / 2 // returns 2 and not 2.5 due to decimal point cutoff
// println(x == 2.5) // ERROR
// Operator '==' cannot be applied to 'Int' and 'Double'
println(x == 2)
```
This is true for a division between any two integer types.
```kotlin=
val x = 5L / 2
println(x == 2L)
```
To return a floating-point type, explicitly convert one of the arguments to a floating-point type.
```kotlin=
val x = 5 / 2.toDouble() // equivalent to 5 / 2.0
println(x == 2.5)
```
:::
##### Bitwise Operations
As for bitwise operations, there're no special characters for them, but just named functions that can be called in infix form, for example:
```kotlin=
val x = (1 shl 2) and 0x000FF000
```
Here is the complete list of bitwise operations (available for `Int` and `Long` only):

- `shl(bits)` – signed shift left
- `shr(bits)` – signed shift right
- `ushr(bits)` – unsigned shift right
- `and(bits)` – bitwise and
- `or(bits)` – bitwise or
- `xor(bits)` – bitwise xor
- `inv()` – bitwise inversion
##### Floating point numbers comparison
The operations on floating point numbers discussed in this section are:

Equality checks: `a == b` and `a != b`
Comparison operators: `a < b`, `a > b`, `a <= b`, `a >= b`
Range instantiation and range checks: `a..b`, `x in a..b`, `x !in a..b`
:::info
`a..b` is a Range type, this will be covered later
:::
When the operands `a` and `b` are statically known to be `Float` or `Double` or their nullable counterparts (the type is declared or inferred or is a result of a smart cast), the operations on the numbers and the range that they form follow the IEEE 754 Standard for Floating-Point Arithmetic.

However, to support generic use cases and provide total ordering, when the operands are not statically typed as floating point numbers (e.g. `Any`, `Comparable<...>`, a type parameter), the operations use the `equals` and `compareTo` implementations for `Float` and `Double`, which disagree with the standard, so that:

- `NaN` is considered equal to itself
- `NaN` is considered greater than any other element including POSITIVE_INFINITY
- `-0.0` is considered less than 0.0

##### Character
Characters are represented by the type Char. They can not be treated directly as numbers
```kotlin=
fun check(c: Char) {
    if (c == 1) { // ERROR: incompatible types
        // ...
    }
}
```
Character literals go in single quotes: `'1'`. Special characters can be escaped using a backslash. The following escape sequences are supported: `\t`, `\b`, `\n`, `\r`, `\'`, `\"`, `\\` and `\$`. To encode any other character, use the Unicode escape sequence syntax: `'\uFF00'`.

We can explicitly convert a character to an `Int` number:
```kotlin=
fun decimalDigitValue(c: Char): Int {
    if (c !in '0'..'9') 
    // checks if the character is
    // between 0 and 9 on the ascii table
        throw IllegalArgumentException("Out of range")
    return c.toInt() - '0'.toInt() // Explicit conversions to numbers
}
```
:::info
ASCII is the numeric representation of characters that the computer sees
:::
Like numbers, characters are boxed when a nullable reference is needed. Identity is not preserved by the boxing operation.
##### Booleans
The type Boolean represents booleans, and has two values: true and false.

Booleans are boxed if a nullable reference is needed.

Built-in operations on booleans include

`||` – lazy disjunction - Or
`&&` – lazy conjunction - And
`!` - negation - Not

#### Advance Types
##### Arrays
Arrays in Kotlin are represented by the `Array` class, that has `get` and `set` functions (that turn into `[]` by operator overloading conventions), and `size` property, along with a few other useful member functions:
```kotlin=
class Array<T> private constructor() {
    val size: Int
    operator fun get(index: Int): T
    operator fun set(index: Int, value: T): Unit

    operator fun iterator(): Iterator<T>
    // ...
}
```
To create an array, we can use a library function arrayOf() and pass the item values to it, so that arrayOf(1, 2, 3) creates an array [1, 2, 3]. Alternatively, the arrayOfNulls() library function can be used to create an array of a given size filled with null elements.

Another option is to use the Array constructor that takes the array size and the function that can return the initial value of each array element given its index:
```kotlin=
// Creates an Array<String> with values ["0", "1", "4", "9", "16"]
val asc = Array(5) { i -> (i * i).toString() }
// {} after the array constructor is 
// kotlin syntactic sugar for calling lambdas
asc.forEach { println(it) }
// same with the {} after the forEach
```
As we said above, the `[]` operation stands for calls to member functions `get()` and `set()`.

Arrays in Kotlin are invariant. This means that Kotlin does not let us assign an `Array<String>` to an `Array<Any>`, which prevents a possible runtime failure (but you can use `Array<out Any>` which we will get to later in the Generics Section)
##### Primitive type arrays
Kotlin also has specialized classes to represent arrays of primitive types without boxing overhead: ByteArray, ShortArray, IntArray and so on. These classes have no inheritance relation to the Array class, but they have the same set of methods and properties. Each of them also has a corresponding factory function:
```kotlin=
val x: IntArray = intArrayOf(1, 2, 3)
x[0] = x[1] + x[2]
```
```kotlin=
// Array of int of size 5 with values [0, 0, 0, 0, 0]
val arr = IntArray(5)

// e.g. initialise the values in the array with a constant
// Array of int of size 5 with values [42, 42, 42, 42, 42]
val arr = IntArray(5) { 42 }

// e.g. initialise the values in the array using a lambda
// Array of int of size 5 with values [0, 1, 2, 3, 4]
// (values initialised to their index value)
var arr = IntArray(5) { it * 1 }
```
##### Strings
Strings are represented by the type String. Strings are immutable. Elements of a string are characters that can be accessed by the indexing operation: `s[i]`. A string can be iterated over with a for-loop:
```kotlin=
for (c in str) {
    println(c)
}
```
:::info
All Kotlin for loops act like Java for-each loops, through the use of iterators.
:::
You can concatenate strings using the `+` operator. This also works for concatenating strings with values of other types, as long as the first element in the expression is a string:
```kotlin=
val s = "abc" + 1
println(s + "def")
```
:::info
Note that in most cases using string templates or raw strings is preferable to string concatenation.
:::
##### String Literals
Kotlin has two types of string literals: escaped strings that may have escaped characters in them and raw strings that can contain newlines and arbitrary text. Here's an example of an escaped string:
```kotlin=
val s = "Hello, world!\n"
```
Escaping is done in the conventional way, with a backslash. See Characters above for the list of supported escape sequences.

A raw string is delimited by a triple quote ("""), contains no escaping and can contain newlines and any other characters:
```kotlin=
val text = """
    for (c in "foo")
        print(c)
"""
```
You can remove leading whitespace with `trimMargin()` function:
```kotlin=
val text = """
    |Tell me and I forget.
    |Teach me and I remember.
    |Involve me and I learn.
    |(Benjamin Franklin)
    """.trimMargin()
```
By default | is used as margin prefix, but you can choose another character and pass it as a parameter, like `trimMargin(">")`.
##### String Templates
String literals may contain template expressions, i.e. pieces of code that are evaluated and whose results are concatenated into the string. A template expression starts with a dollar sign ($) and consists of either a simple name:
```kotlin=
val i = 10
println("i = $i") // prints "i = 10"
```
or an arbitrary expression in curly braces:
```kotlin=
val s = "abc"
println("$s.length is ${s.length}") // prints "abc.length is 3"
```
Templates are supported both inside raw strings and inside escaped strings. If you need to represent a literal $ character in a raw string (which doesn't support backslash escaping), you can use the following syntax:
```kotlin=
val price = """
${'$'}9.99
"""
```

#### Control Flow
Kotlin Docs for: [Control Flow](https://kotlinlang.org/docs/reference/control-flow.html#control-flow-if-when-for-while)
- [Returns and Jumps](https://kotlinlang.org/docs/reference/returns.html)

#### Functions
Kotlin Docs for: [Functions](https://kotlinlang.org/docs/reference/functions.html)

#### Null Safety
Kotlin Docs for: [Null Safety](https://kotlinlang.org/docs/reference/null-safety.html)

#### New Types
- Any
    - The root of the Kotlin class hierarchy. Every Kotlin class has Any as a superclass.
- Nothing
    - Nothing has no instances. You can use Nothing to represent "a value that never exists": for example, if a function has the return type of Nothing, it means that it never returns (always throws an exception).
- Unit
    - For Common, JVM, JS
        - The type with only one value: the Unit object. This type corresponds to the void type in Java.
    - For Native
        - The type with only one value: the Unit object.
- Dynamic (JS only)
    - For JS
        - when a variable set to Type `dynamic`, type checking is turned off to mimic the dynamic type system of the JS enviroment
#### Kotlin Type Hierarchy
Every Type in Kotlin has 2 forms: A non-nullable form and a nullable form (denoted with a `?`)
![](https://i.imgur.com/fgO0TDn.png)
However
![](https://i.imgur.com/Q5G2EGU.png)
This means that if a parameter is created as an instance of `Int`, you are still able to pass in an `Int?` as `Int?` is a "super" type of `Int`. Therefore all Nullable Types are a **super** type of the Non-Nullable Type

#### Collections
##### Collection, List, Set, Map
Kotlin Docs for:
- [Overview of Collections](https://kotlinlang.org/docs/reference/collections-overview.html)
- [Constructing Collections](https://kotlinlang.org/docs/reference/constructing-collections.html)

##### Iterators
Kotlin Docs for: [Iterators](https://kotlinlang.org/docs/reference/iterators.html)

##### Ranges and Progressions
Kotlin Docs for: [Ranges and Progressions](https://kotlinlang.org/docs/reference/ranges.html)

##### Sequences
Kotlin Docs for: [Sequences](https://kotlinlang.org/docs/reference/sequences.html)

##### Operations on Collections
Kotlin Docs for:
- [Operations on Collections Overview](https://kotlinlang.org/docs/reference/collection-operations.html)
- [Collection Write Operations](https://kotlinlang.org/docs/reference/collection-write.html)
- Specific Operations
    - [List](https://kotlinlang.org/docs/reference/list-operations.html)
    - [Set](https://kotlinlang.org/docs/reference/set-operations.html)
    - [Map](https://kotlinlang.org/docs/reference/map-operations.html)

### OOP is back
#### Classes in Kotlin
Kotlin Docs for: [Classes and Inheritance](https://kotlinlang.org/docs/reference/classes.html)

#### Open vs Sealed
- Open
    All classes in Kotlin have a common superclass `Any`, that is the default superclass for a class with no supertypes declared:
    ```kotlin=
    class Example // Implicitly inherits from Any
    ```
    `Any` has three methods: `equals()`, `hashCode()` and `toString()`. Thus, they are defined for all Kotlin classes.
    By default, Kotlin classes are final: they can’t be inherited. To make a class inheritable, mark it with the `open` keyword.
    ```kotlin=
    open class Base //Class is open for inheritance
    ```
    To declare an explicit supertype, place the type after a colon in the class header:
    ```kotlin=
    open class Base(p: Int)
    
    class Derived(p: Int) : Base(p)
    ```
    If the derived class has a primary constructor, the base class can (and must) be initialized right there, using the parameters of the primary constructor.
    
    If the derived class has no primary constructor, then each secondary constructor has to initialize the base type using the super keyword, or to delegate to another constructor which does that. Note that in this case different secondary constructors can call different constructors of the base type:
    ```kotlin=
    class MyView : View {
        constructor(ctx: Context) : super(ctx)

        constructor(ctx: Context, attrs: AttributeSet): super(ctx, attrs)
    }
    ```
- Sealed
    - Kotlin Docs for: [Sealed Classes](https://kotlinlang.org/docs/reference/sealed-classes.html)

#### Lateinit
##### Late-Initialized Properties and Variables
Normally, properties declared as having a non-null type must be initialized in the constructor. However, fairly often this is not convenient. For example, properties can be initialized through dependency injection, or in the setup method of a unit test. In this case, you cannot supply a non-null initializer in the constructor, but you still want to avoid null checks when referencing the property inside the body of a class.

To handle this case, you can mark the property with the `lateinit` modifier:
```kotlin=
public class MyTest {
    lateinit var subject: TestSubject

    @SetUp fun setup() {
        subject = TestSubject()
    }

    @Test fun test() {
        subject.method()  // dereference directly
    }
}
```
The modifier can be used on `var` properties declared inside the body of a class (not in the primary constructor, and only when the property does not have a custom getter or setter) and, since Kotlin 1.2, for top-level properties and local variables. The type of the property or variable must be non-null, and it must not be a primitive type.

Accessing a `lateinit` property before it has been initialized throws a special exception that clearly identifies the property being accessed and the fact that it hasn't been initialized.

##### Checking whether a lateinit var is initialized (since 1.2)
To check whether a `lateinit var` has already been initialized, use `.isInitialized` on the [reference to that property](https://kotlinlang.org/docs/reference/reflection.html#property-references):
```kotlin=
if (foo::bar.isInitialized) {
    println(foo.bar)
}
```
This check is only available for the properties that are lexically accessible, i.e. declared in the same type or in one of the outer types, or at top level in the same file.

#### Visibility Modifiers
Kotlin Docs for: [Visibility Modifiers](https://kotlinlang.org/docs/reference/visibility-modifiers.html)

#### Object Expressions and Declarations
Kotlin Docs for: [Object Expressions and Declarations](https://kotlinlang.org/docs/reference/object-declarations.html)

#### \@Jvm Annotations
Kotlin Docs for: [Annotations](https://kotlinlang.org/docs/reference/annotations.html)

The following are Jvm specific annotations to help with Java interoperability
- JvmDefault
    Specifies that a JVM default method should be generated for non-abstract Kotlin interface member.
    - Starting from JDK 1.8, interfaces in Java can contain default methods. You can declare a non-abstract member of a Kotlin interface as default for the Java classes implementing it. To make a member default, mark it with the @JvmDefault annotation. Here is an example of a Kotlin interface with a default method:
    ```kotlin=
    interface Robot {
        @JvmDefault fun move() { println("~walking~") }
        fun speak(): Unit
    }
    ```
    The default implementation is available for Java classes implementing the interface.
    ```java=
    //Java implementation
    public class C3PO implements Robot {
        // move() implementation from Robot is available implicitly
        @Override
        public void speak() {
            System.out.println("I beg your pardon, sir");
        }
    }
    ```
    ```java=
    C3PO c3po = new C3PO();
    c3po.move(); // default implementation from the Robot interface
    c3po.speak();
    ```
    Implementations of the interface can override default methods.
    ```java=
    //Java
    public class BB8 implements Robot {
        //own implementation of the default method
        @Override
        public void move() {
            System.out.println("~rolling~");
        }

        @Override
        public void speak() {
            System.out.println("Beep-beep");
        }
    }
    ```
    For the `@JvmDefault` annotation to take effect, the interface must be compiled with an `-Xjvm-default` argument. Depending on the case of adding the annotation, specify one of the argument values:
    - `-Xjvm-default=enabled` should be used if you add only new methods with the `@JvmDefault` annotation. This includes adding the entire interface for your API.
    - `-Xjvm-default=compatibility` should be used if you are adding a `@JvmDefault` to the methods that were available in the API before. This mode helps avoid compatibility breaks: all the interface implementations written for the previous versions will be fully compatible with the new version. However, the compatibility mode may add some overhead to the resulting bytecode size and affect the performance.

:::info
Note that if an interface with `@JvmDefault` methods is used as a delegate, the default method implementations are called even if the actual delegate type provides its own implementations.
```kotlin=
interface Producer {
    @JvmDefault fun produce() {
        println("interface method")
    }
}

class ProducerImpl: Producer {
    override fun produce() {
        println("class method")
    }
}

class DelegatedProducer(val p: Producer): Producer by p {}

fun main() {
    val prod = ProducerImpl()
    DelegatedProducer(prod).produce() // prints "interface method"
}
```
:::

- JvmField
    Instructs the Kotlin compiler not to generate getters/setters for this property and expose it as a field.
    - If you need to expose a Kotlin property as a field in Java, annotate it with the \@JvmField annotation. The field will have the same visibility as the underlying property. You can annotate a property with `@JvmField` if it has a backing field, is not private, does not have `open`, `override` or `const` modifiers, and is not a delegated property.
    ```kotlin=
    class User(id: String) {
        @JvmField val ID = id
    }
    ```
    ```java=
    // Java
    class JavaClient {
        public String getID(User user) {
            return user.ID;
        }
    }
    ```

- JvmMultifileClass
    Instructs the Kotlin compiler to generate a multifile class with top-level functions and properties declared in this file as one of its parts. Name of the corresponding multifile class is provided by the JvmName annotation.

- JvmName
    Specifies the name for the Java class or method which is generated from this element.
    - Handling Signature clashes with \@JvmName
        - Sometimes we have a named function in Kotlin, for which we need a different JVM name in the byte code. The most prominent example happens due to type erasure:
        ```kotlin=
        fun List<String>.filterValid(): List<String>
        fun List<Int>.filterValid(): List<Int>
        ```
        These two functions can not be defined side-by-side, because their JVM signatures are the same: `filterValid(Ljava/util/List;)Ljava/util/List;`. If we really want them to have the same name in Kotlin, we can annotate one (or both) of them with @JvmName and specify a different name as an argument:
        ```kotlin=
        fun List<String>.filterValid(): List<String>
        
        @JvmName("filterValidInt")
        fun List<Int>.filterValid(): List<Int>
        ```
        From Kotlin they will be accessible by the same name `filterValid`, but from Java it will be `filterValid` and `filterValidInt`.
        The same trick applies when we need to have a property `x` alongside with a function `getX()`:
        ```kotlin=
        val x: Int
            @JvmName("getX_prop")
            get() = 15

        fun getX() = 10
        ```
        To change the names of generated accessor methods for properties without explicitly implemented getters and setters, you can use `@get:JvmName` and `@set:JvmName`:
        ```kotlin=
        @get:JvmName("x")
        @set:JvmName("changeX")
        var x: Int = 23
        ```

- JvmOverloads
    Instructs the Kotlin compiler to generate overloads for this function that substitute default parameter values.
    - If a method has N parameters and M of which have default values, M overloads are generated: the first one takes N-1 parameters (all but the last one that takes a default value), the second takes N-2 parameters, and so on.
    - Normally, if you write a Kotlin function with default parameter values, it will be visible in Java only as a full signature, with all parameters present. If you wish to expose multiple overloads to Java callers, you can use the @JvmOverloads annotation.
    The annotation also works for constructors, static methods, and so on. It can't be used on abstract methods, including methods defined in interfaces.
    ```kotlin=
    class Circle @JvmOverloads constructor(centerX: Int, centerY: Int, radius: Double = 1.0) {
        @JvmOverloads fun draw(label: String, lineWidth: Int = 1, color: String = "red") { /*...*/ }
    }
    ```
    For every parameter with a default value, this will generate one additional overload, which has this parameter and all parameters to the right of it in the parameter list removed. In this example, the following will be generated:
    ```java=
    // Constructors:
    Circle(int centerX, int centerY, double radius)
    Circle(int centerX, int centerY)

    // Methods
    void draw(String label, int lineWidth, String color) { }
    void draw(String label, int lineWidth) { }
    void draw(String label) { }
    ```
    :::info
    Note that, as described in Secondary Constructors, if a class has default values for all constructor parameters, a public no-argument constructor will be generated for it. This works even if the `@JvmOverloads` annotation is not specified.
    :::

- JvmStatic
    Specifies that an additional static method needs to be generated from this element if it's a function. If this element is a property, additional static getter/setter methods should be generated.
    - As mentioned above, Kotlin represents package-level functions as static methods. Kotlin can also generate static methods for functions defined in named objects or companion objects if you annotate those functions as @JvmStatic. If you use this annotation, the compiler will generate both a static method in the enclosing class of the object and an instance method in the object itself. For example:
    ```kotlin=
    class C {
        companion object {
            @JvmStatic fun callStatic() {}
            fun callNonStatic() {}
        }
    }
    ```
    Now, `callStatic()` is static in Java, while `callNonStatic()` is not:
    ```kotlin=
    C.callStatic(); // works fine
    C.callNonStatic(); // error: not a static method
    C.Companion.callStatic(); // instance method remains
    C.Companion.callNonStatic(); // the only way it works
    ```
    Same for named objects:
    ```kotlin=
    object Obj {
        @JvmStatic fun callStatic() {}
        fun callNonStatic() {}
    }
    ```
    In Java:
    ```java=
    Obj.callStatic(); // works fine
    Obj.callNonStatic(); // error
    Obj.INSTANCE.callNonStatic(); // works, a call through the singleton instance
    Obj.INSTANCE.callStatic(); // works too
    ```
    Starting from Kotlin 1.3, `@JvmStatic` applies to functions defined in companion objects of interfaces as well. Such functions compile to static methods in interfaces. Note that static method in interfaces were introduced in Java 1.8, so be sure to use the corresponding targets.
    ```kotlin=
    interface ChatBot {
        companion object {
            @JvmStatic fun greet(username: String) {
                println("Hello, $username")
            }
        }
    }
    ```
    `@JvmStatic` annotation can also be applied on a property of an object or a companion object making its getter and setter methods static members in that object or the class containing the companion object.

- JvmSuppressWildcards
    Instructs compiler to generate or omit wildcards for type arguments corresponding to parameters with declaration-site variance, for example such as `Collection<out T>` has.
    - If the innermost applied @JvmSuppressWildcards has suppress=true, the type is generated without wildcards. If the innermost applied @JvmSuppressWildcards has suppress=false, the type is generated with wildcards.
    It may be helpful only if declaration seems to be inconvenient to use from Java.

- JvmSynthetic
    Sets `ACC_SYNTHETIC` flag on the annotated target in the Java bytecode.
    - Synthetic targets become inaccessible for Java sources at compile time while still being accessible for Kotlin sources. Marking target as synthetic is a binary compatible change, already compiled Java code will be able to access such target.
    This annotation is intended for rare cases when API designer needs to hide Kotlin-specific target from Java API while keeping it a part of Kotlin API so the resulting API is idiomatic for both languages.

- JvmWildcard
    Instructs compiler to generate wildcard for annotated type arguments corresponding to parameters with declaration-site variance.
    - It may be helpful only if declaration seems to be inconvenient to use from Java without wildcard.

- PurelyImplements
    Instructs the Kotlin compiler to treat annotated Java class as pure implementation of given Kotlin interface. "Pure" means here that each type parameter of class becomes non-platform type argument of that interface.
    - Example:
    ```java=
    class MyList<T> extends AbstractList<T> { ... }
    ```
    Methods defined in `MyList<T>` use `T` as platform, i.e. it's possible to perform unsafe operation in Kotlin:
    ```kotlin=
    MyList<Int>().add(null) // compiles
    ```
    ```java=
    @PurelyImplements("kotlin.collections.MutableList")
    class MyPureList<T> extends AbstractList<T> { ... }
    ```
    Methods defined in `MyPureList<T>` overriding methods in `MutableList` use `T` as non-platform types:
    ```kotlin=
    MyPureList<Int>().add(null) // Error
    MyPureList<Int?>().add(null) // Ok
    ```

- Strictfp
    Marks the JVM method generated from the annotated function as `strictfp`, meaning that the precision of floating point operations performed inside the method needs to be restricted in order to achieve better portability.

- Synchronized
    Marks the JVM method generated from the annotated function as `synchronized`, meaning that the method will be protected from concurrent execution by multiple threads by the monitor of the instance (or, for static methods, the class) on which the method is defined.

- Throws
    This annotation indicates what exceptions should be declared by a function when compiled to a JVM method.
    - Example:
    ```kotlin=
    @Throws(IOException::class)
    fun readFile(name: String): String {...}
    ```
    will be translated to
    ```java=
    String readFile(String name) throws IOException {...}
    ```

- Transient
    Marks the JVM backing field of the annotated property as `transient`, meaning that it is not part of the default serialized form of the object.

- Volatile
    Marks the JVM backing field of the annotated property as `volatile`, meaning that writes to this field are immediately made visible to other threads.
    
#### Generics
Kotlin Docs for: [Generics](https://kotlinlang.org/docs/reference/generics.html)

#### Nested Classes
Kotlin Docs for: [Nested Classes](https://kotlinlang.org/docs/reference/nested-classes.html)

#### Enum Classes
Kotlin Docs for: [Enum Classes](https://kotlinlang.org/docs/reference/enum-classes.html)

#### Data Classes (Java 14+ Record Class)
Kotlin Docs for: [Data Classes](https://kotlinlang.org/docs/reference/data-classes.html)

#### Operator Overloading
Kotlin Docs for: [Operator Overloading](https://kotlinlang.org/docs/reference/operator-overloading.html)

#### Extension Functions
Kotlin Docs for: [Extensions](https://kotlinlang.org/docs/reference/extensions.html)

#### Type Aliases
Kotlin Docs for: [Type Aliases](https://kotlinlang.org/docs/reference/type-aliases.html)

### Java Interop
Kotlin Docs for:
- [Calling Java from Kotlin](https://kotlinlang.org/docs/reference/java-interop.html)
- [Calling Kotlin from Java](https://kotlinlang.org/docs/reference/java-to-kotlin-interop.html)

### Functional Programming, but it is better
Kotlin Docs for: [Functional Programming, Migrating from Python](https://kotlinlang.org/docs/tutorials/kotlin-for-py/functional-programming.html)

#### Lambdas
Kotlin Docs for: [Lambdas](https://kotlinlang.org/docs/reference/lambdas.html)

#### Inline functions and Inline Classes
Kotlin Docs for: 
- [Inline Functions](https://kotlinlang.org/docs/reference/inline-functions.html)
- [Inline Classes](https://kotlinlang.org/docs/reference/inline-classes.html)

#### Nice Utility Functions
Kotlin Docs for: [Nice Utility Functions](https://kotlinlang.org/docs/tutorials/kotlin-for-py/functional-programming.html#nice-utility-functions) from [Functional Programming, Migrating from Python](https://kotlinlang.org/docs/tutorials/kotlin-for-py/functional-programming.html)

### More Language Constructs
#### Destructuring Declarations
Kotlin Docs for: [Destructuring Declarations](https://kotlinlang.org/docs/reference/multi-declarations.html)

#### Type Checks and Casting
Kotlin Docs for: [Type Checks and Casting](https://kotlinlang.org/docs/reference/typecasts.html)

#### This Expression (But Smarter)
Kotlin Docs for: [This Expressions](https://kotlinlang.org/docs/reference/this-expressions.html)

#### Equality
Kotlin Docs for: [Equality](https://kotlinlang.org/docs/reference/this-expressions.html)

#### Exceptions
Kotlin Docs for: [Exceptions](https://kotlinlang.org/docs/reference/exceptions.html)

#### Scoped Functions
Kotlin Docs for: [Scoped Functions](https://kotlinlang.org/docs/reference/scope-functions.html)

#### Type-Safe Builders
Kotlin Docs for: [Type-Safe Builders](https://kotlinlang.org/docs/reference/type-safe-builders.html)

### Concurrency
#### Coroutines (The Kotlin Approach)
##### What are Coroutines
Kotlin Docs for: [Basics of Coroutines](https://kotlinlang.org/docs/reference/coroutines/basics.html)

##### Cancellations and Timeouts
Kotlin Docs for: [Cancellations and Timeouts](https://kotlinlang.org/docs/reference/coroutines/cancellation-and-timeouts.html)

##### Suspending Functions
Kotlin Docs for: [Suspending Functions](https://kotlinlang.org/docs/reference/coroutines/composing-suspending-functions.html)

##### Coroutine Context and Dispatchers
Kotlin Docs for: [Coroutine Context and Dispatchers](https://kotlinlang.org/docs/reference/coroutines/coroutine-context-and-dispatchers.html)

##### Flow, Channels and Pipelines
Kotlin Docs for:
- [Asynchronous Flow](https://kotlinlang.org/docs/reference/coroutines/flow.html)
- [Channels](https://kotlinlang.org/docs/reference/coroutines/channels.html)

##### Exception Handling
Kotlin Docs for: [Exception Handling](https://kotlinlang.org/docs/reference/coroutines/exception-handling.html)

##### Shared Mutable State and Concurrency
Kotlin Docs for: [Shared Mutable State and Concurrency](https://kotlinlang.org/docs/reference/coroutines/shared-mutable-state-and-concurrency.html)

##### Threads VS Coroutines
As Kotlin is able to target the JVM and has very stable Java interop, Threads are still able to be used. Meaning now there are two different forms of Concurrency available.

Now the question becomes which do you use? Well, it depends on the situation, each have their own pros and cons. Threads are preemptively multitasked and provide concurrency and along with parallelism. Coroutines, on the ohter hand, are cooperatively multitasked and provide concurrency but do not provide parallelism. This means that coroutines have no need for support from the underlying OS. All in all, threads have their uses and so do coroutines and its important to understand which is better for which situation.

