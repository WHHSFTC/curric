./[curric](/curric)/[kotlin](/curric/kotlin)/[basics](/curric/kotlin/basics)/[variables](/curric/kotlin/basics/var)/
# Variables
Variables can be declared two different ways. val or var. Depending on if the variable is val or var, the variable will behave differently.

The type of the variable in Kotlin can be either explicitly given or the type can be inferred. To explicitly define the type, place a `:` after the variable name and then the type.
```kotlin
var name: Type
```
## Val vs Var
- Val
    - Defining a variable with the `val` keyword makes the variable read-only.
    
    > _Read-only variables are variables that can only be assigned a value once._
    ```kotlin
    val a: Int = 9 // explicit typing, immediate assignment of value
    val b = 2 // Type 'Int' is inferred
    val c: Int // Type is required when no initializer is provided
    c = 3
    ```
- Var
    - Defining a variable with the `var` keyword allows the variable to be reassigned.
    ```kotlin
    var x = 5 // Type 'Int' is inferred
    x += 1
    ```