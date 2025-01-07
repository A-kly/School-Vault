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
