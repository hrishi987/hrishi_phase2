# 1. clutter-overflow

> Clutter, clutter everywhere and not a byte to use.

## Solution:
- read the source code, ran the program through nc connection but found out that giving `0xdeadbeef` as input wasnt working
- set executable perms for the chall file
- read abt `buffer overflow` and learnt that `gets` is vulnerable to it
- SIZE is set to 256 bytes in the clutter array, so input exceeding that should start the overflow, then we can write `0xdeadbeef` to code variable
- realised that `0xdeadbeef` must be entered in little endian bytes format as `\xef\xbe\xad\xde` after 256 A. So i tried pasting that together
- that gave me the output `code == 0x4141414141414141` so i found out that i entered too many A's or smthn. On further messing, i found that the limit is actually 264 bytes. this seems inefficient, so i tried creating a python code for this
- that worked successfully
```bash
What do you see?
code == 0xdeadbeef: how did that happen??
take a flag for your troubles
cat: flag.txt: No such file or directory
```

```py
import struct
print('A'*264+struct.pack('l',0xdeadbeef))
```
- piped it to nc connection command and got flag

## Flag:

```
picoCTF{c0ntr0ll3d_clutt3r_1n_my_buff3r}
```

## Concepts learnt:

- buffer overflow and gets is vulnerable to it
- using struct module in python to convert stuff to bytes



***

# 2. buffer overflow 0

> Let's start off simple, can you overflow the correct buffer? The program is available here. You can view source here.
Connect using:
nc saturn.picoctf.net 62857

## Solution:
- made nc connection and noticed it was a simple input program
- saw gets() being used in the program and since i alr know that gets can be exploited by buffer overflow, thought i had to do smthn with it
- then I read up and found out that strcopy() is also vulnerable
- in vuln() func, buf2 size is 16 so i thought of givin an input exceeding that. Got the flag

```bash
Input: AAAAAAAAAAAAAAAAAAAAA
picoCTF{ov3rfl0ws_ar3nt_that_bad_9f2364bc}
```

## Flag:

```
picoCTF{ov3rfl0ws_ar3nt_that_bad_9f2364bc}
```

## Concepts learnt:

- buffer overflow and strcpy is vulnerable to it




***

# 3. format string 0

> Can you use your knowledge of format strings to make the customers happy?
Download the binary here.
Download the source here.

## Solution:
- ran the exec file and it first showed 3 options to choose from, only `Gr%114d_Cheese` worked and on checkin the code, saw a relation and it made sense. It had a formatter %114d which increases the length of the string and thats whats asked in the question and the condition in the code.
```py
if (count > 2 * BUFSIZE) {
```
- in the second menu choice, only `Cla%sic_Che%s%steak` worked prolly cuz it exited out with error as no argument was passed for %s.
- ran the same in the netcat conn program and got flag

## Flag:

```
picoCTF{7h3_cu570m3r_15_n3v3r_SEGFAULT_c8362f05}
```

## Concepts learnt:

- format specifiers


## Resources:

- [format specifiers](https://www.geeksforgeeks.org/c/format-specifiers-in-c/)

***

