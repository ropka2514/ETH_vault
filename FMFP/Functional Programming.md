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
## Intro to Functional Programming
- Functions can be defined in file and loaded on console with 
```shell
<Main> :load gcd.hs
[1 of 1] Compiling Main    ( gcd.hs, interpreted )
```
- And executed
```shell
<Main> gcd 9 12
3
<Main> tail [1,2,3]
[2,3]
<Main> head [1,2,3]
1
<Main tail ( tail [1,2,3])
[3]
```
- Function definition build from both patterns mi and guard gi
	```haskell
	fun m1 ... mn
		| g1        = e1
			.
			.
		| gm        = em
		| otherwise = e -- optional!
	```
	- Patterns `mi` are variables, constants, or build from data constructurs (tuples)
	- Guards `gi` are Boolean expressions
	- Pattern matching forces [[Expression evaluation|evaluation]]
#### Syntax
- Haskell function [[GCD (Greatest Common Divider)|example]]
- Function consists of different cases(evaluated from top to bottom in case of overlap):
```haskell
functionName x1 ... xn
	 | guard1 = expr1 -- guard are condisions 
	 | guard2 = exprm -- expressions are outputs
```
- Program consists of several definitions:
```haskell
myConstant = 5 -- constant function

aFunction y1 ... ym
	| guard1 = expr1
	| guard2 = expr2

anotherFunction x1 ... xn = ...
```
- Indentation determines separation of definition:
	- All function definitions must start at same indentation level.
	- If a defintion requires n > 1 lines, indent lines 2 to n further
- Recommended layout:
```haskell
f1 x1 x2
	| a long guard which may go over 
	  a number of lines
	    = a long expression that can go over
		  several lines
	| g2 = e2

f2 x1 x2 x3 = ...
```
- Erroneous layout:
```haskell
square x = x * x
 cube x = x * x * x -- parse error on input '='
 
```
- Spaces are important. 
	 ### Do not use TABs!!

#### Types
- Haskell is strongly typed language
- Either programmer provides types along with function definiton `gcd :: Int -> Int -> Int` or the System computes types itself.
- Function/argument types must "match"
```
gcd 3 True  

<interactive>: 1:1: error:
- ﻿﻿No instance for (Integral Bool) arising from a use of 'gcd'
- In the expression: gcd True 3
In an equation for 'it': it = gcd True 3
```
- $Int$ Type with at least the range $\{-2^{29} , ..., 2^{29} - 1\}$
	- Support for unbounded integers and arithmetic: $Integer$
	- Functions: +, -, ^, div, mod, abs
	```
	? mod 7 2
	1
	```
	- An infix function is called an "operator"
	```
	? 7 'mod' 2
	1
	```
	- Operator can also be written in prefix notation
	```
	? + 3 4
	<interactive>:1:1: parse error on input '+'
	? (+) 3 4
	7
	```
	- Operators have different binding strength (^ bind stronger than +)
- $Bool$: True, False
	- Binary __*operators*__ &&, ||, unary __*function*__ $not$ as expeted
		- not binds stronger than && and ||
		- ($==$) on Bool is **"if and only if"**
	- [[XOR - function definition|Example: definiton of XOR]]
- $Char$: **'** a **'**, **'** b **'**, ...
	```shell
	? ord 'a' -- requires Char module loaded with :module Data.Char
	97
	? chr 97
	'a'
	```
- $String$: "hello", "abc", ...
	```shell
	? "Hello" ++ "there"
	"Hello there"
	```
- $Double$: 0.3456
	- Functions like +, -, * , / , abs, acos, asin, ceiling, ...
- $Tuple$
	- Used to model composite objects ("records")
	- **Example**: Student has name, ID number, starting year
		- Type `(String, Int, Int)`
		- with element `("Ueli Naef", 1234, 2015)`
		- Tuple type has to have $n \ge 2$ elements 
	- Functions can take tuples as arguments or return tupled values
		```haskell
		addpair :: (Int, Int) -> Int
		addPair (x,y) = x+y
		? addPair (3,4)
		7
		```
	- Patterns can be nested
		```haskell
		shift :: ((Int, Int), Int) -> (Int, (Int, Int))
		shift ((x, y), y) = (x, (y, z))
		```
	- Patterns matching can be used to decompose tuples
		```haskell
		name (s, id, y) = s
		stuNumber (s, id, y) = id
		year (s, id, y) = y
		```