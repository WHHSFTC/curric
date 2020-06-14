./[curric](/curric)/[Functional-Programming](/curric/func)/[Anonymous-Class](/curric/func/anon)/
# Anonymous Classes
Anonymous Classes are inner classes without a name and for which only a single object is created. An anonymous inner class can be useful when making an instance of an object with certain “extras” such as overloading methods of a class or interface, without having to actually subclass a class.
  For example:
  If you had a interface Age
  ```java
  interface Age {
      int a = 21;
      int getAge();
  }
  ```
  and you had a class Person that implements the Age interface
  ```java
  class Person implements Age {
      @Override
      public int getAge() {
          return a;
      }
  }
  ```
  and you were creating a new Person object
  ```java
  class Main {
      public static void main(String[] args) {
          Person me = new Person();
          System.out.println(me.getAge());
      }
  }
  ```
  instead of having to create a class that implements the Age interface, you could use an anonymous class instead
  ```java
  class Main {
      public static void main(String[] args) {
          Age me = new Age() {
              @Override
              public int getAge() {
                  return a;
              }
          };
          System.out.println(me.getAge());
      }
  }
  ```
  this will act the same as the example with the Person class, but in this is example, the "Person" class is now an anonymous inner class of Age