# Fun - A simple functional Language
- A program in the `Fun` language is a collection of functions
- Functions defined over lists and atoms
- computations = functions evaluated on argument(s)
- math like syntax (for now)

>[!example]
> $$f (x, y) = x ∗ x + y$$
> - The symbol = is read as is defined as
> - f(x,y) is called the lefthand side
> - The function definition is on the righthand side

## Function Evaluation
- The function definition means that the two expressions are equal
- As in math, apply the function by replacing terms that are equal with eachother
- As defined in the example, we can replace the left hand side with the right hand side for ANY `x` and `y`
- This is the same as having "for all" quantifiers for each variable:
$$ ∀x∀y : f (x, y) = x ∗ x + y$$
- we can make an interpreter that mechanically evaluates this functions
- needs to do two things
	- replace f by it's definition (righthand side)
	- substitute variables
	- -> = "result of evaluation is..."
- eg
	- f (2, 3) = 2 ∗ 2 + 3 -> 7
## Terminology
- Syntax
	- Which text is valid?
- Semantics
	- Meaning of program
- Execution
	- Evaluating function applications, ( in prev example, replacing equals by equals)
### Function terminology
- Function
	- Mapping of domain to co-domain
- Function definition
	- What do?
- Application
	- Evaluate for specific argunments

## Objects in Fun
- Atoms
	- primitive, inseperable, includes reals
- Lists
	- Defined inductively
	- () is empty list
	- if `x1...xn` are atoms, `(x1...xn)` is a list
	- Nothing else in list
### List examples
- Nested lists are allowed
- `(a (b) c (d))`
- `(a ((b) c (d) ((((e))))))`
- `(((((((((()))))))))(((()))))`

