./[curric](/curric)/[kotlin](/curric/kotlin)/[basics](/curric/kotlin/basics)/[Strings](/curric/kotlin/basics/str)/
# Strings
Strings are represented by the type String. Strings are immutable. Elements of a string are characters that can be accessed by the indexing operation: `s[i]`. A string can be iterated over with a for-loop:
```kotlin
for (c in str) {
    println(c)
}
```
> __All Kotlin for loops act like Java for-each loops, through the use of iterators.__

You can concatenate strings using the `+` operator. This also works for concatenating strings with values of other types, as long as the first element in the expression is a string:
```kotlin
val s = "abc" + 1
println(s + "def")
```
> __Note that in most cases using string templates or raw strings is preferable to string concatenation.__

## String Literals
Kotlin has two types of string literals: escaped strings that may have escaped characters in them and raw strings that can contain newlines and arbitrary text. Here's an example of an escaped string:
```kotlin
val s = "Hello, world!\n"
```
Escaping is done in the conventional way, with a backslash. See Characters above for the list of supported escape sequences.

A raw string is delimited by a triple quote ("""), contains no escaping and can contain newlines and any other characters:
```kotlin
val text = """
    for (c in "foo")
        print(c)
"""
```
You can remove leading whitespace with `trimMargin()` function:
```kotlin
val text = """
    |Tell me and I forget.
    |Teach me and I remember.
    |Involve me and I learn.
    |(Benjamin Franklin)
    """.trimMargin()
```
By default | is used as margin prefix, but you can choose another character and pass it as a parameter, like `trimMargin(">")`.
## String Templates
String literals may contain template expressions, i.e. pieces of code that are evaluated and whose results are concatenated into the string. A template expression starts with a dollar sign ($) and consists of either a simple name:
```kotlin
val i = 10
println("i = $i") // prints "i = 10"
```
or an arbitrary expression in curly braces:
```kotlin
val s = "abc"
println("$s.length is ${s.length}") // prints "abc.length is 3"
```
Templates are supported both inside raw strings and inside escaped strings. If you need to represent a literal $ character in a raw string (which doesn't support backslash escaping), you can use the following syntax:
```kotlin
val price = """
${'$'}9.99
"""
```