### Specification

- Let $x, y \in N$ be given. 
- The number $z$ is the **greatest common divisor** of $x$ and $y$ iff $z|y$ and $z|x$ and there is no $z'$, with $z' > z$, such that $z'|x$ and $z'|y$.
- Here $z|x \equiv \exists a \in N  .  a*z = x$

### Imperative GCD

```java
public static in gcd (int x, int y) {
	while (x != y) {
		if (x > y) x = x-y;
		else y = y - x;
	}
	return x;
}
```
- Consists of control flow and assignment(changes computer's state)

### Functional GCD
```Haskell
gcd x y
  | x == y    = x
  | x > y     = gcd (x - y) y
  | otherwise = gcd x       (y - x)
```
- Formalizes _**what**_ should be computed, rather than _**how**_