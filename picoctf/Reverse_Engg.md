# 1. GDB baby step 1

> Can you figure out what is in the eax register at the end of the main function? Put your answer in the picoCTF flag format: picoCTF{n} where n is the contents of the eax register in the decimal number base. If the answer was 0x11 your flag would be picoCTF{17}.
Disassemble this.

## Solution:

- ran gdb on the file as suggested
- read upon gdb commands and used `disassemble main`, found that a hexadecimal value was sent to `eax` register
- got the decimal number from the hexadecimal value `0x86342`

```bash
(gdb) disassemble main
Dump of assembler code for function main:
   0x0000000000001129 <+0>:     endbr64
   0x000000000000112d <+4>:     push   %rbp
   0x000000000000112e <+5>:     mov    %rsp,%rbp
   0x0000000000001131 <+8>:     mov    %edi,-0x4(%rbp)
   0x0000000000001134 <+11>:    mov    %rsi,-0x10(%rbp)
   0x0000000000001138 <+15>:    mov    $0x86342,%eax
   0x000000000000113d <+20>:    pop    %rbp
   0x000000000000113e <+21>:    ret
End of assembler dump.
```

## Flag:

```
picoCTF{549698}
```

## Concepts learnt:

- learned to kinda use the gdb debugger


## Resources:

- [GDB info site](https://ctf101.org/reverse-engineering/what-is-gdb/)


***

# 2. vault-door-3

> This vault uses for-loops and byte arrays. The source code for this vault is here: VaultDoor3.java

## Solution:

- went through the code and realised the jumbled flag was given. All i had to do was run the checkPassword code agn with the jumbled flag

```java
class Main {
    public static void main(String[] args) {
        String password = "jU5t_a_sna_3lpm18gb41_u_4_mfr340";
        char[] buffer = new char[32];
        int i;
        for (i=0; i<8; i++) {
            buffer[i] = password.charAt(i);
        }
        for (; i<16; i++) {
            buffer[i] = password.charAt(23-i);
        }
        for (; i<32; i+=2) {
            buffer[i] = password.charAt(46-i);
        }
        for (i=31; i>=17; i-=2) {
            buffer[i] = password.charAt(i);
        }
        String s = new String(buffer);
        System.out.println(s);
    
    }
}
```

## Flag:

```
picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_1fb380}
```



***

# 3. ARMssembly 1

> For what argument does this program print `win` with variables 85, 6 and 3? File: chall_1.S Flag format: picoCTF{XXXXXXXX} -> (hex, lowercase, no 0x, and 32 bits. ex. 5614267 would be picoCTF{0055aabb})


## Solution:

- used `file` command on the file and understood that it contains `assembler source ASCII text`


```
put codes & terminal outputs here using triple backticks

you may also use ```python for python codes for example
```

## Flag:

```
picoCTF{}

```

## Concepts learnt:

- 



***