# Ackerman Function (ARS Exercises)

## Note:
This blog assumes you know what an ARS is and are familiar with them. Do not use this as a source for basic information on what an ARS is. 

This exercise can be found at [this link](https://hackmd.io/@alexhkurz/BJ23jmpIw) under the "Optional (but interesting)" title.

# What is the Ackermann Function?
According to Wikipedia, the Ackeramann Function is "one of the simplest and earliest-discovered examples of a total computable function that is not primitive recursive." I had no clue what that means, so I did some more digging. A primitive recursive function is a function that can be solved iteratively with a for loop in addition to recursively. So the Ackermann function was one of the first fully computable functions that is recursive and couldn't also be solved iteratively. So essentially its an algorithm that **must** be recursive.This function isn't used to compute anything meaningful or useful like an algorithm for physics, but it does have its purpose in the mathematical world.

The most common version of this function is called the Achermann-Peter function and only takes two arguments (rather than the three of the original function).

The function A is defined as: <br />
`A(0, n) = n + 1`<br />
`A(m + 1, 0) = A(m, 1)`<br />
`A(m + 1, n + 1) = A(m, A(m + 1, n))`<br />

This set of equations doesn't seem to bad at first glance. It's just a bunch of addition and if statements. If you actually attempt to compute it, with even small numbers, you will see that this task grows extremely quickly.

# Haskell Version:
So the goal of this blog is to show how different C# and haskell are when approaching this type of an algorithm. First, let's start with the Haskell version because it is far closer to the actual algorithm in terms of ease to type and syntax.

The function I'm calling ack is defined as <br />
`ack :: Int -> Int -> Int`<br />
`ack 0 n = n + 1`<br />
`ack m 0 = ack (m - 1) 1`<br />
`ack m n = ack (m-1) (ack (m) (n-1))`<br />

Start with running very small numbers through this. If you want it done within the hour, your numbers must be less than 10. 

These are my tests with the Haskell program:<br />
| M      | N | Output | Time |
| ----------- | ----------- | ----------- | ----------- |
| 1 | 2 | 4 | Instant |
| 2 | 3 | 9 | Instant |
| 3 | 4 | 125 | Nearly Instant | 
| 3 | 6 | 509 | Nearly Instant |
| 3 | 7 | 1021 | 0.25 seconds |  
| 3 | 8 | 2045 | 0.5 seconds | 
| 3 | 9 | 4093 | 5 seconds | 
| 4 | 5 | N/A | Over 3 minutes (didn't finish) |

I am doing these tests on my desktop PC with an Intel i7 5820k (6 core, 12 thread) overclocked to 4.0 GHz, so a very capable machine. This is important because that seemingly simple function is able to fully utilize a single core when I put in 4 and 5 as my arguments. I couldn't find a good way of timing those functions with Haskell code, so I just used a stopwatch on anything that wasn't essentially instant. 

There are certain things we can take away from this data, no matter how crude the timing methodoligy might be. We can see that the value for M has a much greater impact on the completion time than N. We can see that slowly incrementing N while keeping M at 3 creates an exponential increase in completion time and output. As we increase the value for N, we can see that the output value is <br />
`(2 * previous output) + 3 = new output` <br />
when M is 3. 





# C# Version
The C# version of this algorithm is a little more complicated to write, but potentially more intuitive to read, especially for someone who is used to imperative or C based languages. 

    public static int A(int m, int n)
    {
        if (m == 0)
        {
            return n + 1;
        }
        else if (n == 0)
        {
            return A(m - 1, 1);
        }
        else
        {
            return A(m - 1, A(m, n - 1));
        }
    }
    

This is a little bit more to write because C# doesn't support pattern matching and requires return statements, but it is essentially the same thing.


These are my tests with the C# program:<br />
| M      | N | Output | Time |
| ----------- | ----------- | ----------- | ----------- |
| 1 | 2 | 4 | Instant |
| 2 | 3 | 9 | Instant |
| 3 | 4 | 125 | Instant | 
| 3 | 6 | 509 | Instant |
| 3 | 7 | 1021 | Instant |  
| 3 | 8 | 2045 | 0.00002 seconds | 
| 3 | 9 | 4093 | 0.00010 seconds | 
| 4 | 5 | N/A | Failed (Stack Overflow) |


As we can see, the C# is far more efficient, but once it gets overwhelmed, it just crashes. 

# Conclusion
The Haskell version is far simpler to write because of Haskell's ability to handle pattern matching, but the C# is vastly more efficient. The Haskell is able to at least keep trying to compute the value even if its performance is crippled when it gets overloaded while the C# just chokes on it and crashes.