./[curric](/curric)/[Functional-Programming](/curric/func)/[Java-Streams](/curric/func/streams)/
# Java Streams ( the functional API for Java Collections )
Java Streams is an API that applies a specific action (filter, map, or reduce) over the entire collection. After applying the specific action, a new modified collection is returned, allowing for method chaining (do operators one after another)
  ```java
  // Example of Chaining
  originalCollection.firstMethod().secondMethod().finalMethod()
  
  // syntax guidelines state to put a newline 
  // before every new method call for readability 
  originalCollection
      .firstMethod()
      .secondMethod()
      .finalMethod()
  ```
Types of Streams
- `Stream<T>`
    - Generic Stream of type T where T extends Object

- `IntStream`
    - Stream of type int wrapped in Integer object, and also adding specific syntactic sugar methods such as sum, average, and count

- `LongStream`
    - Stream of type long wrapped in Long object, and also adding specific syntactic sugar methods such as sum, average, and count

- `DoubleStream`
    - Stream of type double wrapped in Double object, and also adding specific syntactic sugar methods such as sum, average, and count

- Essential Stream Functions
    - `map`
        - Returns a stream consisting of the results of applying the given function to the elements of this stream.
        - `mapToInt`
            - applies map and specifically returns IntStream
        - `mapToDouble`
            - applies map and specifically return DoubleStream
        - `mapToLong`
            - applies map and specifically return LongStream
    - `filter`
        - Returns a stream consisting of the elements of this stream that match the given predicate.
    - `forEach`
        - Performs an action for each element of this stream.
    - `reduce`
        - Performs a reduction on the elements of this stream, using an associative accumulation function, and returns an Optional describing the reduced value, if any.
    - `collect`
        - Performs a mutable reduction operation on the elements of this stream using a Collector.