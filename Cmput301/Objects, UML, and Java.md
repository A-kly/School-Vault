# Important concepts
![[Pasted image 20240112100013.png]]
# Object-Oriented Models
![[Pasted image 20240112100427.png]]
## Java
Principal designer: James Gosling, Sun Microsystems
Language goals:
- simple, object-oriented
- robust, secure
- network and thread support
- “compile once, run anywhere”

- Language design inspired by …
	- Lisp - garbage collection, reflection (ask object info about itself)
	- Simula-67, C++ - classes
	- Algol-68 - overloading (same method name can take multiple kinds of parameters (multiple constructors))
	- Pascal, Modula-2 - strong type checking (ensuring types are compatible and checking it in the compiler (cannot call floats integers for example)) 
	- C - syntax (kinda)
	- Ada-  exceptions
	- Objective C, Eiffel - interfaces (take objects that are unrelated and treat them as if they are the same, *they can be thought of as **contracts** for classes saying "yes my object does this thing"*)
	- Modula-3 - threads
# UML (Unified Modeling Language)
Principal inventors: Grady Booch, Ivar Jacobson, James Rumbaugh
Purpose:
- express object-oriented designs visually
- programming language independent
- communicate, evaluate, and reuse designs
- make design intent more explicit
- can think about design, before coding
## Abstraction
- Object:
	- an entity with specific attribute values (state), behavior, and identity
	- typically instantiated from a class
- Class (factory and structure of objects):
	- associated type of an object
	- defines attributes and methods
### Java and UML Class
![[Pasted image 20240112102336.png]]
==*Class* is represented by a Box, any important *attributes* should be put in second box section (not used often), *methods* should be put in third box section.==

## Encapsulation
- Class:
	- access control for attributes and methods *(Getters or setters used instead)*
		- e.g., public or private
	- access is not the same as visibility 
	- “design by contract” *(public, private, protected)*
		- *public interface represents a contract between the developer who implements the class and the developer who uses the class*
### Example:
![[Pasted image 20240112102955.png|500]]
![[Pasted image 20240112103003.png|500]]
![[Pasted image 20240112103015.png]]
- This is the previous code in UML
- Notice how we use `name:type` notation in UML instead of `type name` notation.
- Attribute and method name order should be logical
- Constructor has same name as class

## Decomposition
Association relationship:
- “some” relationship between classes
	- e.g., between Book and Patron
### UML Association
![[Pasted image 20240112103632.png]]
- *Looks like database diagrams*
- related
- NOT ownership
## More decomposition
Aggregation relationship:
- weak “has-a” relationship
- whole “has-a” part
	- eg. hands has a fingers
- a part may belong to (be shared with) other wholes
- e.g., a Section and a Student
### Java and UML Aggregation
![[Pasted image 20240112104220.png|400]]
- section *has a* student
	- BUT *student can be shared with other classes*
- "DIAMOND GOES TO THE JEWLERY BOX"
	- aka, UML diamond goes to container or "holder" in the relationship
- **weak relationship = hollow diamond = students and sections can exist separately**
![[Pasted image 20240112104727.png]]
- one Locations can be held by several frames (cursor, etc. )
- one size can be held by many frames (Fullscreen, etc.)
## More MORE Decomposition
Composition relationship:
strong “has-a” relationship
exclusive containment of parts
related object life times
the whole cannot exist without having the parts; if the whole is destroyed, the parts should also be destroyed
often access the parts through the whole

==MISSED CLASS DUE TO PASSPORT APPOINTMENT, missed UML stuff==
# Generalization
- Look for commonalities:
	- Common attributes
		- eg. all vehicles have...?
	- common methods (behaviour)
		- eg. all vehicles have...?
- **Generalize:** find what is common and factor it out into a more general "base" abstraction

