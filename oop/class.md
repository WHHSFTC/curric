./[curric](/curric)/[oop](/curric/oop)/[class](/curric/oop/class)
# Classes and Access
In Java, mostly everything you'll deal with are _objects_, meaning that their behavior is defined by a _class_. Generally, objects can have information unique to them, but what they can do is the same between all objects of the same class. For example, imagine a class `Car` (classes are always capitalized). Any `Car` object you have will be able to `goVrooom()` (methods are in camel case, and always followed by parentheses). However, some cars may look different than others; they may have a ifferent `make`, `model`, or `year`. You use the`.` operator to access methods and fields of classes. The following code snippet may illustrate this:
```java
System.out.println(lukesCar.year);   // 87
System.out.println(lukesCar.make);   // "Oldsmobile"
System.out.println(lukesCar.model);  // "Cutlass Sierra"
lukesCar.goVrooom();   // vroooms, albeit louder than most 
                       // as it has no muffler
System.out.println(jaransCar.year);  // 92
System.out.println(jaransCar.make);  // "Jeep"
System.out.println(jaransCar.model); // "Wrangler"
jaransCar.goVrooom();  // *quiet vrooom*
```

Almost all code belongs to some specific class, which is a block as described above. 
```java
class Car {

}
```
What goes in a class, of course, depends on what the class is for. Following the `Car` example from above, this class would have the methods `goVrooom()` and `detachMuffler()` and three fields `year`, `make`, and `model`.
These are the fields and methods that are exposed to code outside the class, so they should be marked `public`, as should the class itself.
```java
public class Car {
    public int year;
    public String make;
    public String model;
    
    public void goVrooom() {
        // make a noise
    }
    
    public void detachMuffler() {
        // it can't be that hard to securely mount a muffler
    }
}
```
Of course, there must be some state stored within the class. How does the car know how loud to vrooom?
People who aren't in the know of `lukesCar` don't have access to the information of whether it has a muffler unless they try to steal it or drive the car. So there has to be a field for this that is not `public` but rather `private`.
```java
public class Car {
    public int year;
    public String make;
    public String model;
    
    private boolean hasMuffler;
    
    public void goVrooom() {
        if (hasMuffler) {
            // make a muffled vrooom
        } else { 
            // make a loud vrooom
        }  
     
    
    public void detachMuffler() {
        hasMuffler = false;
    }
}
```
This idea of using `public` methods to control the values of `private` methods is called _encapsulation_, and it is a very common practice in Object-Oriented Programming.