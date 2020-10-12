# Abstract Vs Concrete Syntax

## What is Abstract Syntax?
Abstract syntax is very similar to descrete syntax. The syntax is all about what does it really mean to say "add" or "subtract" and what is the computer really doing under the hood. In abstract syntax we express the number 3 as SSSO or as in discrete it would be 0->->->.

IF we were trying to solve the expression 1 = 2 * 3 with abstract syntax, we would need to translate the numbers into our discrete-like form and translate the math symbols into functions because the + sign doesn't work on SSSO. The translation steps would look like this:
```
1 + 2 * 3
SO + SSO * SSSO
Add SO (Multiply SSO SSSO)
```
This starts to look much more like the programming we are used to. 

## What is Concrete Syntax?
Concrete syntax is closer to what you are used to, but not quite the same. Concrete syntax in this class is all about using the complex syntax we already know to understand parsing. In this class we used that syntax to show how a computer actually sees the following expression and how it understands how to do order of operations:
```
1 + 2 * 3
```

How does the parser know that in reality, that expression is executed like this:
```
1 + ( 2 * 3 )
```
What the parser does is represent every expression as a tree. Using a tree allows for very quick execution of statements like these and very easy uses of recursion. The below tree is the representation of our original expression.
```
    Plus
     / \ 
  Num   Times
   |      / \
   1   Num   Num
        |     |
        2     3

```
(Num is when we convert the symbol of 1 to the actual value 1. Think of it like parsing the string "1" to the int 1)

But how does the parser know to do this? It is actually a group of relatively simple rules it needs to follow. 
```
Exp -> Exp '+' Exp1                                
Exp -> Exp1                                        
Exp1 -> Exp1 '*' Exp2                              
Exp1 -> Exp2                                       
Exp2 -> Integer                                         
Exp2 -> '(' Exp ')'                                
```

It is a very recursive way to approach the expression. It some of the statements are very self explanetory and seem a little overly simple, but that's the great part. It is not as difficult to understand as you'd expect. All the first line is doing is splitting an expression at the equals sign. If we used | as a way to show how/where we split the function, this is the two statements.
```
1 + 2 * 3
1 | 2 * 3
```

So in the first statement Exp is the entire expression, but in the second statement, Exp = 1 while Exp1 = 2 * 3. If you were to write down every single individual step that you made while solving this expression, it would end up being very similar if not exactly the same as those rules mentioned earlier.