./[curric](/curric)/[kotlin](/curric/kotlin)/[oop](/curric/kotlin/oop)/[jvm-annotations](/curric/kotlin/oop/jvmanno)/
# \@JVM Annotations
The following are Jvm specific annotations to help with Java interoperability
- JvmDefault
    Specifies that a JVM default method should be generated for non-abstract Kotlin interface member.
    - Starting from JDK 1.8, interfaces in Java can contain default methods. You can declare a non-abstract member of a Kotlin interface as default for the Java classes implementing it. To make a member default, mark it with the @JvmDefault annotation. Here is an example of a Kotlin interface with a default method:
    ```kotlin
    interface Robot {
        @JvmDefault fun move() { println("~walking~") }
        fun speak(): Unit
    }
    ```
    The default implementation is available for Java classes implementing the interface.
    ```java
    //Java implementation
    public class C3PO implements Robot {
        // move() implementation from Robot is available implicitly
        @Override
        public void speak() {
            System.out.println("I beg your pardon, sir");
        }
    }
    ```
    ```java
    C3PO c3po = new C3PO();
    c3po.move(); // default implementation from the Robot interface
    c3po.speak();
    ```
    Implementations of the interface can override default methods.
    ```java
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

> Note that if an interface with `@JvmDefault` methods is used as a delegate, the default method implementations are called even if the actual delegate type provides its own implementations.
```kotlin
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

- JvmField
    Instructs the Kotlin compiler not to generate getters/setters for this property and expose it as a field.
    - If you need to expose a Kotlin property as a field in Java, annotate it with the \@JvmField annotation. The field will have the same visibility as the underlying property. You can annotate a property with `@JvmField` if it has a backing field, is not private, does not have `open`, `override` or `const` modifiers, and is not a delegated property.
    ```kotlin
    class User(id: String) {
        @JvmField val ID = id
    }
    ```
    ```java
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
        ```kotlin
        fun List<String>.filterValid(): List<String>
        fun List<Int>.filterValid(): List<Int>
        ```
        These two functions can not be defined side-by-side, because their JVM signatures are the same: `filterValid(Ljava/util/List;)Ljava/util/List;`. If we really want them to have the same name in Kotlin, we can annotate one (or both) of them with @JvmName and specify a different name as an argument:
        ```kotlin
        fun List<String>.filterValid(): List<String>
        
        @JvmName("filterValidInt")
        fun List<Int>.filterValid(): List<Int>
        ```
        From Kotlin they will be accessible by the same name `filterValid`, but from Java it will be `filterValid` and `filterValidInt`.
        The same trick applies when we need to have a property `x` alongside with a function `getX()`:
        ```kotlin
        val x: Int
            @JvmName("getX_prop")
            get() = 15

        fun getX() = 10
        ```
        To change the names of generated accessor methods for properties without explicitly implemented getters and setters, you can use `@get:JvmName` and `@set:JvmName`:
        ```kotlin
        @get:JvmName("x")
        @set:JvmName("changeX")
        var x: Int = 23
        ```

- JvmOverloads
    Instructs the Kotlin compiler to generate overloads for this function that substitute default parameter values.
    - If a method has N parameters and M of which have default values, M overloads are generated: the first one takes N-1 parameters (all but the last one that takes a default value), the second takes N-2 parameters, and so on.
    - Normally, if you write a Kotlin function with default parameter values, it will be visible in Java only as a full signature, with all parameters present. If you wish to expose multiple overloads to Java callers, you can use the @JvmOverloads annotation.
    The annotation also works for constructors, static methods, and so on. It can't be used on abstract methods, including methods defined in interfaces.
    ```kotlin
    class Circle @JvmOverloads constructor(centerX: Int, centerY: Int, radius: Double = 1.0) {
        @JvmOverloads fun draw(label: String, lineWidth: Int = 1, color: String = "red") { /*...*/ }
    }
    ```
    For every parameter with a default value, this will generate one additional overload, which has this parameter and all parameters to the right of it in the parameter list removed. In this example, the following will be generated:
    ```java
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
    ```kotlin
    class C {
        companion object {
            @JvmStatic fun callStatic() {}
            fun callNonStatic() {}
        }
    }
    ```
    Now, `callStatic()` is static in Java, while `callNonStatic()` is not:
    ```kotlin
    C.callStatic(); // works fine
    C.callNonStatic(); // error: not a static method
    C.Companion.callStatic(); // instance method remains
    C.Companion.callNonStatic(); // the only way it works
    ```
    Same for named objects:
    ```kotlin
    object Obj {
        @JvmStatic fun callStatic() {}
        fun callNonStatic() {}
    }
    ```
    In Java:
    ```java
    Obj.callStatic(); // works fine
    Obj.callNonStatic(); // error
    Obj.INSTANCE.callNonStatic(); // works, a call through the singleton instance
    Obj.INSTANCE.callStatic(); // works too
    ```
    Starting from Kotlin 1.3, `@JvmStatic` applies to functions defined in companion objects of interfaces as well. Such functions compile to static methods in interfaces. Note that static method in interfaces were introduced in Java 1.8, so be sure to use the corresponding targets.
    ```kotlin
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
    ```java
    class MyList<T> extends AbstractList<T> { ... }
    ```
    Methods defined in `MyList<T>` use `T` as platform, i.e. it's possible to perform unsafe operation in Kotlin:
    ```kotlin
    MyList<Int>().add(null) // compiles
    ```
    ```java
    @PurelyImplements("kotlin.collections.MutableList")
    class MyPureList<T> extends AbstractList<T> { ... }
    ```
    Methods defined in `MyPureList<T>` overriding methods in `MutableList` use `T` as non-platform types:
    ```kotlin
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
    ```kotlin
    @Throws(IOException::class)
    fun readFile(name: String): String {...}
    ```
    will be translated to
    ```java
    String readFile(String name) throws IOException {...}
    ```

- Transient
    Marks the JVM backing field of the annotated property as `transient`, meaning that it is not part of the default serialized form of the object.

- Volatile
    Marks the JVM backing field of the annotated property as `volatile`, meaning that writes to this field are immediately made visible to other threads.