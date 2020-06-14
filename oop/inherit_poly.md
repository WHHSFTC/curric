./[curric](/curric)/[oop](/curric/oop)/[inherit & poly](/curric/oop/inherit_poly)
# Inheritance
Sometimes the objects of a class can be demarcated further into subclasses. For this example, let's include other vehicles. All vehicles can take you somewhere, but not all vehicles can vrooom. Bikes don't vroom; bikes squeak. For the concepts of movement, let's imagine that the classes `Person` and `Place` exist, and that we can move someone by setting their `.location` variable.
```java
public class Vehicle {
    public void move(Person person, Place place) {
        person.location = place;
    }
}
```
```java
Vehicle v = new Vehicle();
Person me = new Person("Luke");
Place manu = new Place("12055 Mosteller Rd, Cincinnati, OH 45241");
v.move(me, manu);
```
Great! Now we can create a `Vehicle` object and use it to move people places. But now we lost the ability to do vehicle-specific things like vroooming and squeeaking. Let's make a Car class and a Bike class then, like before.
```java
public class Car {
    public int year;
    public String make;
    public String model;
    
    private boolean hasMuffler;
    
    public Car(int year, String make, String model) {
        this(year, make, model, true);
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
    }
    
    public void detachMuffler() {
        hasMuffler = false;
    }
}
public class Bike {
    double squeakiness;
    
    public Bike() {
        this(1.0);
    }
    
    public Bike(double squeakiness) {
        this.squeakiness = squeakiness;
    }
    
    public void squeeak() {
        // squeaks depending on the value of squeakiness
    }
}
```
Ok, now we have a vehicle that moves, a car that vrooms and tracks the presence of a muffler, and a bike that squeaks and tracks when it is oiled. But cars and bikes are vehicles, so they should be able to move too. In other words, they should _inherit_ the ability to move. We must define `Car` and `Bike` as subclasses of `Vehicle` using the `extends` keyword:
```java
public class Car extends Vehicle {
    // ...
}
public class Bike extends Vehicle {
    // ...
}
```
Now, a `Car` can do anything defined in `Vehicle` as if it were its own method, or access any instance variables, as long as those fields and methods are marked `public` or `protected`.
```java
Bike b = new Bike();
Person me = new Person("Luke");
Place home = new Place(); // I will not disclose my home address
b.move(me, home);
b.squeeak();
```


# Polymorphism

In fact, not only can a `Car` do anything a `Vehicle` can do, you don't even need to know it's a `Car` to make it do vehicular things. This is an important feature of OOP called _polymorphism_: any object can act as a member of its own class, or of any class its class inherits or implements. 

This means that functions that operate on generic `Vehicle`s work on any `Car`, `Bike`, or other types of `Vehicles` that we haven't yet defined. 

For example, the `.print(Object obj)` method of `PrintStream`s like `System.out` takes any `Object`. In Java, it is a universal truth that all objects inherit `Object`, and supply its few methods. These include `.toString()`, which returns a `String` representation of any `Object`. The `print` method uses this to output objects to the terminal. `Object` comes with a default implementation of `.toString()`, which outputs long, often garbled data about the object, so it is unnecessary but good practice to define your own `toString()` method. Any object, even if not as an `Object` reference, can be passed into this function:
```java
Bike b = new Bike();
System.out.print(b); // outputs a string that can be used to obtain data about the bike
```

Often, when using polymorphism you'll find it necessary to convert a pointer between different classes by casting. A function like `print(obj)` requires an `Object` argument. As you can see, the argument `b` of class `Bike` is automatically converted into an `Object`. This is allowed because every `Bike` is also an `Object`. However, if you only have access to an `Object` variable but you need to access `Bike`-specific methods, you must cast it manually: `Bike b = (Bike) obj`. Just like with primitive variables, manually casting is dangerous; you must be certain that the reference points to a `Bike` object or an object of a subclass of `Bike`. Otherwise, there will be a runtime error. 

A useful aspect of inheritance is that a subclass can override its inherited functions. In order to add more contraints to the `move` function, such as on distance, to the `Bike` class, we can redefine the method in `Bike`.

```java
public class Bike {
    //...
    public void move(Person person, Place place) {
        if (place.distance < 20){
            person.location = place;
        } else {
            System.out.println("Too far!");
        }
    }
    //...
}
```
With this overloaded method, any call to `.move()` on a reference to a `Bike` object will use the new limit. Note: this applies not only to references of the type `Bike`, but also of casted references that are treated as a superclass but still point to `Bike` objects.
