./[curric](/curric)/[basics](/curric/basics)/[Loops](/curric/basics/loop)/
# Loops
- `for`
    - The `for` statement provides a compact way to iterate over a range of values
    ```
    for (initialization; termination; increment) {
        statement(s) 
    }
    ```
    - The initialization expression initializes the loop; it's executed once, as the loop begins.
    - When the termination expression evaluates to false, the loop terminates.
    - The increment expression is invoked after each iteration through the loop; it is perfectly acceptable for this expression to increment or decrement a value.
    ```java
    for (int i = 0; i < 11; i++) {
        System.out.println(i); // prints every i used in the loop
    }
    ```
    Output
    ```
    0
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    ```
- `while`
    - The while statement continually executes a block of statements while a particular condition is true.
    ```
    while (expression) {
        statement(s)
    }
    ```
    - Unlike `for` loops, in `while` loops you have the initialization, termination, and increment all done separately.
    ```java
    int i = 0;
    while (i < 11) {
        System.out.println(i); // prints every i used in the loop
        i++;
    }
    ```
    Output (same as `for`)
    ```
    0
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    ```
- Enhanced `for` and Iterators
    - Enhanced `for` loops or more commonly know as for each loops, use the individual values in the collection instead of the index.
    For example:
    ```java
    int[] arr = new int[] {1, 2, 3, 4, 5}; // array creation shorthand
    
    // using for loop to print every element
    for (int i = 0; i < arr.length; i++) {
        System.out.print(arr[i]);
    }
    // 12345
    
    // using for each to print every element
    for (int i : arr) {
        System.out.print(i);
    }
    // 12345
    ```
    Both outputs are the same.
    But they don't act the same way. In the `for` loop, we are using an index to get every element. However in the `for` each loop, the element gets copied into the the variable i. `for` each loops are used in situations where you don't need the index of an element, while `for` loops are when the index of the element plays an important role.