# 1. m00nwalk

> Decode this message from the moon.

## Solution:

- viewed hint 1 "how did the images get sent back to earth from moon". This gave an idea of using sstv audio decoder
- Got the flag img after decoding the audio
- ![alt text](screenshots/moonwalk.png "screenshot")


## Flag:

```
picoCTF{beep_boop_im_in_space}
```

## Concepts learnt:

- existence of SSTV

## Resources:

- [decoder](https://sstv-decoder.mathieurenaud.fr/)


***

# 2. Trivial Flag Transfer Protocol

> Figure out how they moved the flag.

## Solution:

- used wireshark export objects to get a bunch of files from the pcap
- it had three picture?.bmp files and a program.deb file, along with plan and instructions files which had gibberish
- decoder the gibberish in instructions.txt using online decoder to get `"TFTP DOESNT ENCRYPT OUR TRAFFICS .WE MUST DISGUISE OUR FLAG TRANSFER . FIGURE OUT A WAY TO HIDE THE FLAG AND I WILL CHECK BACK FOR THE PLAN"`
- decoded the text in `plan` file to get `"I USED THE PROGRAM AND HID IT WITH - DUED I LIG EN CE. CHECKOUT THE PHOTOS"`
- used steghide to extract data from the pictures using command `steghide extract -sf picture?.bmp` for all pictures
- got stuck on the passphrase for a while and then figured out it was DUEDILIGENCE as given in the txt file
- got flag.txt from picture3.bmp


## Flag:

```
picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}
```

## Concepts learnt:

- steghide command
- convenient online decoder
- working with wireshark and pcap files

## Resources:

- [decoder](https://www.cachesleuth.com/multidecoder/)


***


