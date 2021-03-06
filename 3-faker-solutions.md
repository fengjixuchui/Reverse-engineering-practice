#### Faker challenge -  400 points
#### Taken from TUCTF

This past weekend I participated in TUCTF, I was finally able to utilize some of the basics reverse engineering skills I have studied over the past few weeks. This challenge is called "faker", and it can be solved with a very clean and simple patch that I to call a hidden flag function which I utilized to get the flag for this CTF.

We can start by running the binary, we are presented with 4 options, 3 of which print out a fake flag, hence the challenge name and the 4th option exits the program. 

![program options](https://raw.githubusercontent.com/x00pwn/reverse-engineering-practice/master/images/0-faker.png)

----

We can open up the challenge in IDA pro and examine the internals of the program.

![main function](https://raw.githubusercontent.com/x00pwn/reverse-engineering-practice/master/images/1-faker.png)

We can analyze the main function and we see a couple of other interesting functions. 

![functions](https://raw.githubusercontent.com/x00pwn/reverse-engineering-practice/master/images/4-faker.png)

1. To start, the function `printFlag` function is responsible for printing and decrypting the flags (fake and real)
2. The function `printmenu` is responsible for printing the various options on the main menu.
3. There are also three functions `A`, `B`, and `C` which are all responsible for printing out the fake flags. 
4. The most important function is the `thisone` function which is not called by default and contains the real flag.


And within each flag function there is a comment with encrypted text. Assuming that encrypted text is the flag, which based on the lengths of the fake flags, we can assume it indeed is.

![fake function encrypted flag](https://raw.githubusercontent.com/x00pwn/reverse-engineering-practice/master/images/2-faker.png)

The `thisone` function looks like it's also holding encrypted text, assuming that encrypted text is the flag, we can assume this function would print the real challenge flag. 

`"\\PJ\\fC|)L0LTw@Yt@;Twmq0Lw|qw@w2$a@0;w"...` is the encrypted real flag from the "thisone" function.

#### Winning

We can simply redirect the call to one of the fake flag printing functions to point to the real flag function, so when we try to use a fake flag function, it prints the real flag. Let's get patching. 

I will be targeting the `call C` within the `loc_1506:` function, instead of calling "C" we will have it call the `thisone` function. Simply select `call C` and do Edit > Patch program > Assemble Instruction, and change `C` to `thisone`. 

![patching](https://raw.githubusercontent.com/x00pwn/reverse-engineering-practice/master/images/3-faker.png)

Then apply the patches to the current binary. Now run the patched binary and selected the "Flag C" option to call the new function to get the real flag.

![pwned](https://raw.githubusercontent.com/x00pwn/reverse-engineering-practice/master/images/5-faker.png)

`TUCTF{7h3r35_4lw4y5_m0r3_70_4_b1n4ry_7h4n_m3375_7h3_d3bu663r}`

![won](https://raw.githubusercontent.com/x00pwn/reverse-engineering-practice/master/images/6-faker.png)
