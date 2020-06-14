./[curric](/curric)/[basics](/curric/basics)/[Operators](/curric/basics/operators)/
# Operators
## Logical Operations - return a `boolean`



- and: `a & b -> c` / `a && b -> c`
    |a|b|c|
    |-|-|-|
    |`false`|`false`|`false`|
    |`false`|`true`|`false`|
    |`true`|`false`|`false`|
    |`true`|`true`|`true`|
- or: `a | b -> c` / `a || b -> c`
    |a|b|c|
    |-|-|-|
    |`false`|`false`|`false`|
    |`false`|`true`|`true`|
    |`true`|`false`|`true`|
    |`true`|`true`|`true`|
- xor: `a^b -> c`
    |a|b|c|
    |-|-|-|
    |`false`|`false`|`false`|
    |`false`|`true`|`true`|
    |`true`|`false`|`true`|
    |`true`|`true`|`false`|
- not: `!a -> b`
    |a|b|
    |-|-|
    |`false`|`true`|
    |`true`|`false`|
- equality: `a == b` / `a.equals(b)`
  Returns `true` if `a` and `b` are equivalent, or `false` otherwise.
  `==` is used for primitives
  `.equals()` is used for complex types
## Arithmatic Operations
- addition ( `+`, `+=` )
    - Self explanatory addition
    ```java
    // the plus operator
    int a = 10;
    int b = 20;
    int c = a + b; // 30
    
    // the plus assign operator
    int a += b; 
    // this is the same as
    int a = a + b;
    ```
- subtraction ( `-`, `-=` )
    - Self explanatory subtraction
    ```java
    // the minus operator
    int a = 20;
    int b = 10;
    int c = a - b; // 10
    
    // the minus assign operator
    int a -= b;
    // this is the same as
    int a = a - b;
    ```
- multiplication ( `*`, `*=` )
    - Self explanatory multiplication
    ```java
    // the times operator
    int a = 10;
    int b = 10;
    int c = a * b; // 100
    
    // the times assign operator
    int a *= b;
    // this is the same as
    int a = a * b;
    ```
- division ( `/`, `/=` )
    - Self explanatory division
    ```java
    // the division operator
    int a = 20;
    int b = 10;
    int c = a / b; // 2
    
    // the division assign operator
    int a /= b;
    // this is the same as
    int a = a / b;
    ```
- remainder ( %, %= )
    - Here is where things get tricky. The % (remainder) function is a function that returns the remainder of the two inputs. For example:
    ```java
    // the remainder operator
    int a = 20 % 10; // this equals 0, since 20 / 10 has no remainder
    int b = 21 % 2; // this equals 1, since 21 / 2 equals 10 remainder 1
    
    // the remainder assign operator
    int a %= b;
    // this is the same as
    int a = a % b;
    ```
- increment and decrement ( `++`, `--` )
    - the increment and decrement operators are operators that either increment the current value by 1 or decrement it by 1, without having to reassign the value of the variable
    ```java
    int a = 10;
    
    // we could increment this value by 1 by manually adding 1
    a = a + 1; // now 11
    
    // or with the += operator
    a += 1; // now 12
    
    // but the ++ operator allows us to do this as well
    a++; // now 13
    ```
    Same with the `--` (decrement operator)
    ```java
    int b = 10;
    
    // we could decrement this value by 1 by manually subtracting 1
    b = b - 1; // now 9
    
    // or using the -= operator
    b -= 1; // now 8
    
    // but the -- operator allows us to do this as well
    b--; // now 7
    ```
    However, there is a slight difference with the `++` and `--` operators. The difference is prefix vs postfix.
    
    What is prefix and postfix? Prefix is where the operator being applied is before the value its being applied on. Postfix is where the operator being applied is after the value its being applied on.
    
    In incrementing and decrementing, whether you choose to do a prefix ( `++i`, `--i` ) or a postfix ( `i++`, `i--` ) their will be a different outcome. The prefix will change the value then use it, while the postfix will use the old value then update the variable. 
    For example:
    ```java
    int i = 10;
    
    int j = ++i; // j's value is 11 and i's value is 11
    
    int k = i++; // k's value is 11 and i's value is 12
    ```
Note: all of the above examples are with ints. However, when doing arithmatic operations with doubles, they will behave the same as ints but with decimal places.

If you intermix arithmatic operators between doubles and ints, lets say in addition. `2.0 + 1 = 3.0` This is a double plus an integer, therefore Java will say: "Ok, I will cast the integer to a double to abide by addition rules of doubles" 
:::info
Java Rule: If you do any arithmatic operation with a double and some other number (int or double), the output will be double
:::
## String
- Concatenation
    - Simply put, this is "adding" two strings together.
    ```java
    String a = "Hello ";
    String b = "World!";
    String c = a + b; // "Hello World!"
    ```