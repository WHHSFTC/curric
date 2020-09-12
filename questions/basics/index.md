./[curric](/curric)/[questions](/curric/questions)/[basics](/curric/questions/basics)/

**Test out your knowledge that you have learned!!**

*Try to trace the code. Don't put the code into an IDE and run it.*

Question 1: What does this `main` method output to the console?
```java
public static void main(String[] args) {
    System.out.println("Knowledge Test Time!!");
}
```
- `Hello World!`
- `Knowledge Test Time!!`
- `I am confused`
- No Output

Question 2: What are the types of these variables

    a. true
    b. 10
    c. 13.0
    d. "what type is this?"


Question 3: What does this `main` method output to the console
```java
public static void main(String[] args) {
    int value = 12;
    if (value == 10) {
        System.out.println("Value is exactly 10");
    } else if (value < 10) {
        System.out.println("Value is less than 10");
    } else {
        System.out.println("Value is greater than 10");
    }
}
```
- `Value is exactly 10`
- `Value is less than 10`
- `Value is greater than 10`
- No Output

Question 4: What does this `main` method output to the console
```java
public static void main(String[] args) {
    int a = 10;
    int b = 13;
    double c = 100.0;
    int d = 51;

    double result = ((d + a) * c) + ((a * 3) + (b % 10));

    System.out.println(result);
}
```
- `6000`
- `133`
- `6133`
- `Error, type of int and type of double can not be applied to operation *`

Question 5: What does this `main` method output to the console
```java
public static void main(String[] args) {
    String result = "";

    for (int i = 0; i < 4; i++) {
        result = result + "Hello ";
    }

    System.out.println(result);
}
```
- `Hello Hello Hello Hello `
- `Hello Hello Hello Hello`
- `HelloHelloHelloHello`
- `Hello`

Question 6: What does `mysteryFunction(3)` return
```java
public static int mysteryFunction(int n) {
    int ret = 0;

    for (int i = 0; i < n; i++) {
        ret += 2 * (i + 1);
    }

    return ret;
}
```
- `6`
- `12`
- `24`
- `6133`
