## Crackme name : Mexican
## Language     : C/C++ 
## Platform     : Windows
## Difficulty   : Very easy

We can start by loading the executable file into IDA pro, I will be using IDA freewre for this.

![main function](https://raw.githubusercontent.com/x00pwn/crackmes.one-solutions/master/images/1-mexican.png)

Analyzing the main function in graph view shows the there is a function called Z4flagv being called, the function name includes "flag" in it, so theres a good chance this is what we are after. Let's analyze the assembly to understand what is happening.

![Z4flagv function](https://raw.githubusercontent.com/x00pwn/crackmes.one-solutions/master/images/2-mexican.png)

