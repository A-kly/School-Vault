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
![[Pasted image 20240112102955.png]]
![[Pasted image 20240112103003.png]]
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
