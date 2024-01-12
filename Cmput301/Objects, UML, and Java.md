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