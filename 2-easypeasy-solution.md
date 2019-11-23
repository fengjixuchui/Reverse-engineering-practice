#### Crackme name : Easy Peasy
#### Language : C/C++
#### Platform : Windows
#### Difficulty : Very easy

Pretty much the easiest crackme, it's a 64 bit binary file, viewing the main function just reveals the credentials for "logging into the program". Running the program and providing a random username terminates the program and gives us a taunting message.

![bad running](https://raw.githubusercontent.com/x00pwn/reverse-engineering-practice/master/images/1-easypeasy.png)

Viewing the decompiled version of the program purely just reveals the plaintext credentials to login...
![cli running](https://raw.githubusercontent.com/x00pwn/reverse-engineering-practice/master/images/2-easypeasy.png)

```
Username : iwonderhowitfeelstobeatimetraveler
Password : heyamyspaceboardisbrokencanyouhelpmefindit?
```


![good running](https://raw.githubusercontent.com/x00pwn/reverse-engineering-practice/master/images/0-easypeasy.png)

Now we can log in with the credentials.

Let's try and patch the application with a customized username and password now. Since it's way to easy.
