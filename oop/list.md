./[curric](/curric)/[oop](/curric/oop)/[Lists](/curric/oop/list)
# List 
## The most common Interface
### Lets take a couple steps back for a second

Another type of data structure most commonly used in Computer Programming is called the List. Lists are different from Arrays, in the fact that Arrays have a set size, while a Lists' size is mutable. Meaning that a Lists' size can change based on the number of elements put into it. However, a List in Java is an interface, the implementation of the List is most commonly used by a type called `ArrayList`

To create an `ArrayList`, you use the `new` keyword, just like any other object. However, you must also include the type parameter, as ArrayLists and Lists utilize generic type parameters.
```java
// import java.util.ArrayList; importing ArrayLists
// to cover all basis we use
import java.util.*; // the * symbol means import everything from the utils package

// To create an list
ArrayList<Integer> list = new ArrayList<Integer>();
// we must you Integer, the object wrapper for ints, as type parameters only allow of objects (aka classes)

// populate the list with every int from 0 to 4
for (int i = 0; i < 5; i++) {
    list.add(i);
}

System.out.println(list); // [0, 1, 2, 3, 4]
```

Essential List Functions
- `add(E e)`
    - Appends the specified element to the end of this list (optional operation)
- `get(int index)`
    - Returns the element at the specified position in this list
- `indexOf(Object o)`
    - Returns the index of the first occurrence of the specified element in this list, or -1 if this list does not contain the element.
- `size()`
    - Returns the number of elements in this list.
- `subList(int fromIndex, int toIndex)`
    - Returns a view of the portion of this list between the specified fromIndex, inclusive, and toIndex, exclusive.

[Reference to Oracle Docs for Lists](https://docs.oracle.com/javase/8/docs/api/java/util/List.html)
[Reference to Oracle Docs for ArrayLists](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html)