- **Implementation inheritance:** generalize about method signatures, method implementations, and/or attributes
- **General part:** Superclass/ base class defines attributes and methods to be shared
- **Specific part:** extends superclass, is a derived class (subclass) which can overide methods, add methods and add attributes
## Java Implementation Inheritance
```java
public class Shape { // superclass
	protected Location myLocation;
	public Shape() { … }
	public void setLocation( Location p ) { … }
	public Location getLocation() { … }
	}
	

public class Circle extends Shape { // subclass
	private int diameter;
	public Circle() { … }
	public void setDiameter( int d ) { … }
	…
	}
	
public class Square extends Shape { // subclass
	private int side;
	public Square() { … }
	public void setSide( int s ) { … }
	}
```
- Both circle and square extend shape
- a circle is not a square
- a square is not a circle
- a shape is a shape
- circle and square have added attributes
	- diameter for circle
	- side for square
## UML Inheritance
- Implementation inheritance relationship:
	- *“is-a*” relationship between classes
	- subclass “is-a” kind of superclass
	- subclass “*extends*” superclass
	- eg. **Circle “is-a” kind of Shape**
![[Pasted image 20240117101010.png|400]]
- We don't need to add "multiplicity" (aka, a certain number of circles are shapes, aka, quantity)
## Generalization Principles
- **Inappropriate inheritance**:
	- subclass inherits from superclass but "is-a" relationship does not exist
	- **if "is-a" test fails:** *No inheritance* is appropriate
	- **if "is-a" test passes:** *may or may not* be appropriate
- **Liskov substitution principle:**
	- an instance of a subclass should always be able to be substituted anywhere a reference to a superclass object is used
	- aka: *we should be able to treat all subclasses at their superclass always in any scenario*
```java
Shape s;
s = new Circle(); // instance of subclass
…
Location l = s.getLocation(); // superclass method
```
## Inheritance Example
Suppose:
- class Dog
	- provides bark(), fetch()
- class Cat extends Dog
	- “hides” bark(), “hides” fetch(), and adds purr()
- Is Cat a Dog??
	- **Absolutely not, we cannot call bark or fetch on them, Liskov substitution principle is not followed**
	- We should separate these two classes
## Inheritance Example 2
Suppose:
- class Window
	- provides show(), move(), resize()
- class FixedSizeWindow extends Window
	- “hides” resize()
- FixedSizeWindow “is a” Window?
	- **Maybe?? If we wanna use FixedSizeWindow as a Window, then it will cause problems. Liskov's principle is violated.**
	- We should separate these classes. `resize()` could be separated to another place. We could make two classes with no inheritance (FixedSizeWindow and ResizableWindow). 
## Inheritance Example 3
Suppose:
- class ArrayList
	- provides add(), get(), remove(), …
- class ProjectTeam extends ArrayList
- ProjectTeam “is a” ArrayList?
	- **Maybe? Arraylist does more things than what ProjectTeam does. ProjectTeam is not supposed to be an ordered collection of objects. Arraylist is doing too much.**
	- ProjectTeam shouldn't **BE** an ArrayList, it might wanna just **HAVE** an ArrayList as an attribute.

## Inheritance Issue
- Problem:
	- superclass method is inherited, but it is not appropriate what to do?
```java
public class Rectangle {
	public Rectangle( Size s ) { … }
	public void setLocation( Location p ) { … }
	public void setSize( Size s ) { … }
	public void draw() { … }
	public void clear() { … }
	public void rotate() { … }
	}
	
public class Square extends Rectangle {
	// inherits setSize(), but want to “hide” it
	}
	// Square ‘is a’ Rectangle?
	// Square specializes Rectangle?
```
What can we do??
### Override the Method Approach
```java
public class Square extends Rectangle {
	public void setSize( Size s ) {
	// should not implement
		}
	}
```
- This *violates Liskov's substitution principle.*
### Aggregation Approach
```java
public class Square {
	private Rectangle rect;
	// Square ‘has a’ Rectangle,
	// not ‘is a’ Rectangle
	public Square( int side ) {
		rect = new Rectangle(
		new Size( side, side ) );
	}
…
	public void setSide( int newSide ) {
		rect.setSize(
			new Size( newSide, newSide ) );
	}
		
	public void draw() {
		rect.draw();
	}
…
}
```
- In this case, *Square is not considered a rectangle by java*
### Restructuring Approach
```java
public class Quadrilateral {
	…
	public Quadrilateral() { … }
	public void setLocation( Location p ) { … }
	public void draw() { … }
	public void clear() { … }
	public void rotate() { … }
}
	
public class Rectangle extends Quadrilateral {
	public Rectangle( Size s ) { … }
	public void setSize( Size s ) { … }
}
	
public class Square extends Quadrilateral {
	public Square( int side ) { … }
	public void setSide( int side ) { … }
}
```
- We make a larger superclass to encompass all required behaviours
- In this case, *Square is not considered a rectangle by java, it **is** considered a quadrilateral*
## Inheritance But more
- Java abstract class:
	- *declares one or more abstract methods*
	- **cannot be instantiated**; must be subclassed and have abstract methods overridden
