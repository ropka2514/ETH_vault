#### ﻿﻿xor defined using other operators:  
    xor x y = (x I| y) && not (x && y)
#### ﻿﻿xor defined using guards:  
```haskell
xor x y
	| x         = not y
	| otherwise = y
```
#### xor defined using multiple cases (new):  
```haskell
xor True True = False  
xor True False = True 
xor False True = True
xor False False = False
```
#### Cases can contain variables ( "patterns"):  
```haskell
xor True  y = not y 
xor False y = y
```
