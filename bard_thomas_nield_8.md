## Use Bard to Identify Code Vulnerabilites

When using LLM's like Bard, a helpful task they can assist is taking a "first pass" at something. What I mean by this is Bard cannot replace a real "expert" on a given topic, but you can have it take a first stab at assessing a task. One such area is code security and finding vulnerabilities. For example, let's say I have this Python code I plan on using for a web service. 

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

That being said, the output is not perfect because some extra artifacts have been put into the Python code. When I put this Python code in PyCharm (with the SQLite database and SQLAlchemy library ready), it seemed to make up a non-existant call to SQLAlchemy with `from sqlalchemy.ext.declarative.orm import Query`. This is a limitation of the LLM and possibly hallucinated with other ORM libraries besides SQLAlchemy. It also created a dependent `User` class but did not show how to utilize it in the example. 

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

You do not know what you do not know, and Bard can help highlight security concerns you may not have been aware of. This does not mean Bard will identify every security issue (and you should assume it will not), but the ones it does point out will give you knowledge immediately on what needs to be fixed. To find further corner cases that Bard might be missing, you can always do further code analysis and talk to more experienced peers later. But at least you can get the glaring issues resolved with Bard first. 

While we are here, we might as well maximize Bard by asking it what other issues it might be overlooking. 

**PROMPT:**

> What other security issues should I watch out for that Bard might not have captured here? 

**RESPONSE:**

>Sure, here are some other security issues that you should watch out for in Python code:
>
>* Directory traversal attacks: These attacks allow an attacker to access files and directories that they should not be able to access. This can be done by injecting malicious code into a URL or by exploiting a vulnerability in the code.
>* Insecure deserialization: This is a vulnerability that allows an attacker to inject malicious code into a serialized object. This can be done by exploiting a vulnerability in the code or by sending a malicious serialized object to the application.
>* Remote code execution (RCE): This is a serious vulnerability that allows an attacker to execute arbitrary code on the target system. This can be done by exploiting a vulnerability in the code or by sending a malicious file to the application.
>* XML external entity (XXE) attacks: These attacks allow an attacker to read arbitrary files on the target system. This can be done by exploiting a vulnerability in the code or by sending a malicious XML document to the application.
>* Insecure cryptographic libraries: These libraries can be vulnerable to various attacks, such as man-in-the-middle attacks and brute-force attacks. It is important to use secure cryptographic libraries and to keep them up to date.
>
>In addition to these specific vulnerabilities, there are also some general security best practices that you should follow when writing Python code. These include:
>
>* Sanitizing all user input: This is the most important security best practice. All user input should be sanitized before it is used in the code. This will help to prevent attackers from injecting malicious code into the application.
>* Using prepared statements: Prepared statements are a secure way to execute SQL queries. They help to prevent SQL injection attacks.
>* Keeping your code up to date: It is important to keep your code up to date with the latest security patches. This will help to protect your application from known vulnerabilities.
>* Using a secure development environment: A secure development environment will help to prevent attackers from gaining access to your code. This includes using a firewall, antivirus software, and other security measures.
>I hope this helps! Let me know if you have any other questions.

Okay, this is helpful. These are the kinds of personal growth tasks that make Bard useful. Bard may not provide perfect information but it provides quick leads we can easily follow up and verify, and give us further topics for our own growth and research. Bard is not going to take your job as a developer, but it can certainly assist you! 
