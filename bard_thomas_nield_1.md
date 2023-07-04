## Using Bard to Compose SQL Queries

It is well-known that LLM platforms like [Google Bard](https://bard.google.com) can help write code for developers. With some review and diligence, it can be a valuable assistant to generate code to execute those common tasks. One of these common tasks is querying databases, and we will discuss in this article how to leverage SQL capabilities in Bard. It can be especially helpful to iterate a given query and convert it between one SQL platform to another. 

Let's start by asking Bard to generate all records from a specific table, which got me this response below: 

**PROMPT:**

>Write SQL that will pull all records from a customer table 

**RESPONSE:** 

>Sure, here is the SQL code to pull all records from a customer table:
>
>SELECT *
>FROM customer;
>
>The SELECT * clause tells the database to return all columns from the customer table. The FROM clause specifies the table that we want to query. In this case, we are querying the customer table.
>
>To run this code, you would need to connect to a database and then execute the query. Once the query is executed, the database will return all records from the customer table.

Of course, I can continue this conversation with Bard and it will maintain context of my task until I reset. I can ask it to modify the query so that it returns 10 records. 

**PROMPT:**

>Can you also run that SQL query but only return the first 10 records? 

**RESPONSE:**

>Sure, here is the SQL code to run that query but only return the first 10 records:
>
>SELECT *
>FROM customer
>LIMIT 10;
>
>The LIMIT clause tells the database to only return the first 10 records from the customer table. The 10 after the LIMIT keyword specifies the number of records that we want to return.
>
>To run this code, you would need to connect to a database and then execute the query. Once the query is executed, the database will return the first 10 records from the customer table.


Now let's say I copied that SQL query into Microsoft SQL Server and discovered it is not working. The reason is that SQL Server does not use a `LIMIT 10` operation but rather a `TOP 10 *` instead. Even if we did not know this, we can try and ask Bard to convert the query into Microsoft SQL Server. 

**PROMPT:**

>Can you convert that for Microsoft SQL Server? 


**RESPONSE:**

>Sure, here is the SQL code to run that query in Microsoft SQL Server:
>
>SELECT TOP 10 *
>FROM customer;
>
>The LIMIT clause tells the database to only return the first 10 records from the customer table. The 10 after the LIMIT keyword specifies the number of records that we want to return.
>
>To run this code, you would need to connect to a database and then execute the query. Once the query is executed, the database will return the first 10 records from the customer table.


Great! So Bard did correct that SQL so that it is compatible with Microsoft SQL Server. Of course, it interestingly hallucinated in its description using the `LIMIT` clause instead, but we got the correct code. Let's then ask it to only pull a record with the `first_name` of "Jon". 

**PROMPT:**

>Retrieve the record with a first_name of "Jon" 


**RESPONSE:**


>Sure, here is the SQL code to retrieve the record with a first_name of "Jon":
>
>SELECT *
>FROM customer
>WHERE first_name = 'Jon';
>
>The SELECT clause in this query specifies the columns that we want to select from the customer table. In this case, we are selecting all columns.
>
>The WHERE clause in this query specifies the condition that we want to filter the results by. In this case, we are filtering the results to only include rows where the first_name column contains the string "Jon".
>
>To run this code, you would need to connect to a database and then execute the query. Once the query is executed, the database will return the record with the first_name of "Jon" from the customer table.


Finally, let's ask it to concatenate the `first_name` and `last_name` into a single field but for MySQL. 

**PROMPT:**


>Concatenate the first_name and last_name fields, but make it compatible with MySQL
>

**RESPONSE:**


>Sure, here is the SQL code to concatenate the first_name and last_name fields, but make it compatible with MySQL:
>
>SELECT CONCAT(first_name, ' ', last_name) AS full_name
>FROM customer;
>
>The CONCAT() function in this query concatenates the first_name and last_name columns, separated by a space. The AS full_name clause specifies the alias for the output of the CONCAT() function.
>
>To run this code, you would need to connect to a MySQL database and then execute the query. Once the query is executed, the database will return all rows from the customer table, with the first_name and last_name columns concatenated into a single column called full_name.

Sure enough, it correctly identified the `CONCAT()` function as the proper means to concatenate in MySQL. It even took the sensible liberty of naming that field `full_name`. If we asked it to rewrite this query for SQLite, it will correctly use the `+` operator instead. 

**PROMPT:**

>Rewrite that last query but for SQLite

**RESPONSE:**


>Sure, here is the SQL code to concatenate the first_name and last_name fields, but make it compatible with SQLite:
>
>SELECT first_name || ' ' || last_name AS full_name
>FROM customer;
>
>The || operator in this query concatenates the first_name and last_name columns, separated by a space. The AS full_name clause specifies the alias for the output of the || operator.
>
>To run this code, you would need to connect to a SQLite database and then execute the query. Once the query is executed, the database will return all rows from the customer table, with the first_name and last_name columns concatenated into a single column called full_name.


Hopefully this gives you a taste of Bard's capabilities of being a SQL assistant, and even if you are a veteran SQL developer it can still provide a handy reference to convert SQL from one platform (e.g. MySQL) to another (e.g. Microsoft SQL Server).
