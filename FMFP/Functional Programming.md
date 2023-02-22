### Functions and values
- Functions compute values
- Functions are values: can compute and return them
- _**No side effects:**_ f(x) always returns the same value, compared to: 
	- Since no side effects, can reason as in mathematics. 
``` java
class Test {  
	static int y = 0;
	static int f (int x) {
		y = y + 1:
		return y;
	}
	public static void main (String() args) {
		System.out.printin(f(0));
		System.out.println(f(0)); // Different than last time
	}
}
```
### Basic Concepts 
##### [[GCD (Greatest Common Divider)|Example: OOP vs FP(GCD)]]
- This property is called **_referential transparency_**:
	- an expression evaluates to the same in every context.
		- No assignments  
		- No global variables
	- Easy to parallelize as computations cannot interfere
- Recursion instead of iteration
- Flexible type system
	- Avoids many kinds of programming errors (e.g. no runtime errors: 3+True => type error(at compile time))
	- Polymorphism supports reusability
		`sort [5,3,4]` 
		`sort ["hello", "there", "world"]`
