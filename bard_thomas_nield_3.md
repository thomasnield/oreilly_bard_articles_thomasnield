## Use Bard to Convert R to Python

Here is a useful task that LLM's like Google Bard can be of assistance. Let's say you inherited several R scripts in your workplace and you wanted to convert them to Python. With a little bit of prompting, you can save yourself some time and get your R code turned into Python code. 

Let's start simple. I have this simple R code declaring and printing a vector. I want to turn it into Python code. 

```R
s <- c('apple','red',5,TRUE)
print(s)
```

I can prompt Google Bard to convert it to Python like this. Note I am pasting the code into a triple-ticks ``` block: 

**PROMPT:**


>Can you convert this R code into Python code? ```s <- c('apple','red',5,TRUE)
>print(s)```


**OUTPUT:**

>Sure, here is the Python code that converts the R code s <- c('apple','red',5,TRUE):
>```python
>s = ['apple', 'red', 5, True]
>print(s)
>```
>The Python code is equivalent to the R code in terms of functionality. It creates a list called `s` that contains the elements `'apple'`, `'red'`, `5`, and `True`. Then, it prints the contents of the list `s`.

This is a great start, but let's say I wanted to using Pandas rather than a plain Python list. I can continue to prompt and ask for this change. 

**PROMPT:**

>Awesome, can you use Pandas to do that task? 


**OUTPUT:**

>Sure, here is the Python code that uses Pandas to do the same task:
>```python
>import pandas as pd
>
>s = pd.Series(['apple', 'red', 5, True])
>print(s)
>```
>The Python code first imports the Pandas library. Then, it creates a Pandas Series called `s` that contains the elements `'apple'`, `'red'`, `5`, and `True`. Finally, it prints the contents of the Series `s`.

Impressive, right? Well, we have just gotten started. Here is an R script I have that runs a SQL query against a SQLite database. 


```R
library(DBI)
library(RSQLite)

db <- dbConnect(SQLite(), dbname='thunderbird_manufacturing.db')

my_query <- dbSendQuery(db, "SELECT * FROM CUSTOMER LIMIT 1")
my_data <- dbFetch(my_query, n = 1)

dbClearResult(my_query)

remove(my_query)
dbDisconnect(db)
print(my_data)
```

There's a lot going on here in this script. Let's see if Bard can convert it into Python without any hand-holding, and if it figures out which libraries to use too.

**PROMPT:**


>Can you convert this R script into a Python script? ```library(DBI)
>library(RSQLite)
>
>db <- dbConnect(SQLite(), dbname='thunderbird_manufacturing.db')
>
>my_query <- dbSendQuery(db, "SELECT * FROM CUSTOMER LIMIT 1")
>my_data <- dbFetch(my_query, n = 1)
>
>dbClearResult(my_query)
>
>remove(my_query)
>dbDisconnect(db)
>print(my_data)```


**RESPONSE:**

>Sure, here is the Python script that converts the R script library(DBI); library(RSQLite); db <- dbConnect(SQLite(), dbname='thunderbird_manufacturing.db'); my_query <- dbSendQuery(db, "SELECT * FROM CUSTOMER LIMIT 1"); my_data <- dbFetch(my_query, n = 1); dbClearResult(my_query); remove(my_query); dbDisconnect(db); print(my_data):

>```python
>import sqlite3
>
>connection = sqlite3.connect('thunderbird_manufacturing.db')
>
>my_query = connection.execute('SELECT * FROM CUSTOMER LIMIT 1')
>my_data = my_query.fetchone()
>
>connection.close()
>
>print(my_data)
>```
>The Python code is equivalent to the R code in terms of functionality. It first imports the sqlite3 library. Then, it creates a connection to the thunderbird_manufacturing.db database. Next, it executes the SELECT * FROM CUSTOMER LIMIT 1 query and stores the results in a variable called my_data. Finally, it closes the connection to the database and prints the contents of the variable my_data.

Not bad! It did the conversion correctly! It figured out to use the `sqlite3` package as this was using a SQLite driver originally. It also used the `fetchone()` function capturing the context this was for a single result. 

Here is another example. Let's convert  this simple scatterplot written in R into a Python script using matplotlib. 


```r
x <- c(5,7,8,7,2,2,9,4,11,12,9,6)
y <- c(99,86,87,88,111,103,87,94,78,77,85,86)

plot(x, y)
```


**PROMPT:**


>Convert this r code to python using matplotlib ```x <- c(5,7,8,7,2,2,9,4,11,12,9,6)
>y <- c(99,86,87,88,111,103,87,94,78,77,85,86)
>
>plot(x, y)```


**OUTPUT:**

>Sure, here is the Python code that converts the R code `x <- c(5,7,8,7,2,2,9,4,11,12,9,6)` and `y <- c(99,86,87,88,111,103,87,94,78,77,85,86)` to Python using Matplotlib:
>
>```python 
>import matplotlib.pyplot as plt
>
>x = [5, 7, 8, 7, 2, 2, 9, 4, 11, 12, 9, 6]
>y = [99, 86, 87, 88, 111, 103, 87, 94, 78, 77, 85, 86]
>
>plt.plot(x, y)
>plt.xlabel('x')
>plt.ylabel('y')
>plt.show()

Great! That worked too. Lastly, let's try to convert one dataframe from R into a dataframe using Pandas. Let's also remove the first column and first row. 

```r
df <- data.frame (
  Length = c(200, 110, 80),
  Width = c(100, 150, 120),
  Height = c(60, 30, 45)
)

# Remove the first row and column
df_new <- df[-c(1), -c(1)]

# Print the new data frame
df_new 


**PROMPT:**


>Convert this r code to python using pandas: ```df <- data.frame (
>  Length = c(200, 110, 80),
>  Width = c(100, 150, 120),
>  Height = c(60, 30, 45)
>)
>
># Remove the first row and column
>df_new <- df[-c(1), -c(1)]
>
># Print the new data frame
>df_new ```


**OUTPUT:**

>Sure, here is the Python code that converts the R code `df <- data.frame (
Length = c(200, 110, 80),
Width = c(100, 150, 120),
Height = c(60, 30, 45)
)
>
>Remove the first row and column
>df_new <- df[-c(1), -c(1)]
>
>Print the new data frame
>df_new ` to Python using Pandas:
>
>```python
>import pandas as pd
>
>df = pd.DataFrame({
>    "Length": [200, 110, 80],
>    "Width": [100, 150, 120],
>    "Height": [60, 30, 45]
>})
>
># Remove the first row and column
>df_new = df.iloc[1:, 1:]
>
># Print the new data frame
>print(df_new)
>```

Handy, right? Granted the conversions might not always work 100% as hallucinations can occur. For example, nonexistent functions can be called on objects that do not have those functions. When this happens, you can attempt to have Bard correct it or you can seek to correct it manually. In most worst cases, the LLM can give you a starting point to work with. 
