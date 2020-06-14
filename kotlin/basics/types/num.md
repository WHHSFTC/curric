./[curric](/curric)/[kotlin](/curric/kotlin)/[basics](/curric/kotlin/basics)/[Numbers](/curric/kotlin/basics/num)/
# Numbers
In Kotlin, everything is an object in the sense that we can call member functions and properties on any variable. Some of the types can have a special internal representation - for example, numbers, characters and booleans can be represented as primitive values at runtime - but to the user they look like ordinary classes. In this section we describe the basic types used in Kotlin: numbers, characters, booleans, arrays, and strings.
- Byte, Short, Int, Long
    - All variables initialized with integer values not exceeding the maximum value of Int have the inferred type Int. If the initial value exceeds this value, then the type is Long. To specify the Long value explicitly, append the suffix L to the value.

    | Type | Size (bits) | Min value | Max value |
    |------|-------------|-----------|-----------|
    | Byte |8            |-128       |127        |
    | Short|16           |-32768     |32767      |
    |Int   |32           |-2,147,483,648 (-2^31)|	2,147,483,647 (2^31 - 1)|
    |Long  |64           |-9,223,372,036,854,775,808 (-2^63)|9,223,372,036,854,775,807 (2^63 - 1)|
    ```kotlin
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
    ```kotlin
    val pi = 3.14 // Double
    val e = 2.7182818284 // Double
    val eFloat = 2.7182818284f // Float, actual value is 2.7182817
    ```
    - Note that unlike some other languages (Java in particular), there are no implicit widening conversions for numbers in Kotlin. For example, a function with a Double parameter can be called only on Double values, but not Float, Int, or other numeric values.
    ```kotlin
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

## Explicit Conversion
Due to different representations, smaller types are not subtypes of bigger ones. If they were, we would have troubles of the following sort:
```kotlin
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
```kotlin
val b: Byte = 1 // OK, literals are checked statically
val i: Int = b // ERROR
```
We can use explicit conversions to widen numbers
```kotlin
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
```kotlin
val l = 1L + 3 // Long + Int => Long
```
- Operations
    Kotlin supports the standard set of arithmetical operations over numbers (`+` `-` `*` `/` `%`), which are declared as members of appropriate classes (but the compiler optimizes the calls down to the corresponding instructions)
    
#### Division of Integers
- Note that division between integers always returns an integer. Any fractional part is discarded. For example:
    ```kotlin
    val x = 5 / 2 // returns 2 and not 2.5 due to decimal point cutoff
    // println(x == 2.5) // ERROR
    // Operator '==' cannot be applied to 'Int' and 'Double'
    println(x == 2)
    ```
    This is true for a division between any two integer types.
    ```kotlin
    val x = 5L / 2
    println(x == 2L)
    ```
    To return a floating-point type, explicitly convert one of the arguments to a floating-point type.
    ```kotlin
    val x = 5 / 2.toDouble() // equivalent to 5 / 2.0
    println(x == 2.5)
    ```
## Bitwise Operations
As for bitwise operations, there're no special characters for them, but just named functions that can be called in infix form, for example:
```kotlin
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
## Floating point numbers comparison
The operations on floating point numbers discussed in this section are:

Equality checks: `a == b` and `a != b`
Comparison operators: `a < b`, `a > b`, `a <= b`, `a >= b`
Range instantiation and range checks: `a..b`, `x in a..b`, `x !in a..b`

> `a..b` is a Range type, this will be covered later

When the operands `a` and `b` are statically known to be `Float` or `Double` or their nullable counterparts (the type is declared or inferred or is a result of a smart cast), the operations on the numbers and the range that they form follow the IEEE 754 Standard for Floating-Point Arithmetic.

However, to support generic use cases and provide total ordering, when the operands are not statically typed as floating point numbers (e.g. `Any`, `Comparable<...>`, a type parameter), the operations use the `equals` and `compareTo` implementations for `Float` and `Double`, which disagree with the standard, so that:

- `NaN` is considered equal to itself
- `NaN` is considered greater than any other element including POSITIVE_INFINITY
- `-0.0` is considered less than 0.0