./[curric](/curric)/[oop](/curric/oop)/[constructor](/curric/oop/constructor)
# Constructors
In the previous examples, we dealt with existing objects. However, we never touched on the creation of new objects. `jaransCar` did not magically appear into the world as a '92 Jeep Wrangler. A factory had to _construct_ it first. In Java, classes have a special method caled the _constructor_, invoked by the `new` keyword. A constructor, just like any method, can take arguments, and it can be overloaded. 
```java
public class Car {
    public int year;
    public String make;
    public String model;
    
    private boolean hasMuffler;
    
    // constructor syntax:
    public Car(int year, String make, String model) {
        // we have to use this to avoid ambiguity
        this.year = year;
        this.make = make;
        this.model = model;
        hasMuffler = true;
    }
    
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
Note that `this` always refers to the current object, an intuitive and consistent behavior (@javascript). We use it to distinguish between the `year`, `make`, and `model` provided as arguments and the fields of the class.
This assumes that all cars are created with a muffler. But what if we want to leave the possibility to special order a muffler-less car? We can simply add an overloaded constructor. 
```java
public class Car {
    public int year;
    public String make;
    public String model;
    
    private boolean hasMuffler;
    
    public Car(int year, String make, String model) {
        this.year = year;
        this.make = make;
        this.model = model;
        hasMuffler = true;
    }
    
    public Car(int year, String make, String model, boolean hasMuffler) {
        this.year = year;
        this.make = make;
        this.model = model;
        this.hasMuffler = hasMuffler;
    }
    
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