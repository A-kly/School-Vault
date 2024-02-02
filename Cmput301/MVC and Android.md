# Model/View/Controller
![[Pasted image 20240202103436.png|500]]
- **Representation:** how we store
- **Computation:** logic
- **presentation:** visualizing it
![[Pasted image 20240202103533.png|500]]
- Views ==can== modify the data (if they want)
![[Pasted image 20240202103614.png|500]]
- We want all views to be updated once the data is updated
- tell view to update
![[Pasted image 20240202103713.png|500]]
- views request data in order to update
## Model/View/Controller Roles
### Model
- entity layer
	- complete, self-contained representation of the data managed by the application
	- provides services to manipulate this data
	- *"the back end"*
- main responsibilities
	- representation and computation issues
	- sometimes persistence
- ==A good app should survive the removal of it's GUI==
### View
- boundary layer
	- set of user interface components
	- determines what is needed for a particular perspective of the data
	- *"the front end"*
- main responsibility
	- presentation issues
- ==This is the GUI==
### Controller
- control layer
	- handles events and uses appropriate information from user interface components to modify the model
- main responsibility
	- interaction issues
- ==Interact with views and model, onClick listeners, used to complete a task that interacts with view and model==
- ==Can be combined with view (like how we can edit a spreadsheet cell, it displays and also interacts)==

### All together
![[Pasted image 20240202104330.png]]
- delegate changes to view to controller
## Java Observer
- java.util.Observable superclass
```java
public class Observable {
…
public Observable() { … }

// “all models keep track of their views”
public void addObserver( Observer o ) { … }
public void deleteObserver( Observer o ) { … }

// “all models notify their views to update”
public void notifyObservers() { … }
public void notifyObservers( Object arg ) { … }

// note whether the model has changed
public boolean hasChanged() { … }
protected void clearChanged() { … }
protected void setChanged() { … }
…
}
```

- java.util.Observer interface
```java
public interface Observer {
	public void update( Observable s, Object arg );
}
```
# MVC Design Issues
