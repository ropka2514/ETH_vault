### Strategies
- Eager evaluation: evaluate arguments first
	- Also called "call-by-value"
	- Corresnponds to lefft path in picture
- Lazy evaluation: evaluate arguments only when needed (Haskell)
	- Also called "call-by-need" or "left-most/outermost"
	- Certain functions force evaluation, e.g. arithmetic
- `diff x y = x - y`
![[Pasted image 20230222204609.png]]
