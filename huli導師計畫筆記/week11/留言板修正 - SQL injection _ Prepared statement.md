# 留言板修正 - SQL injection / Prepared statement
### 原因
如果我們針對 sql query 的語法漏洞，在帳號加入 # 的符碼，SQL 會把 # 後面的都當作註釋，所以我們可以利用這個方法來讓 SQL 不用真實的 username 就把資料檢索出來，例如下面的例子我們讓 username 是一個空字串但加入一個判斷是否為 true ，因為 1=1 為 true ，所以整段為 true ，我們就拿到所有使用者資料了。
```php
usename: ' or 1=1#
password: 123
SELECT * FROM Ian_users WHERE username = '' or 1=1# and password = '123'
```
![](https://i.imgur.com/BBiHvZ1.png)

或者也可以利用 insert query 來偽造留言
```php
INSERT INTO Ian_comments(nickname, comments) 
VALUES ('$nickname', '$comments')

INSERT INTO Ian_comments(nickname, comments) 
VALUES ('a', '') , ('admin', 'test') 
-> content :') , ('admin', 'test

INSERT INTO Ian_comments(nickname, comments) 
VALUES ('a', (SELECT password FROM Ian_users limit 1))
-> ') , ('admin', (SELECT password FROM Ian_users limit 1))#
-> ') , ('admin', (SELECT password FROM Ian_users where id=3))#
> ') , ((SELECT username FROM Ian_users where id=3), (SELECT password FROM Ian_users where id=3))#
```

### Prepared Statement



###### tags: `week11`