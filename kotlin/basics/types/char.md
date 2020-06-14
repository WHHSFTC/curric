./[curric](/curric)/[kotlin](/curric/kotlin)/[basics](/curric/kotlin/basics)/[Characters](/curric/kotlin/basics/char)/
# Character
Characters are represented by the type Char. They can not be treated directly as numbers
```kotlin
fun check(c: Char) {
    if (c == 1) { // ERROR: incompatible types
        // ...
    }
}
```
Character literals go in single quotes: `'1'`. Special characters can be escaped using a backslash. The following escape sequences are supported: `\t`, `\b`, `\n`, `\r`, `\'`, `\"`, `\\` and `\$`. To encode any other character, use the Unicode escape sequence syntax: `'\uFF00'`.

We can explicitly convert a character to an `Int` number:
```kotlin
fun decimalDigitValue(c: Char): Int {
    if (c !in '0'..'9') 
    // checks if the character is
    // between 0 and 9 on the ascii table
        throw IllegalArgumentException("Out of range")
    return c.toInt() - '0'.toInt() // Explicit conversions to numbers
}
```
> __ASCII is the numeric representation of characters that the computer sees__

Like numbers, characters are boxed when a nullable reference is needed. Identity is not preserved by the boxing operation.