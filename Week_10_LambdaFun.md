# LambdaFun and its Quirks

## What on Earth is LambdaFun?
LambdaFun is the language you will be using for the last assignment. You will be making a circular linked list. The language has very strange properties especially with variable management.

## What are the improvements over the previous Lambda Calculus
- Memory Management:
     - Pointers
     - Keyword "New"
     - Dynamic Allocation of Variables
     
There's not much in that list, but it opens up a whole new world of possibilities.

For example, it allows us to make new lists on the fly that contain objects rather than only primitives. The function Dr. Kurz gave us was the "newCList" function which makes a new circular list node.

```
val newCList = \e.
    let val a = new [] in
    a := [e,a];
    a;;
```
The function above takes in an element called "e", creates a new list, and makes a list pointer called "a". Then it takes *a* and points it to a list with 2 elements, the argument given and *a* (the address of itself). Then the function returns the pointer to this newly created list.

This is wildly useful because it allows manipulation of quite large and complex objects using their pointers.

## Some Issues with the implementation
There are issues that my partner and I faced while tackling this assignment. These "issues" aren't real problems or bugs in the language, but rather just quirks that threw us off and made the assignment significantly harder.

The quirk that gave us such a hard time was the fact that we couldn't get a variable to stay initialized for more than 1 line. This is a piece of code from the assignment that my partner and I tried and at first glance seems like it should work.
```
val insert = \e. \a. 
    let val newNodePtr = newCList(e) in
    let val afterAObj = (next a) in
    next newNodePtr := afterAObj;
    (next a) := newNodePtr;;
```

So the insert function takes in an element to insert into the list, and the address of the node you want to insert after. We create a new pointer that's pointing at the newly created list node from our previous function. We create a pointer to maintain the ability to grab the node after *a* because our new node is supposed to point to that, not the node called *a*. Next we are assigning newNodePtr's "next" address (the pointer to the next node in the list) to be the object after *a*. So at that first semicolon, two a new node has been created, is pointing at the following node, and is ready for us to point the current node, *a*, at it to properly link the element into the list. The problem comes when we go to the next line. NewNodePtr is "uninitialized". My partner and I were extremely confused. It was like the semicolon put us out of scope of that variable's declaration. Out best guess is that because we ended the previous statement, the garbage collector deleted our variable, even though we wanted to use it in the following line. I'm pretty sure LambdaFun doesn't have a garbage collector, but that was the best guess we had and the only word we could use to explain it. 

The way we finally figured out how to do it was by completely reassembling the *a* node and forcing it to point towards the new node. I would have code to explain it, but I'm pretty sure I'm not supposed to have answers to homework on here.