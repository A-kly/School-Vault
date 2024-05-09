## Big O Notation

- (Roughly) **"The set of functions which, as n gets large, grow no faster than a constant times f(n)"
- Definition: ***A function h(n) : N -> R belongs to O(f(n)) if there exists constant c > 0 and n0 in N such that for all n >= n0 it holds that 0 =< h(n) =< cf(n).
- In mathematical notation: _h(n) ∈ O(f(n)) ⟺ ∃c, n0 such that ∀n ≥ n0 , h(n) ≤ cf(n)_
**Examples**:
- 482n^2 ∈ **O(n^2)**
ALSO,
- 482n^2 ∈ **O(n^2.0001)**
ALSO,
- 482n^2 ∈ **O(n^2.5)**
ALSO,
- 482n^2 ∈ **O(n^3)**

- n^3 + 255n^2 + n^2.99999 ∈ **O(n^3)**
***

## Big O Notation

- (Roughly) **"The set of functions which, as n gets large, grow no faster than a constant times f(n)"
- Definition: ***A function h(n) : N -> R belongs to O(f(n)) if there exists constant c > 0 and n0 in N such that for all n >= n0 it holds that 0 =< h(n) =< cf(n).
- In mathematical notation: _h(n) ∈ O(f(n)) ⟺ ∃c, n0 such that ∀n ≥ n0 , h(n) ≤ cf(n)_
**Examples**:
- 482n^2 ∈ **O(n^2)**
ALSO,
- 482n^2 ∈ **O(n^2.0001)**
ALSO,
- 482n^2 ∈ **O(n^2.5)**
ALSO,
- 482n^2 ∈ **O(n^3)**

- n^3 + 255n^2 + n^2.99999 ∈ **O(n^3)**


**Steps**:
_h(n) ∈ O(f(n)) ⟺ ∃c, n0 such that ∀n ≥ n0 , h(n) ≤ cf(n)_

1. find and _c_ and _n0_ for each terms of h
3. add up all your _c_, take the maximum of your _n0_
4. add up all your inequalities to get the ONE inequality  
5. write down what is _c_ and _n0_

**Remarks**:

1. The values of _c_ and _n0_ are not unique
2. You do NOT need to find the smallest possible _c_ and _n0_
3. Do NOT show me _c_ = 204 * 10^6 and _n0_ = 2023 * 10^9
4. O(f(n)) is just an upper bound (not necessarily tight)


![[Pasted image 20230123102440.png]]
_C scales f(n)_
![[Pasted image 20230123102600.png]]
_For all n>= 2023, `204n^2 + 2023n + 90 ≤ 204n^2 + n^2 + n^2`_
_`204n^2 + n^2 + n^2 = 206n^2`_
_Thus, c = 206, n0 = 2023_


**Inverse definition**:
![[Pasted image 20230123103033.png]]
### Properties:
![[Pasted image 20230127100916.png]]

### Process

Divide the given f(n) function by the function we want to compare it to

eg:
`a^n+204 ∈ O(a^n) `

`a^n+204 / a^n `

`= a^204`

therefore: `c = a^204 for any n`
