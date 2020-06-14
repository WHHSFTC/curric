./[curric](/curric)/[kotlin](/curric/kotlin)/[oop](/curric/kotlin/oop)/[open-vs-sealed](/curric/kotlin/oop/openorsealed)/
# Open vs Sealed
- Open\
    All classes in Kotlin have a common superclass `Any`, that is the default superclass for a class with no supertypes declared:
    ```kotlin
    class Example // Implicitly inherits from Any
    ```
    `Any` has three methods: `equals()`, `hashCode()` and `toString()`. Thus, they are defined for all Kotlin classes.
    By default, Kotlin classes are final: they can’t be inherited. To make a class inheritable, mark it with the `open` keyword.
    ```kotlin
    open class Base //Class is open for inheritance
    ```
    To declare an explicit supertype, place the type after a colon in the class header:
    ```kotlin
    open class Base(p: Int)
    
    class Derived(p: Int) : Base(p)
    ```
    If the derived class has a primary constructor, the base class can (and must) be initialized right there, using the parameters of the primary constructor.
    
    If the derived class has no primary constructor, then each secondary constructor has to initialize the base type using the super keyword, or to delegate to another constructor which does that. Note that in this case different secondary constructors can call different constructors of the base type:
    ```kotlin
    class MyView : View {
        constructor(ctx: Context) : super(ctx)

        constructor(ctx: Context, attrs: AttributeSet): super(ctx, attrs)
    }
    ```
- Sealed
    - Kotlin Docs for: [Sealed Classes](https://kotlinlang.org/docs/reference/sealed-classes.html)