./[curric](/curric)/[Functional-Programming](/curric/func)/[Functional-Interface](/curric/func/funint)/
# Functional Interfaces
Thanks to Java 8 ( which is the version of Java you will be using ), functional interfaces were introduced, which replaced the need for anonymouse classes.

A functional interface is an interface that contains only one abstract method. They can have only one functionality to exhibit. From Java 8 onwards, lambda expressions can be used to represent the instance of a functional interface. A functional interface can have any number of default methods.
  To use Functional Interfaces, put the @FunctionalInterface annotation above the interface and make sure that the interface only has one abstract method
  For example
  ```java
  @FunctionalInterface
  interface Calculator {
      int calculate(int x, int y);
  }
  ```
  this is now a functional interface that can be called with lambda syntax.

# Lambdas ( The better Anonymous class )
Lambda expressions basically express instances of functional interfaces. Lambda expressions implement the only abstract function and therefore implement functional interfaces
  Lets say, for example if we had the functional interface:
  ```java
  @FunctionalInterface
  interface Calculator {
      int calculate(int x, int y);
  }
  ```
  we could use lambdas to express instances of Calculator
  ```java
  class Main {
      public static void main(String[] args) {
          int a = 5;
          int b = 6;
          
          Calculator add = (int x, int y) -> x + y;
          
          int result = add.calculate(a, b); // 11
      }
  }
  ```
  In this example, we are using a lambda expression to define the calculate method from the interface calculator. In this case, we said that the calculate function would do addition of the two int parameters passed in.
  
The java.util.function package in Java 8 contains many builtin functional interfaces like
- Predicate: The Predicate interface has an abstract method test which gives a Boolean value as a result for the specified argument. Its prototype is
  ```java
  public interface Predicate<T>{
      public boolean test(T t);
  }
  ```
- BinaryOperator: The BinaryOperator interface has an abstract method apply which takes two argument and returns a result of same type. Its prototype is
  ```java
  public interface BinaryOperator<T> {
      public T apply(T x, T y);
  }
  ```
- Function: The Function interface has an abstract method apply which takes argument of type T and returns a result of type R. Its prototype is
  ```java
  public interface Function<T, R> {
      public R apply(T t);
  }
  ```
# Method References ( The less anonymous lambdas )
You use lambda expressions to create anonymous methods. Sometimes, however, a lambda expression does nothing but call an existing method. In those cases, it's often clearer to refer to the existing method by name. Method references enable you to do this; they are compact, easy-to-read lambda expressions for methods that already have a name.
  For example, using the Arrays.sort method
  using Lambda and compareTo
  ```java
  String[] arr = new String[] { "a", "b", "c", "d"};
  
  Arrays.sort(arr,
      (a, b) -> a.compareTo(b)
  );
  ```
  however, the lambda is really only just calling the String.compareTo(String other) method, so we can just use a method reference instead, since the method called by the lambda already exists.
  ```java
  String[] arr = new String[] { "a", "b", "c", "d"};
  
  Arrays.sort(arr, String::compareTo);
  ```