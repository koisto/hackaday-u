## Exercises

Spoiler alert. 


Solutions to excercises are shown below.


### c1
- Program checks the number of arguments is 2
- String length of password 'hackadayu' is stored
- Argument is compared with 'hackadayu' using strncmp

### c2
- Checks that the number of arguments is 2
- Prints message if arg2 is less than 5 (continues/jumps if greater than 4)
- Based on looking at assembly looks like the code then checks that one of the chars in the string is x68 and the other is x75 (h and u)
- Confirmed by switching to decompiler. First char needs to be 'h', fourth needs to be 'u'.

### c3
- Initially seems similar to the last program. Needs two arguments, second needs to be at least 5 chars.
- Looking at assembly listing seems to do something with 3rd and 4th chars (indexes 2 and 3)
- Looking at decompiler output looks as if index 3 is taken away from index 2 if result == 0x20 then we are in.
- x20 is the difference between lower case and upper case chars in ascii. So 11aA2 should work.

### c4
- Went straight to the decompiler, changed signature and renamed vars. Seems that it is looking for a password the same length as 'hackaday-u'. 
- Password could be 'hackaday-u' with each character incremented by 2: 'jcemcfc{/w'. It is!

### nasm_crack
- Because binary is produced from assembly presumably dissaembly will not be helpful.
- Because the binary hasn't been linked against the standard library there is only one function - called entry. You can see the system calls to write to stdout and read the password from stdin.
- The data section shows the prompt to the user and responses to the password along with the password itself.

### SimpleKeyGen
- Needs an argument of a given format.
- Changed signature for main, usage and checkSerial functions.
- checkSerial checks that string is 16 chars long and the first charater in each pair is 1 less than the previous. 'abcdef0123456789'

### skele
- Password needs to be the same length as 'skeletor'
- Password is 8 ^ 's', 9 ^ 'k', 10 ^ 'e' for the first 8 chars.
- Wrote some python in the repl to work this out

```
$ python
>>> chr(8 ^ ord('s'))
'{'
>>> chr(9 ^ ord('k'))
'b'
>>> chr(10 ^ ord('e'))
'o'
>>> chr(11 ^ ord('l'))
'g'
>>> chr(12 ^ ord('e'))
'i'
>>> chr(13 ^ ord('t'))
'y'
>>> chr(14 ^ ord('o'))
'a'
>>> chr(15 ^ ord('r'))
'}'
```

```
$ ./skele {bogiya}
Correct! You have the power!
```