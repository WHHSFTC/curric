./[curric](/curric)/[kotlin](/curric/kotlin)/[basics](/curric/kotlin/basics)/[arrays](/curric/kotlin/basics/arr)/
# Arrays
Arrays in Kotlin are represented by the `Array` class, that has `get` and `set` functions (that turn into `[]` by operator overloading conventions), and `size` property, along with a few other useful member functions:
```kotlin
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
```kotlin
// Creates an Array<String> with values ["0", "1", "4", "9", "16"]
val asc = Array(5) { i -> (i * i).toString() }
// {} after the array constructor is 
// kotlin syntactic sugar for calling lambdas
asc.forEach { println(it) }
// same with the {} after the forEach
```
As we said above, the `[]` operation stands for calls to member functions `get()` and `set()`.

Arrays in Kotlin are invariant. This means that Kotlin does not let us assign an `Array<String>` to an `Array<Any>`, which prevents a possible runtime failure (but you can use `Array<out Any>` which we will get to later in the Generics Section)
## Primitive type arrays
Kotlin also has specialized classes to represent arrays of primitive types without boxing overhead: ByteArray, ShortArray, IntArray and so on. These classes have no inheritance relation to the Array class, but they have the same set of methods and properties. Each of them also has a corresponding factory function:
```kotlin
val x: IntArray = intArrayOf(1, 2, 3)
x[0] = x[1] + x[2]
```
```kotlin
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