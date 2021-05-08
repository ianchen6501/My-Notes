# View、Stored Procedure 與 Trigger (SQL)
### View
建立一個虛擬的表格供檢視，但無法新增、刪除(CRUD)等等。
用處通常是拿來給業主檢視他們想看得資料。
```sql=
create view 'viewname' as
...SQL request
```
另外也可以用在開放部分資訊給別人看的時候
### stored procedure
就像是 SQL 的 function，但不同於 sum 等等既成 function，是直接在 SQL 裡面設定一個常用的指令
設定的語句如下:
```sql=
DELIMITER //
CREATE PROCEDURE id_content(id int)
begin
Select c.content 
from Ian_blog_content as c
where c.id = id;
end //
DELIMITER ;
```
之後就可以用 id_content 的方法來執行
```sql=
call id_content(id);
```
要編輯 store procedure 要在 table 的 routine 裡面新增、刪除，也可以直接在裡面更改

### trigger
用來建立在 sql 事件發生前、後要執行的事件，例如紀錄使用者更改就可以用下列的語句
```sql=
DELIMITER //
CREATE TRIGGER before_users_upade
	BEFORE UPDATE ON Ian_blog_users
	FOR EACH ROW
BEGIN
	INSERT INTO users_audit (username, nickname, action)
	VALUES (OLD.username, OLD.nickname, 'UPDATE')
END //
DELIMITER ;
```
同時要建立一個 users_audit 的 table，那當下次 Ian_blog_users 有變更時就會自動 Insert 進去 users_audit

### 參考資料
[程式導師實驗計畫第二期：Lesson 8-1](https://docs.google.com/presentation/d/1GkEGrWsDzaFPCo6okzCEPacAuhL6KhiBPzFEllR3xmY/edit#slide=id.g44a5006d8d_0_4)


###### tags: `week14` `view` `stored procefure` `trigger` `SQL`