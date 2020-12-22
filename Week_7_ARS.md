# Abstract Reduction Systems (ARS)

## What is an ARS?
An abstract reduction system is a rewrite system that allows us to ask some of the more complex abstraction questions about rewrite systems. By definition, an ARS is a set A together with a relation → ⊆ A × A. At first glance, that means nothing to me either so don't worry, I'll expand upon it. As part of [his lecture notes](https://hackmd.io/@alexhkurz/BJfvFVK8v#Models-of-computation), he says "If there is no b ∈ A such that a → b then stop (and output a) else replace a by b and [repeat]". All this is saying is that if a rewrite rule exists that you are able to do, then do it until you cannot. These systems are written as (A,→). This definition is extremely vague an opens up the possiblity for a lot of annoying/useless/repetitive/etc systems, but we will explore different attributes of ARSs that ensure they can be easier to understand and more useful.

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

1. AA → A
2. BB → A
3. AB → B
4. BA → B


Answer the following questions: 
- What are the normal forms?
- Are normal forms unique?
- Is it confluent?
- Is it terminating?

Feel free to attempt these on your own before looking at my work below.

**My Work:**
I'm going to start with the input *ABBAABAB* (I just put a bunch of A's and B's in a randomizer).

First I will be trying to find a normal form for this string by just reducing as much as I can.

1. <span style="color:cyan">AB</span>BAABAB → <span style="color:cyan">B</span>BAABAB <br />
2. <span style="color:cyan">BB</span>AABAB → <span style="color:cyan">A</span>AABAB <br />
3. <span style="color:cyan">AA</span>ABAB → <span style="color:cyan">A</span>ABAB <br />
4. <span style="color:cyan">AA</span>BAB → <span style="color:cyan">A</span>BAB <br />
5. <span style="color:cyan">AB</span>AB → <span style="color:cyan">B</span>AB <br />
6. <span style="color:cyan">BA</span>B → <span style="color:cyan">B</span>B <br />
7. <span style="color:cyan">BB</span> → <span style="color:cyan">A</span> <br />

Unable to apply more rules, therefore I have found a normal form. The normal form of *ABBAABAB* is *A*. But we could have had basic predictions of that from just looking at the rules. The rules are slowly removing A's and B's as we apply them. The rules all require an input of 2 characters and reduce those 2 to 1 character. So we can predict that as we apply them, the system wil always reduce to a single A or B. This means that there are 2 normal forms: "A" and "B". 

Also, why did I apply those rules in that order? Can you find a more efficient order? At step 2, why did I apply BB → A instead of AB → B? There wasn't really a reason, I just felt like it would be easier to follow if I went left to right. But the fact that I could have done a couple different things at most of the steps shows that this ARS is confluent.

Now is this terminating? The fact that we found a normal form for "ABBAABAB" shows that it is terminating given that input, but can it guarantee termination? Yes. A giveaway is the fact that there is not a rule that undoes the work a different rule performs. If we added the rules "AB → BA" and "BA → AB", it would result in the ARS being non-terminating. Those rules would allow us to flip flop between AB and BA infinitely. No matter how dumb you'd have to be to just keep swapping those values, it doesn't change the fact that you **can**. 

I like to think of testing termination as if I write code to randomly apply these functions to a given input. The randomness is very important because it ignores common sense. It would be more than happy just infinitely applying both of those rules and there would be a real chance that that could happen. Very unlikely if you kept it running, but still possible. Since it's still possible, it cannot be terminating.