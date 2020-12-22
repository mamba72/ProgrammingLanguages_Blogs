# Abstract Reduction Systems (ARS)

## What is an ARS?
An abstract reduction system is a rewrite system that allows us to ask some of the more complex abstraction questions about rewrite systems. By definition, an ARS is a set A together with a realtion → ⊆ A × A. At first glance, that means nothing to me either so don't worry, I'll expand upon it. As part of [his lecture notes](https://hackmd.io/@alexhkurz/BJfvFVK8v#Models-of-computation), he says "If there is no b ∈ A such that a → b then stop (and output a) else replace a by b and [repeat]". All this is saying is that if a rewrite rule exists that you are able to do, then do it until you cannot. These systems are written as (A,→). This definition is extremely vague an opens up the possiblity for a lot of annoying/useless/repetitive/etc systems, but we will explore different attributes of ARSs that ensure they can be easier to understand and more useful.

## Important Attributes and Defintions of an ARS
1. **Normal Form**: One of the most important aspects of an ARS is whether it reaches a normal from. We have already covered normal forms, but specifically partaining to an ARS, a normal form is a position in the process of reduction where  there is no (a, b) ∈ →, or, if there is no a → b. This essentially means that if you cannot apply one of the rewrite rules, then you have reached a normal form.

2. **Joinable**:
    - [Kurz's Definition](https://hackmd.io/@alexhkurz/r1hRZaG8v#Definitions): "a,b are *joinable*, written as a↓b, if both a and b reduce to the same element. In symbols, a↓b if there is x∈A such that a ∗⟶ x and b ∗⟶ x." (∗⟶ means "reduces to" and the star allows for many steps to be in between).

    - What this is saying is that if two different sequences are able to be reduced to the same output, then those original sequences are joinable. This might seem simple, but it is very important for the next definition. 

3. **Confluent**:
    - [Kurz's Definition](https://hackmd.io/@alexhkurz/r1hRZaG8v#Definitions): "(A,→) is confluent if whenever *x* reduces to *y* and *z*, then *y* and *z* are joinable."

    -  What that's saying is that if there are multiple paths to follow or you have more than one option when reducing, then the ARS is considered to be confluent. This is essentially saying that there is more than one way to "solve" the ARS, allowing you to take many paths.

4. **Terminating**:
    - [Kurz's Definition](https://hackmd.io/@alexhkurz/r1hRZaG8v#Definitions): "(A,→) is terminating if there is no infinite chain a0 → a1 → …"

    - This essentially means that if you are not flip flopping between two different rules, then it is terminating. But this is not as simple as it sounds. If an ARS is terminating, it must guarantee that it is terminating regardless of the input. So if you happen to find an input that terminates, and an another that doesn't you cannot guarantee that the ARS terminates; therefore, it is not terminating.

## An Example:
Rewrite Rules (from [here](https://hackmd.io/@alexhkurz/BJfvFVK8v#Examples-and-Exercises)):
```
AA → A
BB → A
AB → B
BA → B
```

Answer the following questions: 
- What are the normal forms?
- Are normal forms unique?
- Is it confluent?
- Is it terminating?

Feel free to attempt these on your own before looking at my work below.

**My Work:**
I'm going to start with the input *ABBAABAB* (I just put a bunch of A's and B's in a randomizer).

First I will be trying to find a normal form for this string by just reducing as much as I can.
```
ABBAABAB → <span style="color:red">word</span>
```