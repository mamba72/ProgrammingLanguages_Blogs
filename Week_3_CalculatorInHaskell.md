# Calculator in Haskell

## Basis:
The goal of this lesson / assignment is to create a calculator in Haskell, but not using the built in math functions nor the built in Integer Type.

## Step 1: Define a Number
In our calculator we defined our number in a way that took inspiration from discrete math. In discrete a natural number is defined as how many steps (denoted as -> "next") it is from the base number of 0. So the number 3 would be 0->->-> because the number 3 is 3 steps after 0. The -> can also be thought of as +1. Because we felt that this is the best way to represent a number, we created a new data type in Haskell called NN for "natural numbers." 
```
data NN = O | S NN
    deriving (Eq,Show)
```

In Haskell we define a new data type by saying data \*the name of our type\* = \*a mathematial definition\*. We write "deriving" because we would like to take advantage of Haskell's ability to print to the console, so if we derive Show, it lets us use the standard printing function to print our objects. An important part of our definition is the fact that it's recursive. We have NN after S and that allows us to stack successors. 

So if we were to write the number 3 in our new data type it would look like (S(S(S(O)))) since O is our 0 and S is our form of ->. 

## Operations on Our Number
This is a number, we need to create functions to manipulate this number. We started with the most basic numerical operation: 
### Addition:

Our function starts with the declaration. We want our function to be called "add", it needs to take in two NNs and output an NN. This declaration should look like this:
```
add :: NN -> NN -> NN
```

Next, we need to handle our base case. The most "basic" case for addition with natural numbers is when you add 0 to a number since it just returns that original number. This case should look like this:
```
add O n = n
```
Next, we need to handle the generic situation where a number m is being added to n (written like n+m). This is a perfect situation for a recursive function. What does 2+3 even mean? It means 1 + (1 + 3). Pretty simple math, but an incredibly powerful statement. Since +1 or 1+ is the equivalent of ->, we can write that statement as (1 + 3)->. Written in Haskell with our data type it would look like this:
```
add (S n) m = S (add n m)
```

So our entire function will look like this:
```
add :: NN -> NN -> NN
add O n = n
add (S n) m = S (add n m)
```

### Subtraction:
The next relatively basic operation we need is subtraction. The subtraction function is very similar to the add function. We have an extra case where we just return O or 0 if we try to subtract anything from O because we are unable to represent negative numbers.
```
subtr :: NN -> NN -> NN
subtr O n = O
subtr n O = n
subtr (S n) (S m) = subtr n m
```