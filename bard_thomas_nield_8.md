## Use Bard to Identify Code Vulnerabilites

When using LLM's like Bard, a helpful task they can assist is taking a "first pass" at something. What I mean by this is you cannot replace a real "expert" with Bard but you can have it take a first stab at a given task. One such area is security. For example, let's say I have this Python code I plan on using for a web service. 

```python
from sqlalchemy import create_engine, text

engine = create_engine('sqlite:///thunderbird_manufacturing.db')
conn = engine.connect()

def customer_for_id(customer_id):
    stmt = text("SELECT * FROM CUSTOMER WHERE CUSTOMER_ID = " + customer_id)
    return conn.execute(stmt).first()
```

I want to see if there are any security vulnerabilities in it. Let's see what Bard does when I prompt it to analyze this code: 

**PROMPT:**

>Can you find security vulnerabilities with this Python function that will be used in a web application? ```from sqlalchemy import create_engine, text
>
>engine = create_engine('sqlite:///thunderbird_manufacturing.db')
>conn = engine.connect()
>
>def customer_for_id(customer_id):
>    stmt = te x t("SELECT * FROM CUSTOMER WHERE CUSTOMER_ID = " + cu stomer_id)
>    return conn.execute(stmt).first()
>```

**RESPONSE:**

>Sure, I can find security vulnerabilities with the Python function you provided. Here are a few things to consider:
>
>The function takes user input as a parameter, but it does not sanitize the input. This means that an attacker could inject malicious SQL code into the input, which could allow them to access or modify data in the database.
>
>The function does not check the permissions of the user who is calling the function. This means that an attacker could call the function with a customer ID that they do not own, which could allow them to view or modify data that they should not be able to access.
>
>The function does not use prepared statements. This means that the database is vulnerable to SQL injection attacks.
>
>To fix these vulnerabilities, you could do the following:
>
> * Sanitize the user input before it is passed to the SQL statement. This can be done by using a library like sqlalchemy.ext.declarative.orm.Query.filter().
> * Check the permissions of the user who is calling the function. This can be done by using the has_permission() method on the User model.
>* Use prepared statements. This can be done by using the text() function to create a prepared statement.
>Here is an example of how you could fix the vulnerabilities in the function:
>```python
>from sqlalchemy import create_engine, text
>from sqlalchemy.ext.declarative.orm import Query
>
>engine = create_engine('sqlite:///thunderbird_manufacturing.db')
>conn = engine.connect()
>
>
>class User(Query):
>
>    def has_permission(self, permission):
>        return self.filter(self.permissions.contains(permission)).first()
>
>
>def customer_for_id(customer_id):
>    stmt = text("SELECT * FROM CUSTOMER WHERE CUSTOMER_ID = :customer_id")
>    params = {"customer_id": customer_id}
>    return conn.execute(stmt, params).first()
>
>
>def main():
>    customer = customer_for_id(12345)
>    print(customer)
>
>
>if __name__ == "__main__":
>    main()
>```

Okay, this is good because I knew for a fact this Python code is vulnerable to [SQL Injection](https://www.w3schools.com/sql/sql_injection.asp), and Bard picked up on this immediately. SQL injection occurs when a SQL query string is concatenated with parameters, which can be hijacked with a different set of commands [as demonstrated here](https://youtu.be/6JfS8rHanAQ). Bard identified the problem and proposed some solutions, including checking user permissions as well as sanitizing the inputs. 

That being said, the output is not perfect because some extra artifacts have been put into the Python code. When I put this Python code in PyCharm with the SQLite database and SQLAlchemy library ready, it seemed to make up a non-existant call to SQLAlchemy with `from sqlalchemy.ext.declarative.orm import Query`. This is a limitation of the LLM and possibly hallucinated with other ORM libraries besides SQLAlchemy. It also created a dependent `User` class but did not show how to utilize it in the example. 

But this code is not useless! If I remove that import, modify or remove that `User` class (which does provide a starting template for an authentication), I can get this code to compile and work successfully as shown below. If you want to download the SQLite `thunderbird_manufacturing.db` file, you can [get it here](https://github.com/thomasnield/oreilly_programming_with_sql/raw/master/thunderbird_manufacturing.db). 
```python
from sqlalchemy import create_engine, text

engine = create_engine('sqlite:///thunderbird_manufacturing.db')
conn = engine.connect()

def customer_for_id(customer_id):
    stmt = text("SELECT * FROM CUSTOMER WHERE CUSTOMER_ID = :customer_id")
    params = {"customer_id": customer_id}
    return conn.execute(stmt, params).first()

def main():
    customer = customer_for_id(3)
    print(customer)

if __name__ == "__main__":
    main()
```
