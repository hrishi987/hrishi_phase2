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

# 3. rsa_oracle

> Can you abuse the oracle?
An attacker was able to intercept communications between a bank and a fintech company. They managed to get the message (ciphertext) and the password that was used to encrypt the message.
After some intensive reconassainance they found out that the bank has an oracle that was used to encrypt the password and can be found here nc titan.picoctf.net 51847. Decrypt the password and use it to decrypt the message. The oracle can decrypt anything except the password.

## Solution:

- tried decrypting the password directly using the program but that wasnt allowed.
- read up on RSA encryption to understand how it works. Essentially if C = E(m1) is the encrypted m1 msg, then E(m1) . `E(m2) = m1 ^e mod n . m2 ^e mod n = E(m1.m2)`
- creatin a custom python script to do this:
```py
pwd = 2336150584734702647514724021470643922433811330098144930425575029773908475892259185520495303353109615046654428965662643241365308392679139063000973730368839
rand = int(input("Custom encrypted msg : "))
c = pwd*rand
print(f"Msg to decrypt : {c}")
m2 = int(input("Enter decrypted text as hex: "), 16)  

orig = m2 // ord(bytes('a',"utf-8"))
m = orig.to_bytes(len(str(orig)), "big").decode("utf-8").lstrip("\x00")
print(m)

```
- got this output `60f50` . Used openssl to get the flag from secret.enc
```bash
hrishi@LAPTOP-AS47JO28:~/Cryptonite/hrishi_phase2/picoctf$ openssl enc -aes-256-cbc -d -in secret.enc -pass pass:60f50
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
picoCTF{su((3ss_(r@ck1ng_r3@_60f50766}
```


## Flag:

```
picoCTF{su((3ss_(r@ck1ng_r3@_60f50766}
```

## Concepts learnt:

- rsa decoding
## Resources:

- [RSA](https://www.geeksforgeeks.org/computer-networks/rsa-algorithm-cryptography/)


***



