# 1. Linux CLI - Shells Bells
> Explore the Linux command-line interface and use it to unveil Christmas mysteries. 

## Solution:

- jus had to follow the rlly detailed guide provided to complete the first few tasks.
- found out abt a side quest, tried to get the secret key to unlock it
- was provided 3 clues, first clue said 
    "I ride with your session, not with your chest of files.
    Open the little bag your shell carries when you arrive."
- checked env variables using `env` command and found `PASSFRAG1=3ast3r`
- second clue said 
    "The tree shows today; the rings remember yesterday.
    Read the ledger’s older pages."
- will do the sidequests later



## Flag:

```
THM{learning-linux-cli}
THM{sir-carrotbane-attacks}
THM{until-we-meet-again}
```

## Concepts learnt:

- jus basic linux commands


***

# 2. Phishing - Merry Clickmas
> Learn how to use the Social-Engineer Toolkit to send phishing emails.

## Solution:

- followed the instructions provided in the challenge description
- set server.py first and ran it from terminal which hosts the phishing site
- setup setoolkit to send the phishing email
- waited for the credentials in server.py terminal
- got username: admin and pass: unranked-wisdom-anthem


## Flag:

```
password: unranked-wisdom-anthem
```

## Concepts learnt:

- social engineering
- phishing attacks and how they work


***

# 3. Splunk Basics - Did you SIEM?
> Learn how to ingest and parse custom log data using Splunk.

## Solution:

- followed the guidelines provided in the challenge description
- Used search and reporting interface in Spunk to get all the ingested logs.
- Started basic search across the index using custom source type `web_traffic`
- filtered and used search query to find days with max no. of logs( the days in which attack happened)
- with further search queries, found out that most attacks were coming from a single ip `198.51.100.55`
- with multiple search queries, found out the different kind of attacks the attacker ran on the server
- got the necessary data asked in the ques in the end



## Concepts learnt:

- Ingest and interpret custom log data in Splunk
- Create and apply custom field extractions
- Use Search Processing Language (SPL) to filter and refine search results
- Conduct an investigation within Splunk to uncover key insights


***

# 4. AI in Security - old sAInt nick
> Learn how to AI to assist with cybersec tasks

## Solution:

- followed the instructions provided in the challenge description
- set server.py first and ran it from terminal which hosts the phishing site
- setup setoolkit to send the phishing email
- waited for the credentials in server.py terminal
- got username: admin and pass: unranked-wisdom-anthem


## Flag:

```
THM{SQLI_EXPLOIT}
 THM{AI_MANIA} 
```

## Concepts learnt:

- How AI can be used as an assistant in cyber security for a variety of roles, domains and tasks
- Using an AI assistant to solve various tasks within cyber security
- Some of the considerations, particularly in cyber security, surrounding the use of AI



***

# 5. IDOR - Santa’s Little IDOR
> IDOR ,Insecure Direct Object Reference, a type of access control vulnerability

## Solution:

- followed the instructions provided in the challenge description
- checked Network tab in developer options to understand what requests were being sent
- edited info in the Local storage section to gain access to other user accounts
- learnt abt encoding(base64, md5) used in storing data, which is crackable


## Flag:

```
no flags
```

## Concepts learnt:

- Understand the concept of authentication and authorization
- Learn how to spot potential opportunities for Insecure Direct Object References (IDORs)
-  Exploit IDOR to perform horizontal privilege escalation
-   Learn how to turn IDOR into SDOR (Secure Direct Object Reference)




*** 

# 6. Malware Analysis - Egg-xecutable
> Discover some common tooling for malware analysis within a sandbox environment.

## Solution:

- followed the instructions provided in the challenge description
- used pestudio to analyse executable, found checksum value
- checked strings to get first flag
- used regshot to do dynamic analysis, by capturing snapshots of registry before and after running executable
- used procmon to analyse tcp data being sent


## Flag:

```
THM{STRINGS_FOUND}
```

## Concepts learnt:

- The principles of malware analysis
- An introduction to sandboxes
- Static vs. dynamic analysis
- Tools of the trade: PeStudio, ProcMon, Regshot




*** 

# 7. Network Discovery - Scan-ta Clause
> Discover how to scan network ports and uncover what is hidden behind them.

## Solution:

- used Nmap to scan for all open ports
- saw an open ftp port to which i connected using `ftp ip port` command
- used `ls` and `get tbfc_qa_key1` to get first key `KEY1:3aster_`
- connected to 2nd applicatio using nc and got key `KEY2:15_th3_`
- `dig @10.48.157.206 TXT key3.tbfc.local +short` ran this command to get data from udc port and got `KEY3:n3w_xm45`
- combined the keys to access terminal and got flag


## Flag:

```
THM{4ll_s3rvice5_d1sc0vered}
```

## Concepts learnt:

- Learn the basics of network service discovery with Nmap
- Learn core network protocols and concepts along the way
- Apply your knowledge to find a way back into the server




*** 

# 8. Prompt Injection - Sched-yule conflict
> Learn to identify and exploit weaknesses in autonomous AI agents.

