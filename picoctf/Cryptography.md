# 1. Custom encryption

> Can you get sense of this code file and write the function that will decode the given encrypted file content.
Find the encrypted file here flag_info and code file might be good to analyze and get the flag.

## Solution:

- went through code file and started "reverse engineerin" the code to decrypt it.
- understood the `message` first undergoes XOR agnst a predefined key "trudeau". Then each char of this is converted to ascii value and multiplied by shared_key in `encrypt` function
- first i tried reversin the `encrypt` function to `decrypt` to return a text
- then inside the xor encryption function, i added a empty string `orig` to which each decrypted char will get appended to get it to decrypt
- i then ran the program with the same initial key and the cipher, a and b values provided in the `enc_flag` file.
- got the flag in reverse as output, put that in an online text reverser to get actual flag
```bash
hrishi@LAPTOP-AS47JO28:~/Cryptonite/hrishi_phase2/picoctf$ python3 main.py
}7950354e_d6tp0rc2d_motsuc{FTCocip
```


```python
def generator(g, x, p):
    return pow(g, x) % p

def decrypt(cipher, key):
    plaintext = ""
    for num in cipher:
        plaintext +=  chr(num// (key*311))
    return plaintext

def dynamic_xor_decrypt(plaintext, text_key):
    orig = ""
    key_length = len(text_key)
    for i, char in enumerate(plaintext) :
        key_char = text_key[i % key_length]
        
        decrypted_char = chr(ord(char) ^ ord(key_char))
        orig += decrypted_char
    return orig
p = 97
g = 31

cipher = [151146, 1158786, 1276344, 1360314, 1427490, 1377108, 1074816, 1074816, 386262, 705348, 0, 1393902, 352674, 83970, 1141992, 0, 369468, 1444284, 16794, 1041228, 403056, 453438, 100764, 100764, 285498, 100764, 436644, 856494, 537408, 822906, 436644, 117558, 201528, 285498]
a = 97
b = 22
u = generator(g, a, p)
v = generator(g, b, p)
key = generator(v, a, p)
print(dynamic_xor_decrypt(decrypt(cipher,key), "trudeau"))


```

## Flag:

```
picoCTF{custom_d2cr0pt6d_e4530597}
```

## Concepts learnt:

- reversing an algorithm by readin and analysing python code

## Resources:

- [Diffie-Hellman key exhchange alg](https://www.youtube.com/watch?v=NmM9HA2MQGI)


***

# 2. miniRSA

> Let's decrypt this: ciphertext? Something seems a bit small.

## Solution:

- tried using an online rsa decoder using the values provided in ciphertext file.


## Flag:

```
picoCTF{n33d_a_lArg3r_e_ccaa7776}
```

## Concepts learnt:

- rsa decoding
## Resources:

- [decoder](https://www.dcode.fr/rsa-cipher)


***



