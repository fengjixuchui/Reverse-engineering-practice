#### Crackme name : Mexican
#### Language     : C/C++ 
#### Platform     : Windows
#### Difficulty   : Very easy

----

We can start by just plain executing the program from the CMD CLI, we get a message stating "try harder"

![cli running](https://raw.githubusercontent.com/x00pwn/reverse-engineering-practice/master/images/0-mexican.png)

----

Now let's load the executable file into IDA Pro, I will be using IDA Pro freeware for this.

![try harder](https://raw.githubusercontent.com/x00pwn/reverse-engineering-practice/master/images/3-mexican.png)

You can also see in the main function where it loads the aTryHarder variable and calls printf, which is the typical result of just plain executing the program normally. We can quickly analyze this function.

```assembly
.rdata:00404003 ; char aTryHarder[]
.rdata:00404003 aTryHarder      db 'try harder',0       ; DATA XREF: _main:loc_401653↑o
.rdata:0040400E                 align 10h
```
1. aTryHarder is the variable name
2. db indicates it's a double byte
3. 'try harder' is the message
4. the stack is also being aligned 10 bytes to accommodate for the length of the message string

This just shows us the very basic function that will print out the string 'try harder' when the program runs the main function by default.

----

![main function](https://raw.githubusercontent.com/x00pwn/reverse-engineering-practice/master/images/1-mexican.png)


Analyzing the main function in graph view shows the there is a function called Z4flagv being called, the function name includes "flag" in it, so there's a good chance this is what we are after. Let's analyze the assembly to understand what is happening.

![Z4flagv function](https://raw.githubusercontent.com/x00pwn/reverse-engineering-practice/master/images/2-mexican.png)

```assembly
.text:004015E4                 add     eax, 17h
.text:004015E7                 mov     byte ptr [eax], 33h
.text:004015EA                 mov     eax, [ebp+var_C]
.text:004015ED                 add     eax, 18h
.text:004015F0                 mov     byte ptr [eax], 72h
.text:004015F3                 mov     eax, [ebp+var_C]
.text:004015F6                 add     eax, 19h
.text:004015F9                 mov     byte ptr [eax], 72h
.text:004015FC                 mov     eax, [ebp+var_C]
.text:004015FF                 add     eax, 1Ah
.text:00401602                 mov     byte ptr [eax], 6Fh
.text:00401605                 mov     eax, [ebp+var_C]
.text:00401608                 add     eax, 1Bh
.text:0040160B                 mov     byte ptr [eax], 7Dh
.text:0040160E                 mov     eax, [ebp+var_C]
.text:00401611                 add     eax, 1Ch

```
I cut out of the majority of text above since the function is very redundant and repetitive. You can see a bunch of hex being moved into the EAX register, let's use some bash CLI magic to cut out all the hex characters.
`cat hex.txt | cut -d "," -f2 | grep "h" | cut -d "h" -f1` does the trick, it's dirty, but it works. I'm sure I could do this a LOT better, but this one-liner will extract all the hex characters from a raw dump of the function from IDA View-A. 
`666C61677B4D337831630A340B6E0C4D0D6C0E340F6C1077113412721333145F1570166C1733187219721A6F1B7D1C0A`

echoing the hex and piping it into `xxd -r -p` gives us the final flag.

#### flag{M3x1c4n14lw4r3_pl3rro}

Could this have been done more easily? I'm sure. But does this work? Yes.