```java
public abstract class Shape {
	public abstract double area();
	public abstract double perimeter();
	// there may be other instance data and methods
}
class Circle extends Shape {
	public double area() { … }
	public double perimeter() { … }
}
```
## Interface Inheritance
- Java interface:
	- **declares method signatures**
	- classes implement the interface by providing all the method bodies
	- **a “contract”, specifying a capability that an implementing classes must provide**
	- cannot be instantiated 
	-  may extend other (sub)interfaces
```java
public interface Bordered {
	public double area();
	public double perimeter();
}
class Circle implements Bordered {
	public double area() { … }
	public double perimeter() { … }
}
```

```java
public interface Transformable extends Scalable, Translatable, Rotatable {
	…
}
```
This is an example of 3 interfaces
### Java Interface example
```java
public interface Cloneable {
	public Cloneable clone();
}

public class Color implements Cloneable {
	private int red;
	private int green;
	private int blue;
	
	public Color( int r, int g, int b ) { … }
	
	public Cloneable clone() {
		return new Color( red, green, blue );
	}
}
Color red = new Color( 255, 0, 0 );
Color redClone = (Color) red.clone();
```
### UML Interface
![[Pasted image 20240117104921.png]]
## Abstract Class versus Interface
- Differences:
- an abstract class may provide a partial implementation
- a class may implement any number of interfaces, but only extend one superclass

- adding a method to an interface will “break” any class that previously implemented it
# Java Subtleties
## Java Call-by-Value
==The VALUE of each argument is **copied**==
```java
public class Sender {
	public void send() {
		Receiver r = new Receiver();
		Info argRef = new Info();
		r.receive( argRef ); //This line sends argRef to the receive() function
		argRef.doSomeMore(); //argRef can still be accesed here due to Call-by-Value
	}   // argRef IS GOING TO BE CHANGED by what happens in receive()
}
public class Receiver {
	public void receive( Info infoRef ) {
		infoRef.doSomething(); //infoRef IS CHANGED becuase we apply .doSomething() to the object id
		infoRef = null; //We set infoRef to null HERE, NOT IN THE SENDER FUNCTION
	}
}
```
- Every object variable in Java is essencially the object's ID
- We can manipulate the object from anywhere that we pass the object id because Java finds the object associated with the ID, does something with it and then returns
- Line 12 works and DOESN'T affect the object reference in line 6
- THIS ENTIRE THING IS PRETTY MUCH LIKE POINTERS, **References do not have a constant memory location**, Java does not have actual pointers at all.
- `.` operator is incredibly powerful
	- on method, if object does exist, ask class of object if it has the corresponding method, change `this` in the class methods to the value of object before `.`
		- if method doesn't exist in class, ask superclass
## Java Constructors
```java
public class Base {
	protected int value;
		public Base() {
		//There is an invisible (implicit) super() call here
		value = -1;
	}
}

public class Derived extends Base {
	public Derived() {
	//There is an invisible (implicit) super() call here
	}
}

Derived d = new Derived();
d.value; //What does this return?????
         //THERE IS AN INVISIBLE super() call in Derived()
```
- `super()` is a call to the object's superclass constructor
	- It is automatically injected if it is left out

```java
public class Base {
	protected int value;
	public Base( int initValue ) {
		// implicitly inserted call to super()
		value = initValue;
	}
	public Base() {
		this( -1 );
		// this( … ) if used, must come first
	}
}
public class Derived extends Base {
	public Derived( int initValue ) {
		super( initValue );
	}
	public Derived() {
		// implicitly inserted call to super()
	}
}
Derived d = new Derived();
```
![[Pasted image 20240119104940.png]]
**BAD**