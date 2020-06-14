./[curric](/curric)/[basics](/curric/basics)/[Functions](/curric/basics/function)/
# Functions
Often, a certain routine of code will have to be used several times, but not in a way easily controlled by a loop. Take, for instance, the following program, which takes a few sets of three numbers and prints out whether they are a Pythagorean triplet:
```java
public class RepetitiveCode {
    public static void main(String args[]) {
        if(3 * 3 + 4 * 4 == 5 * 5) {
            System.out.println("3-4-5");
        }
        if(8 * 8 + 6 * 6 == 9 * 9) {
            System.out.println("6-8-9");
        }
        if(8 * 8 + 6 * 6 == 10 * 10) {
            System.out.println("6-8-10");
        }
        if(3 * 3 + 10 * 10 == 8 * 8) {
            System.out.println("3-10-8");
        }
        if(10 * 10 + 4 * 4 == 5 * 5) {
            System.out.println("10-4-5");
        }
    }
}
```
```java
public class BetterCode {
    public static void main(String args[]) {
        printTriplet(3, 4, 5);
        printTriplet(8, 6, 9);
        printTriplet(8, 6, 10);
        printTriplet(3, 10, 8);
        printTriplet(10, 4, 5);
    }
    public static void printTriplet(int a, int b, int c) {
        if(a * a + b * b == c * c) {
            System.out.println(a + "-" + b + "-" + c);
        }
    }
}
```
`printTriplet` is the name used to call the function.
`(int a, int b, int c)` are arguments, values that are passed into the function to alter its execution. If this syntax looks familiar, it's because `System.out.print()` is a function call, and `main` is a function. Thesse two are special in that `System.out.print()` is provided by the Java runtime, and you are required to provide `main` as an entry point. 
As the name and arguments consitute a function call, they are the "fingerprint" of a function; two functions within the same class can share one, but not both of these values.
Since two functions can have the same name and different arguments, often functions will be written that mirror other functions but with different arguments, usually using default values in place of the otherwise provided values. 
