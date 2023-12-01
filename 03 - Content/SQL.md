---
creation date: January 2nd 2023
last modified date: January 2nd 2023
aliases: [Structured Query Language]
tags: #📕
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: [[SQLi]] - [[Database]] - [[MySQL]]
Search Tag: #📕  

# [[SQL]]  
___

## Description:  


## Query Types
### SELECT
**MySQL**
- `select * from users;` = Will pull all columns from the table users
- `select username,password from users;` = Will pull both username and password columns from table users
- `select * from users LIMIT 1;` = The limit clause forces the database to only return on row of data
	- `select * from users LIMIT 2,1;` = This will skip the first two rows then return one
- `select * from users where username='admin';` = Only returns usernames that match what we input
- `select * from users where username != 'admin';*` = Returns all others not equal to what we input
- `select * from users where username='admin' or username='jon';` = We can add in more with "**or**" operator
- `select * from users where username='admin and password='securepass';` = We can have it require multiple columns with the "**and**" operator
- `select * from users where username like 'a%';` = Returns all rows that **start with "a"** in the username column
- `select * from users where username like '%n';` = Returns all rows that **end with "n"** in the username column
- `select * from users where username like '%an%';` = Returns all rows that **contain "an"** in the username column

### UNION
Allows us to combine multiple select statements to retrieve from one or more tables.
- `select name,address,city from customers UNION select company,address,city from suppliers;`

### INSERT
Allows us to insert a new row or data into the table.
- `insert into users (username,password) values ('bob','password123')`

### UPDATE
Allows us to update existing rows of a table.
1. We start by selecting the table we want `update %tablename% SET`
2. Now select the field/s that we want to update `username='root',password='pass123'`
3. Finally specify exactly which rows to update `where username='admin';`
4. Fully built query: `update users SET username='root',password='pass123' where username='admin';`

### DELETE
`delete from users where username='martin';` = Will remove all rows in which the username field contains martin from the users table
`delete from users;` = WILL DELETE EVERYTHING FROM users TABLE


___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: January 2nd 2023 (05:55 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>
