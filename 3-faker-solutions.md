#### Take from TUCTF

This past weekend I participated in TUCTF, I was finally able to utilize some of the basics reverse engineering skills I have studied over the past few weeks. This challenge is called "faker", and it can be solved with a very clean and simple patch that I personally used to get the flag for the CTF.

We can start by running the binary, we are presented with 4 options, 3 of which print out a fake flag, hence the challenge name, and the 4th option exits the program. 

We can open up the challenge in IDA pro and examine the programs internals.


We can analyze the main function and we see a couple intresting function, to start, the function **printmenu** is responsible for printing the various options, there are also three functions "A", "B", and "C" which are all responsible for printing out the fake flags, and within each function there is a comment with encrypted text. Assuming that encrypted text is the flag, which based on the lengths of the fake flags, we can assume it indeed is.
