./[curric](/curric)/[kotlin](/curric/kotlin)/[basics](/curric/kotlin/basics)/[New-Types](/curric/kotlin/basics/new)/
## New Types
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