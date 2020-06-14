./[curric](/curric)/[oop](/curric/oop)/[interfaces & abstract classes](/curric/oop/interfaces-abstract)
# Abstract Classes
Now you've learned about inheritance, subclasses and superclasses. Keeping with the vehicle example, we have a superclass, `Vehicle`, and two subclasses, `Car` and `Bike`. This has no glaring conceptual errors, but there is one practical mistake: you can create an instance of `Vehicle` that is not a `Car` or `Bike`. This might be intentional, to allow more types of vehicles, but it is best practice that any new type of vehicle gets it's own subclass, like `Plane`, as there will inevitably be more things to change about the class beyond the bare minimum functionality in `Vehicle`. 

This is a good use case for an _abstract_ class. An abstract class behaves just like any other class; it can have instance members, static members, subclasses, superclasses, etc; except it is illegal to make an instance of an abstract class with `new`. You can only instantiate its subclasses. In this case, we can just add the keyword `abstract` into the class declaration:
```java
public abstract class Vehicle {
	//...
}
```

Because abstract classes are not allowed to be constructed without a subclass, you can place abstract methods in the abstract class. These are methods that have no body, and must be overridden in any non-abstract, or concrete, subclasses. For example, to add a `makeNoise` method to vehicles:
```java
public abstract class Vehicle {
	//...
	public abstract void makeNoise();
	//...
}

public class Car {
	//...
	public void makeNoise() {
		goVrooom();
	}
	//...
}

public class Bike {
	//...
	public void makeNoise() {
		squeeak();
	}
	//...
}
```

# Interfaces
Now we introduce a new structure of OOP. Interfaces are collections of abstract functions. Interfaces have the same polymorphic traits as abstract superclasses, with a few exceptions: interfaces cannot have any function bodies defined; interfaces are `implement`ed by classes and `extend`ed only by other interfaces; multiple interfaces can be implemented or extended.

It is often best to think about an interface as a well defined set of functionality. Using interfaces has the advantage that you can maintain multiple implementations of an interface and swap out implementations by changing only the line where a class is instantiated and cast as the interface. This has many useful implications, especially in rapidly changing code bases like code for a robot, where major design changes involve changing an implementation in the code, while preserving all logic code that manipulates the robot through the interfaces. 
