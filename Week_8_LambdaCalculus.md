# What is Lambda Calculus and How do I Use it?

## What is Lambda Calculus?
You can think of Lambda Calculus more like a calculator than a programming language. It is far more useful for mathemeticians than software engineers, but is still extremely important to know because it is one of the simplest programming languages out there. As the saying goes, "gotta learn how to walk before we can run."


## Programming Constructs:
- **Abstraction**:
    - If *e* is a program (also called an expression), possibly containaing a variable *x*, then <br />
    `λx.e` <br/>
    is the program (or function), which has a formal parameter *x*. This is called abstraction, because the program `λx.e` does not depend on *x* anymore, *x* is abstracted away. This is explained more below.

- **Application**:
    - If *e1* and *e2* are programs then <br/>
    *`e1e2`* <br/>
    is the program which applies the function *e1* to the argument *e2*.

- **Variables**:
    - The basic programs are just the variables.


## Helpful Videos:
Here are some helpful videos Dr. Kurz uploaded to YouTube about Lambda Calculus:
- [Lambda Calculus Syntax](https://www.youtube.com/watch?v=D0kH1BpNr14&feature=youtu.be)
- [Parsing Lamda Calculus Expressions 1](https://www.youtube.com/watch?v=eYstx7uuE6c&feature=youtu.be)
- [Lambda Calculus Semantics](https://www.youtube.com/watch?v=h4aT42t7v9c&feature=youtu.be)


## How is it Different from a Language Like C#?

### Syntax:
Let's take a basic function in C# and convert it to a lambda expression. 

Here is a basic C# function that just adds 1 to the input and returns the result.
```
int plus_one(int x)
{
    return x + 1;
}
```
A pretty basic function, but C# is far from a basic or simple language. There's a lot on that function that's completely useless for a language as simple as Lambda Calculus.

First of all, lambda calculus has no types. Lambda Calculus is, as the name suggests, built primarily for math, so everything is assumed to be an integer, float, or a double. So we remove types.
```
plus_one(x)
{
    return x + 1;
}
```
Now, why do we have a return statement? You've never seen a function in math class with a return statement. Every function just returns the last value of computation.
```
plus_one(x)
{
    x + 1;
}
```
Now, why do we need a different name for the function? The vast majority of functions in math are just *F*, like *F(x)*. Any other naming is probably only because you already have an *F* function. So in Lambda Calculus we remove the function name.
```
(x)
{
    x + 1;
}
```
Now we are left with the pure basics: an input and a computation. But this is still in C-based syntax. In Lambda Calculus, we dont signify the starting of a function with parenthesis nor do we use square brackets to denote the beginning and end of a computation. We start a function with λ and separate the parameters from the computation with a period. So our plus_one function ends up being this:
```
λx. x + 1
```

One thing to note about this conversion is that the abstraction we defined earlier still applies. This is similar to C# where the parameter *X* is only a placeholder and has no handle on what the function actually does, so we could name it anything we wanted from simply changing it to *Y* or to *SomeSuperLameNumber*. Neither Language care or even notice the difference.

### How do we call these functions?
**Note: the words "call" and "apply" are interchangeable.**

So in C# or really any C-based language, we would call the plus_one function by writing
```
plus_one(2);
```
As we determined earlier, the function plus_one is equal to `λx. x + 1`, we would write
```
(λx. x + 1)(2)
```
We surround the equivalent function with parenthesis because it makes it easier to read, but they are not entirely necessary. The parenthesis around the parameter of 2 are only there for the same reason.