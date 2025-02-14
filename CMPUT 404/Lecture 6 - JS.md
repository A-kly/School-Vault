- Use W3schools to learn and experiment
- Use fiddle to look at live js stuff
- Use browser console
- JS runs locally on client
	- Can update info quickly
- Looks a bit like python
	- `function` instead of `def`
- Closure
	- Inner functions can see outer variables
	- outer functions **cannot** see inner variables
- Scope
	- By default, variables are always global
	- `var` makes variables local to FUNCTION
	- `let` is for a variable used only in a small context (let, while, etc.)
	- `const` fixed value
	- **Scope is defined by curly brackets**
- Type coercion
	- "1" + 1 in python = ERROR
	- "1" + 1 in JS = "11"
	- Always try to coerce to str if str is there
- objects and prototypes
	- like struct
	- objects 
		- just has values
	- prototypes
		- has user created functions
- loops
	- `for ... in ...`
	- can loop over object values
- Classes
	- most controvertial part of JS
	- js has many ways of creating them
- Recomended
	```js
class Pokemon {
  constructor(name, level) {
    this.name = name;
    this.level = level;
  }
  levelUp() {
    this.level += 1;
  }
}
pikachu = new Pokemon("Pikachu", 1);
pikachu.levelUp();
```
- old way of doing it
```js

// classes start with a capital letter by convention
function Pokemon(name,level) {
  this.name = name;
  this.level = level;
  this.levelUp = function() {
    this.level += 1;
  }
}
pikachu = new Pokemon("Pikachu", 1);
pikachu.levelUp();
```
- You might also see the methods added to the prototype later
```js
 // classes start with a capital letter by convention
function Pokemon(name,level) {
  this.name = name;
  this.level = level;
}
// have to include "prototype" here so "this" works in the method
Pokemon.prototype.levelUp = function() {
  this.level += 1;
}
pikachu = new Pokemon("Pikachu", 1);
pikachu.levelUp();
```
- Awkward and rarely used
```js
// classes start with a capital letter by convention
var Pokemon = {
  name: null,
  level: null,
  levelUp: function() {
    this.level += 1;
  }
}
pikachu = Object.create(Pokemon);
pikachu.name = "Pikachu";
pikachu.level = 1;
pikachu.levelUp();
```
# Manipulating the DOM (document object model)
- Tutorial is online at W3schools
- Using a hyperlink is not a DOM modification
- Using JS to modify the content of a page is a dom modification
- 