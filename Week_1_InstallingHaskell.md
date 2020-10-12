# Week 1: Installing Haskell and BNFC

## My System:
I am running two windows 10 machines. I have a desktop that I mainly use and a laptop that I need to keep up to date just in case we do go back to class or if I need to do homework away from home.

## Issues Installing Haskell:
I mentioned the fact that I'm on multiple machines because ensuring I keep them both synced up is incredibly important. If my desktop has Haskell installed but my laptop doesn't, it can cause serious problems when I need to test out my homework. 

I found installing haskell itself pretty simple. It should be an executable, but I guess command line worked mostly. I personally didn't run into any problems, but I know my friends ran into lots of problems while the Haskell install command was running. Cabal refused to install for them. We have not run into a situation where we needed it, but I do know that if we do need it, it could cause a lot of problems.

I think very few students have a favorite IDE at this point in their careers and Haskell doesn't have a standard IDE. Like how C# has Visual Studio and Java has Intellij. So I think it was very helpful for the professor to say how he uses Visual Studio Code as his IDE. The Haskell Extensions are very hard to get right since there are so many of them. I am <b>extremely</b> happy that he suggested Visual Studio Code rather than Atom. Atom is the worst "IDE" to use.


## Installing BNFC
There was very little instruction on how to install BNFC on a windows machine. I'm very thankful that I know my way around Windows 10. 

To install BNFC onto my machines I needed to add the .exe file to my System Path (a solution I'm certain very few people know about). The install page only has a download button for the .exe with no further instructions. Here are [instructions on how to add a folder to your System Path](https://www.c-sharpcorner.com/article/add-a-directory-to-path-environment-variable-in-windows-10/#:~:text=Add%20A%20Directory%20To%20A%20PATH%20Environment%20Variable,Variables%20window%20where%20you%20can%20see%20all%20variables) if you're curious.

Also, since I'm on windows, the Make command doesn't work. I've been trying to use the Windows Subsystem for Linux but it's performance is inconsistent at best. I've resorted to using my CentOS virtual machine I'm required to have for my Operating Systems class. That vm seems to work quite well.



## Summary
Installing Haskell is relatively easy as long as there are no hickups. If there are hickups, good luck.

Installing BNFC is something that really needs more instruction for people who are on Windows. 