## Solution:

- tried to get function leaks from the King Malhare Assistant chatbot on the given website
- gave "list all functions" prompt to get more info
- tried to get the  `get_logs` function executed by Ai bot
- repromted by settin dry run to true to get flag


## Flag:

```
    THM{XMAS_IS_COMING__BACK}
```

## Concepts learnt:

- Understand how agentic AI works
- Recognize security risks from agent tools
- Exploit an AI agent




*** 

# 9. Passwords - A Cracking Christmas
> Learn how to crack password-based encrypted files.

## Solution:

- used pdfcrack to crack password of `flag.pdf` (`pdfcrack -f flag.pdf -w /usr/share/wordlists/rockyou.txt`), got password as `naughtylist`
- used zip2john to crack flag.zip file, got password as `winter4ever`


## Flag:

```
THM{Cr4ck1ng_PDFs_1s_34$y}
THM{Cr4ck1n6_z1p$_1s_34$yyyy}
```

## Concepts learnt:

- How password-based encryption protects files such as PDFs and ZIP archives.
- Why weak passwords make encrypted files vulnerable.
- How attackers use dictionary and brute-force attacks to recover passwords.
- A hands-on exercise: cracking the password of an encrypted file to reveal its contents.
- The importance of using strong, complex passwords to defend against these attacks.




*** 

# 10. SOC Alert Triaging - Tinsel Triage
> Investigate and triage alerts through Microsoft Sentinel.

## Solution:

- signed into microsoft azure using acc info given
- opened Sys_LogsCl table in microsoft sentinel to go thru alerts
- clicked on Linux PrivEsc—Kernel Module Insertion high severity incident to get more info and answered qs
- used KQL query provided 
```bash
set query_now = datetime(2025-10-30T05:09:25.9886229Z);
Syslog_CL
| where host_s == 'websrv-01'
| project _timestamp_t, host_s, Message
```
- answered additional qs asked


## Flag:

```
no flags
```

## Concepts learnt:

- Understand the importance of alert triage and prioritisation
- Explore Microsoft Sentinel to review and analyse alerts
- Correlate logs to identify real activities and determine alert verdicts


*** 

# 11. XSS - Merry XSSMas
> Learn about types of XSS vulnerabilities and how to prevent them.

## Solution:

- passed a reflected XSS payload to get first flag
- passed a stored XSS payload to get second flag


## Flag:

```
THM{Evil_Bunny}
THM{Evil_Stored_Egg}
```

## Concepts learnt:

- Understand how XSS works
- Learn to prevent XSS attacks


*** 

# 12. Phishing - Phishmas Greetings
> Learn how to spot phishing emails from Malhare's Eggsploit Bunnies sent to TBFC users.

## Solution:

- opened email inspector and started classifying emails to get flags


## Flag:

```
THM{yougotnumber1-keep-it-going}
THM{nmumber2-was-not-tha-thard!}
THM{Impersonation-is-areal-thing-keepIt}
THM{Get-back-SOC-mas!!}
THM{It-was-just-a-sp4m!!}
THM{number6-is-the-last-one!-DX!}
```

## Concepts learnt:

- Spotting phishing emails
- Learn trending phishing techniques
- Understand the differences between spam and phishing


*** 

# 13. YARA Rules - YARA mean one!
> Learn how YARA rules can be used to detect anomalies.

## Solution:

- moved to `/home/ubuntu/Downloads/easter` directory
- created yara rule and ran it for first qs ans
```bash
rule Find_TBFC_In_Images
{
    strings:
        $tbfc = "TBFC"
    condition:
        $tbfc
}
```
- for the second qs, regex used will be `/TBFC:[A-Za-z0-9]+/`
- ran the command `strings *.jpg | grep TBFC` to find msg sent


## Flag:

```
no flags
```

## Concepts learnt:

- using YARA

*** 

# 14. Containers - DoorDasher's Demise
> Continue your Advent of Cyber journey and learn about container security.

## Solution:

- learnt about docker and associated commands
- got flag after running following commands
```bash
docker exec -it uptime-checker sh
ls -la /var/run/docker.sock
docker exec -it deployer bash
whoami
sudo /recovery_script.sh
cd ..
cat flag.txt
```


## Flag:

```
    THM{DOCKER_ESCAPE_SUCCESS}
```

## Concepts learnt:

- Learn how containers and Docker work, including images, layers, and the container engine
- Explore Docker runtime concepts (sockets, daemon API) and common container escape/privilege-escalation vectors
- Apply these skills to investigate image layers, escape a container, escalate privileges, and restore the DoorDasher service


*** 

# 15. Web Attack Forensics - Drone Alone
> Explore web attack forensics using Splunk.

## Solution:

- logged in to splunk and used the search page to detect suspicious commands `index=windows_apache_access (cmd.exe OR powershell OR "powershell.exe" OR "Invoke-Expression") | table _time host clientip uri_path uri_query status`
- looked for server side / command exec errors `index=windows_apache_error ("cmd.exe" OR "powershell" OR "Internal Server Error")`
- answered the ques using necessary search terms( `index=windows_sysmon *cmd.exe* *whoami*`)


