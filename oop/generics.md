./[curric](/curric)/[oop](/curric/oop)/[generics](/curric/oop/generics)
# Generics
Generics are a facility of generic programming that were added to the Java programming language in 2004 within version J2SE 5.0. They were designed to extend Java's type system to allow "a type or method to operate on objects of various types while providing compile-time type safety".

```java
public class Box<T> {
    // T stands for Type
    private T boxed;

    public Box(T box) {
        this.boxed = box;
    }

    public void set(T newValue) {
        this.boxed = newValue;
    }

    public T get() {
        return boxed;
    }
}
```
In the code above, we are "boxing" a value into a `Box<T>` class. The `<T>` signifies that there is a generic type parameter in use and that allows for us, the developer, to put in a certain type and that is the type `T` will represent
For example:
```java
Box<Integer> boxedInt = new Box<Integer>(10);
// we must use Integer, the object wrapper for the primitive int type, in this case as type parameters will only accept an object (aka class)
// the type of the private field boxed is now of type Integer

System.out.println(boxedInt.get()); // 10, using the get method to access the private variable boxed

Box<String> boxedString = new Box<String>("Boxed"); // now we are boxing a string
// the type of the private field boxed is now of type String

System.out.println(boxedString.get()); // Boxed
```

Reference for [Generics](https://docs.oracle.com/javase/tutorial/java/generics/types.html)