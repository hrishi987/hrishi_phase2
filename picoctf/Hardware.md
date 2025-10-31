# 1. iq test

> let your input x = 30478191278.

wrap your answer with nite{ } for the flag.

As an example, entering x = 34359738368 gives (y0, ..., y11), so the flag would be nite{010000000011}.

## Solution:
- got stuck for quite some time on how to begin as with logic gates, i was normally used to givin binary input, then thought of converting given x value to binary online. got 36 digit binary `011100011000101001000100101010101110`
- had to manually workout the logic gate given with this input with positions x0-x35
- ![alt text](screenshots/iqtest.png "circuit-solved")

## Flag:

```
nite{100010011000}
```

## Concepts learnt:

- revised logic gates



***

# 2. bare-metal-alchemist

> my friend recommended me this anime but i think i've heard a wrong name.


## Solution:
- ran `file ` command on the firmware.elf and found that its `ELF 32-bit LSB executable, Atmel AVR 8-bit`. Found that its an executable for AVR microcontrollers
- tried to reverse engineer the file
- used avr bin utils and found multiple `EOR`s and on searching found out that XOR seem to have been used
- tried a pythons script which goes through the file bytes, iterates through 1-200 to get random key and decode the XOR
- searched manually for flag like ASCII by saving the dump in file.txt and searching "CTF{" and got flag
```py
byt = open("firmware.elf", "rb").read()

for key in range(1, 200):
    decoded = bytes(x ^ key for x in byt)
    print(decoded)
```

## Flag:

```
TFCCTF{Th1s_1s_som3_s1mpl3_4rdu1no_f1rmw4re}
```

## Concepts learnt:

- rev engg practise
- workin with XOR



***

# 3. i_like_logic

> i like logic and i like files, apparently, they have something in common, what should my next step be.



## Solution:
- searched up abt .sal file extension and found out that its a  `Saleae Logic 2 Capture Format file for digital signal data`
- ran strings on a digital.bin file and saw the code `<SALEAE>` too. Read up on sal files Found a software to download to analyse this called `Logic 2`
- used the analyzer tool there for channel 3 and got this in btwn a bunch of text 

## Flag:

```
FCSC{b1dee4eeadf6c4e60aeb142b0b486344e64b12b40d1046de95c89ba5e23a9925}
```

## Concepts learnt:

- learned abt .sal files and LOGIC 2 software

## Resources:

- [LOGIC 2](https://support.saleae.com/product/getting-started/record)
- [more readin](https://file.org/extension/sal)



***