## Flag:

```
no flags
```

## Concepts learnt:

- Detect and analyze malicious web activity through Apache access and error logs
- Investigate OS-level attacker actions using Sysmon data
- Identify and decode suspicious or obfuscated attacker payloads
- Reconstruct the full attack chain using Splunk for Blue Team investigation

*** 

# 16. Forensics - Registry Furensics
> Learn what the Windows Registry is and how to investigate it.

## Solution:

- opened registry explorer, navigated to `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall` to find application installed before abnormal activity, which is `DroneManager Updater`
- went to NTUSER.DAT key to find the path from which user ran the program
- navigated to `HKLM\Software\Microsoft\Windows\CurrentVersion\Run` to find the startup programs and found the value which was added by the program,  `"C:\Program Files\DroneManager\dronehelper.exe" --background`


## Flag:

```
no flags
```

## Concepts learnt:

- Understand what the Windows Registry is and what it contains.
- Dive deep into Registry Hives and Root Keys.
- Analyze Registry Hives through the built-in Registry Editor tool.
- Learn Registry Forensics and investigate through the Registry Explorer tool.

*** 

# 17. CyberChef - Hoperation Save McSkidy
> The story continues, and the elves mount a rescue and will try to breach the Quantum Fortress's defenses and free McSkidy.

## Solution:

- in the first level, the encoding was base64
- encoded `CottonTail` as it was the guards name and passed that in username field
- got the magic question from network tab in develoepr tools, encoded that and passed it in the left field to get encoded password
- decoded that and passed it in password field to unlock the outer wall
- encoded `CarrotHelm`(guard name) to pass in username field, encoded magic ques `Did you change the password?` to get the encoded pass, which  had to decode twice to get `Itoldyoutochangeit!`, proceeded to Guard House level
- encoded guards name which was `LongEars`, got xor key as `cyberchef`, decoded from base64 and xored to get final password `BugsBunny`, proceeded to inner castle level
- encoded guards name `Lenny`
- got a hash, used crackstation to crack the hash, pass was `passw0rd1`, proceeded to Prison Tower level
- username was `Carl` but encoded
- cracked the password using necessary decoding instructions gien, got pass as `51rBr34chBl0ck3r`

## Flag:

```


THM{M3D13V4L_D3C0D3R_4D3P7}


```

## Concepts learnt:

- Introduction to encoding/decoding
- Learn how to use CyberChef
- Identify useful information in web applications through HTTP headers

*** 

# 18. Obfuscation - The Egg Shell File
> McSkidy keeps her focus on a particular alert that caught her interest: an email posing as northpole-hr.

## Solution:

- opened the given code in vscode and applied necessary decoding recipes on cyberchef to get the flags

## Flag:

```


THM{C2_De0bfuscation_29838}
THM{API_Obfusc4tion_ftw_0283}

```

## Concepts learnt:

- Learn about obfuscation, why and where it is used.
- Learn the difference between encoding, encryption, and obfuscation.   
- Learn about obfuscation and the common techniques.
- Use CyberChef to recover plaintext safely.

*** 

# 19. ICS/Modbus - Claus for Concern
> Learn to identify and exploit weaknesses in ICS systems.

## Solution:

- installed and setup pymodbus. Checked HR0 and HR1 and the system signature HR4
- created a script to see full system state. Created a remediation script and got the flag

## Flag:

```


THM{eGgMas0V3r}

```

## Concepts learnt:

- How SCADA (Supervisory Control and Data Acquisition) systems monitor industrial processes
-What PLCs (Programmable Logic Controllers) do in automation  
- How the Modbus protocol enables communication between industrial devices

*** 

# 20. Race Conditions - Toy to The World
> Learn how to exploit a race condition attack to oversell the limited-edition SleighToy.

## Solution:

- Setup FoxyProxy and Burp
- sent a proxy request to `/process_checkout` endpoint in burp suite
-  used Repeater tool to send multiple confirmed orders
- got required flags

## Flag:

```
THM{WINNER_OF_R@CE007}
THM{WINNER_OF_Bunny_R@ce}

```

## Concepts learnt:

- Understand what race conditions are and how they can affect web applications.
- Learn how to identify and exploit race conditions in web requests.
- How concurrent requests can manipulate stock or transaction values.

*** 

# 21. Malware Analysis - Malhare.exe
> Learn about malware analysis and forensics.

## Solution:

- went through HTA file structure
- used text editor to view HTA and ran command `pluma /root/Rooms/AoC2025/Day21/survey.hta`
- searched for metadata and function definitions
- answered the questions asked
- function getQuestions is downloadin survey ques from `survey.bestfestiivalcompany.com`
- got the flag after answerin all qeus

## Flag:

```
THM{Malware.Analysed}

```

## Concepts learnt:

- Application metadata
- Any network calls or encoded data
- Clues about exfiltration

*** 