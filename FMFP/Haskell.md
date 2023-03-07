##### Haskell is a **Lazy** Pure Functional Language
- Lazy programming language only evaluates arguments when strictly necessary, thus,  
	1. avoiding unnecessary computation and  
	2. ensuring that programs terminate whenever possible. For example, given the definitions
### Introduction
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
- Useful GHCi commands:
	- :?                                -- Help! Show all commands  
	- :load $test$                   -- Open file test.hs or test.lhs
	- :reload                       -- Reload the previously loaded file 
	- :main $a1$ $a2$                -- Invoke main with command line args a1 a2 
	- :!                                 -- Execute a shell command
	- :edit $name$                 -- Edit script name
	- :edit                            -- Edit current script
	- :type $expr$                  -- Show type of expr
	- :quit                            -- Quit GHCi
### Syntax
- Haskell function [[GCD (Greatest Common Divider)|example]]
- [[XOR - function definition|Multiple ways to define a function]]
- Functions are defined as equations:
```haskell
square x = x * x             add x y = x + y
```
- Parentheses are often needed in Haskell too 
```haskell
> add (square 2) (add 2 3)
9
```
- Function application has the highest precedence 
```haskell
square 2 + 3
--means
(square 2) + 3 
---not 
square (2+3)
```
- Function application operator $ has the lowest precedence and is used to rid of parentheses
```haskell
sum ([1..5] ++ [6..10]) -> sum $ [1..5] ++ [6..10]
```
- Another (more reasonable) example
```haskell
x +/- y = (x+y, x-y)

> 10 +/- 1
(11,9)
```
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

### Types
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
	- `show` converts values to `String`
		- `? show 23` -> `"23"`
		- `? show True` -> `"True"`
		- `? show (17, 'a')` -> `"(17,'a')"`
		- `? show (17 + 42)` -> `"59"`
	- `read` converts `Strings` to values. **Always specify the desired type!**
		- `? read "23" :: Integer` -> `23`
		- `? read "23" :: Double` -> `23.0`
		- `? read "(17, 'a')" :: (Int, Char)` -> `(17,'a')`
		- `? (read "17" :: Int)+(read "42"::Int)` -> `59`
		- `? read "17+42" :: Int` -> `Exception: Prelude.read: no parse`


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
### Input and Output
- ###### How would we write this in Haskell?
```java 
void f(String out) {
   String inp1 = Console.readLine();
   String inp2 = Console.readLine();
   if (inp2.equals(inp1)) System.out.println(out); }
```
- Wrap types in **IO** to capture side effects
```haskell
getLine :: IO String.       putStrLn :: String -> IO ()
```
- Syntax for IO type:  
	- do block sequences side effects I <- extracts values from IO  
	- return wraps values in IO
	```haskell
	f :: String -> IO ()
	f out = do
	  inp1 <- getLine
	  inp2 <- getLine
	  if inp2 == inp1
	    then putStrLn out
	    else return ()
	```


### Running main function
-  `main :: IO ()` is the entry function for Haskell programs
```haskell
main :: IO ()
main = do
   putStrLn "Enter your name:"
   name <- getLine
   putStrLn ("Hello, " ++ name ++ "!")
```
- compile with ghc
	```shell
	> ghc hello.hs
	> ./hello
	Enter your name:
	David
	Hello, David!
	```
- run with GHCi
	```shell
	> ghci
	? :load hello.hs
	? main
	Enter your name:
	David
	Hello, David!
	```
- ##### No Escape from IO
	- IO sticks to values – this must be handled!
		- Best to compute with IO values in do blocks 
		- Clumsier than with pure expressions  
		- Results are wrapped, too
		- Stay out of IO as long as possible
		- Separate computations from user interface
		```haskell
		---Side effects-----------------------Pure------------------
		main :: IO ()                    gcd :: Int -> Int -> Int
		main = do                        gcd x y
		  n <- getLine                    | x == y    = x
		  m <- getLine                    | x > y     = gcd (x-y) y
		  let x = gcd (read n) (read m)   | otherwise = gcd x (y-x)
		  putStrLn (show x)
		```
