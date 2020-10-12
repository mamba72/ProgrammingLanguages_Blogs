# Learning Functional vs Imperative Programming Langauges

## What are functional and Imperative Languages?
Every language you've learned so far is an Imperative language. Imperative langauges are (vast majority) Object Orientated, very linear, and more commonly used. 

Functional languages are almost entirely function based, meaning you wouldn't write lots of sequential statements to change a variable as the program runs, you would create many smaller functions to do the smaller tasks you need to accomplish. Functional languages usually have a more mathematics feel to them rather than the purely operational and linear structure from imperative ones.



## Real Examples:

My prefered programming language is C#, so all my Imperative langauge examples will be in C#. 


### Function Definition and Implementation
A C# function for selecting the elements at even indicies in a list:
```
public List<string> Evens(List<string> myList)
{
    List<string> evensList = new List<string>();
    for(int index = 0; index < myList.size(); index += 2)
    {
        evensList.add(myList.get(index));
    }
    return evensList;
}
```

A Haskell function for the same thing:
```
select_evens :: [a] -> [a]
select_evens [] = []
select_evens [x] = []
select_evens (x:y:ys) = y : select_evens(ys)
```

<b>Differences:</b>
1. We can see that the Haskell one is far shorter and much less writing, but in my opinion much harder to follow. That opinion is probably only a result of me using Imperative languages for much longer. 
1. We can also see that Haskell does not have an explicit "return" when C# does.
1. Haskell also does not have explicit parameters. It just has a letter in brackets to signify "some list".
1. Haskell functions are also far more commonly recursive while imperative are usually iterative.
1. In C# the body of the function is shown by using the curly brackets {} while Haskell it's only the following lines after a function declaration (the first line of the function).
1. The haskell function is composed of 3 different cases and Haskell knows which case to use based on the arguments. In the example, the first case is when the list is empty, second for when list has only one element, third is a generic, recursive case.

## When to Use Imperative vs Functional

Imperative languages are often better for larger, more complex projects. You would never want to write a new video game in Haskell, but its extremely common to build games in C#. Functional languages are much better suited for smaller, very fast applications that are more math focused.