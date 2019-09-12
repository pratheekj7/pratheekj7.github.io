---
title: "My Blog"
date: 2019-09-10T15:52:55+05:30
draft: true
---

**What is _SQL Injection_?**
>SQL injection is a code injection technique that might destroy your database.
>SQL injection is one of the most common web hacking techniques.
>SQL injection is the placement of malicious code in SQL statements, via web page input.

**SQL in Web Pages**
>SQL injection usually occurs when you ask a user for input, like their username/userid, and instead of a name/id, the user gives you an SQL statement that you will unknowingly run on your database.

>Look at the following example which creates a SELECT statement by adding a variable (userId) to a select string. The variable is fetched from user input (getRequestString):

>**Example**
userId = getRequestString("UserId");
sql = "SELECT * FROM Users WHERE UserId = " + userId;

**SQL Injection Examples**
1. _SQL Injection Based on 1=1 is Always True_
>Look at the example above again. The original purpose of the code was to create an SQL statement to select a user, with a given user id.

>If there is nothing to prevent a user from entering "wrong" input, the user can enter some "smart" input like this:

>userId: 
105 OR 1=1

>Then, the SQL statement will look like this:

>**SELECT UserId, Name, Password FROM Users WHERE UserId = 105 or 1=1;**
The SQL above is valid and will return userId, name, password from the "Users" table, since OR 1=1 is always TRUE.

>A hacker might get access to all the user names and passwords in a database, by simply inserting 105 OR 1=1 into the input field.

2. _SQL Injection Based on ""="" is Always True_
>A hacker might get access to user names and passwords in a database by simply inserting " OR ""=" into the user name or password text box:

>User Name:
" or ""="
Password:
" or ""="

>The code at the server will create a valid SQL statement like this:

>**SELECT * FROM Users WHERE Name ="" or ""="" AND Pass ="" or ""="";**
The SQL above is valid and will return all rows from the "Users" table, since OR ""="" is always TRUE.

3. _SQL Injection Based on Batched SQL Statements_ 
>A batch of SQL statements is a group of two or more SQL statements, separated by semicolons.

>The SQL statement below will return all rows from the "Users" table, then delete the "Suppliers" table.
>**SELECT * FROM Users; DROP TABLE Suppliers;**

>Look at the following example:

>userId = getRequestString("UserId");
SQL = "SELECT * FROM Users WHERE UserId = " + userId;

>And the following input:
user id: 
105; DROP TABLE Suppliers

>The valid SQL statement would look like this:

>**SELECT * FROM Users WHERE UserId = 105; DROP TABLE Suppliers;**

**Prevention Techniques**
1. Use of Prepared Statements (with Parameterized Queries)
2. Use of Stored Procedures

