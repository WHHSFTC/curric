./[curric](/curric)/[basics](/curric/basics)/[Type](/curric/basics/type)/
# Type
- `byte`, `short`, `int`, `long` (integers)

   ```java
   byte b = 1; // bytes are 8 bits long, [-128, 127]
   short s = 10; // shorts are 16 bits long, [-32,768, 32,767]
   int i = 20; // ints are 32 bits long, [-2^31, 2^31)
   long l = 30; // longs are 64 bits long, [-2^63, 2^63)
   // all are of 2's complement
   ```
- `float`, `double` (floating numbers)
   ```java
   float f = 10f; // single-precision 32-bit IEEE 754 floating point 
   double d = 20.0; // double-precision 64-bit IEEE 754 floating point
   ```
- `String`, `char` (Text)
   ```java
   String s = "This is a string";
   char c = 'G'; // this is a character
   // char can only be one letter long and uses single quotes
   ```
- `boolean` (true and false)
   ```java
   boolean tf = true; // booleans designtes true or false
   ```
- array ( `T[] where T is the defining type of the array`)

  ```java
  // creates an int array of size five filled with default values
  // in this case the default value of an int is 0
  int[] arr = new int[5]; 
  ```
  `int[] arr` is `[0, 0, 0, 0, 0]`
  To access a value in an array, an index is required.
  
  > All array indices start at 0 and go up to the length of the array - 1
  
  ```java
  int[] arr = new int[5];
  
  arr[0] = 1;
  arr[1] = 2;
  arr[2] = 3;
  arr[3] = 4;
  arr[4] = 5;

  System.out.println(Arrays.toString(arr)); // prints out the list in readable form, this is imported from java.util.Arrays
  ```
  `int[] arr` is now `[ 1, 2, 3, 4, 5]`
  
  > You can create an array of any type, just use `[]` after the type and it will become an array. i.e. `int[] double[] byte[] String[] char[] boolean[]`
  
reference: 
[Basic Types](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes)
and [Arrays](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/arrays.html) and [Strings](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html)


All of the above types are known as primitives, except `String`. Primitive types begin with a lowercase letter and are the types you'd expect a language to handle intuitively. However, they don't have all the features of complex types like `String` and `ArrayList`, which you'll learn about later. For this reason, Java has a workaround known as auto-encapsulation where it will automatically treat primitives like `int` as complex wrappers like `Integer`, and vice versa, depending on context.