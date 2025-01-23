- Lists are a special case of this format where cdr of the last element is equal to `nil`
- Lisp prints s-expr in their simplest form
```lisp
* (cons (cons 1 (cons 2 3)) 4)
((1 2 . 3) . 4)
* ’(a . (b . (c . nil)))
(A B C)
* ’(a b . (c))
(A B C)
* ’(a . (b c))
(A B C)
* ’(a b . (c . nil))
(A B C)
```
- In order to simplify, follow series of operations with car and cdr to figure out structure, then simplify
- every time we get to another dotted pair, we set `car` to be that dotted pair