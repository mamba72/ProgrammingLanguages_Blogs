# What even is Hoare Logic?
Well... we don't really need to know what it is entirely. We are more interested in how it pertains to loops. While loops in particular. Hoare logic is all about "contractual programming" which is where a function promises an output if given correct input. This might be an over simplification, but think of it as a division function. Given the correct input, the function will always divide the two numbers, but if the user does not satisfy that condition, like dividing by zero, the function will not be able to promise a consistent output. 

This is very important to while loops because if a user gives improper inputs, it could create an infinite loop. So for the purposes of this class, Dr. Kurz suggested the title of "Correctness of While Programs."

# Correctness of While Programs (Loops)

## Definitions
Before we continue, we need to define three terms. These three things are the whole basis for the correctness of while loops.
- **Preconditions:**
    - The conditions required from the user to guarantee correct performance.
- **Postconditions:**
    - The conditions the function/loop/program is guaranteeing to the user.
- **Invariants:**
    - This has been defined in previous lectures, but they are still important nad have a different effect here. Invariants that are guaranteed to hold after the execution if they held before the execution. 

## Examples
I think this concept is far easier to learn by doing examples rather than talking theory because it is really more application than theory.

This is the example from the [lecture notes](https://hackmd.io/Df57tnuCSGaW8wqqsl57FQ#Example):

```
while(x!=0) do z := z + y; x := x-1 done
```

So for me, I didn't really understand what this was saying, so if it helps, this is a C# version
```
int x, y, z //these are parameters of a function
while (x!=0) 
{
    z = z + y;
    x = x + 1;
}
```

Lets walk through this program and list the values of x,y, and z for every iteration. Let's start with x = 5, y = 2, and z = 0 just to test it out.

| X | Y | Z |
| ----------- | ----------- | ----------- |
| 5 | 2 | 0 |
| 4 | 2 | 2 |
| 3 | 2 | 4 |
| 2 | 2 | 6 |
| 1 | 2 | 8 |
| 0 | 2 | 10 |

So after doing the calculations, we see that x=0, y=2, z=10. 

Do you see any invariants? (Some relations between the input and the output)

Immediately, I see that an invariant is y=2. Y does not change throughout this entire program.

This one is harder to spot, but the initial values for x and y multiply to be the final value for z. As it turns out, `X * Y = Z` is almost an invariant. We have to add one thing. What if z didnt start at 0? Then our final invariant would be `x*y+z`. 

Our two invariants:
- X * Y + Z will result in a constant value throughout computation.
- Y will always be constant throughout computation.


So we determined the invariants of the example, but what about the pre and post conditions? 

I think the best way to look at determining preconditions is by asking myself "how can I break it?". What values will break this while loop? When I say break, I don't mean throw an error, because have X = "Stephen" would obviously break it. I mean what can send that while into an infinite while? 

The condition within that while loop is X != 0 and within that loop we are decrementing X with each iteration. So any number that can be decremented to equal zero will operate correctly. That means any negative number will never decrement to 0. So a precondition would be that X must be greater than or equal to 0.

What about a postcondition? Our post condition could be how the original value for X, call it X0, multiplied by the original value of Y, call it Y0, plus the original value for Z, call it Z0, is equal to our final value for Z, call it ZF. Written in math notation, ZF = Y0 * X0 + Z0 is our postcondition.

The proper way to write that is as follows:

<span style="color:gold">{ X > 0 ∧ X = X0 ∧ Z = Z0 ∧ Y = Y0 }</span> while (x != 0) do z := z + y; x := x - 1 done <span style="color:gold">{ Z = Z0 + X0 * Y0 }</span>

