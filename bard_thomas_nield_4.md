## Use Bard to Create Shell Scripts

Being able to leverage automation in your daily work is incredibly satisfying. Rather than iterating files and manually copying and pasting something from each one, you can use shell scripting to do it for you. There are also great scripting tools like [AutoHotKey](https://www.autohotkey.com) to automate repetitive UI tasks in Windows, and [Hammerspoon](https://www.hammerspoon.org) can do the same in macOS. However, these have a learning curve like everything else. You can save time by leveraging Bard to generate these scripts for you. 

Years ago, I had a legal client who asked me to perform discovery on a large file and report what was in it. It was 130GB in size and darn near impossible to open without specialized tools. After all, it was too big to open in a text editor. However, I remembered that Linux and macOS provides command-line tools that can perform these kinds of tasks. Rather than spending 5 hours researching the right tools and commands like I did back then, let's see if Bard can assist in this task. 

Let's first ask bard to write a shell script that samples and shows the first 10 lines of a file. 


**PROMPT:**

>Show me a shell script to sample the first 10 lines of a file


**RESPONSE:**

>Sure, here is a shell script to sample the first 10 lines of a file:
>```sh 
>#!/bin/bash
>
># Get the name of the file
>file_name=$1
>
># Sample the first 10 lines of the file
>head -n 10 $file_name
>```
>To run this script, you would save it as a file with a `.sh` extension, and then run it from the command line. For example, if you saved the script as `sample_first_10_lines.sh`, you would run it like this:
>```sh
>./sample_first_10_lines.sh my_file.txt
>```

Okay awesome, when I tested this on my Mac with a test file called `my_file.txt` it ran without a hitch. It sure enough printed the first 10 lines of that file. 

Now let's say this leads us to discover this text file is a MySQL database dump, which indeed was my situation.A SQL dump is a text file containing all the SQL commands in scripted form to recreate a database, including the table definitions and their data. The most meaningful thing I could do for my client was extract the `CREATE TABLE` definitions from the file, which shows the table names and what columns they contain. This effectively would answer their question on what kind of data was inside the file, but I had 130 GB to sift through. I did not remember the right command to do this task either. Let's get Bard to help with this! 

**PROMPT:**

>Write a shell script to extract all CREATE TABLE commands in a MySQL dump file


**RESPONSE:**

>Sure, here is the shell script to extract all CREATE TABLE commands in a MySQL dump file:
>```sh
>#!/bin/bash
>
># Get the name of the MySQL dump file
>dump_file=$1
>
># Create a new file to store the CREATE TABLE commands
>create_table_file="create_tables.sql"
>
># Use grep to extract all lines that start with "CREATE TABLE"
>grep -E "CREATE TABLE" $dump_file > $create_table_file
>
># Print a message to the user
>echo "All CREATE TABLE commands have been extracted to >$create_table_file"
>```
>To run this script, you would save it as a file with a `.sh` extension, and then run it from the command line. For example, if you saved the script as `extract_create_tables.sh`, you would run it like this:
>```
>./extract_create_tables.sh my_dump.sql
>```

Ah, `grep`! That's the command we need to sift through a file and return matches inside of it. However, when I ran this on my test file `my_dump.sql` it only grabbed the `CREATE TABLE` keywords and nothing more. I want not just the name of the table that follows but also the column definitions too. 

Let's see if we can get Bard to correct this and understand my intention a bit more explicitly. 

**PROMPT:**

>Can you retrieve the column declarations in the CREATE TABLE commands too? 

**RESPONSE:**
>Sure, here is the shell script to extract all CREATE TABLE commands in a MySQL dump file, including the column declarations:
>```sh
>#!/bin/bash
>
># Get the name of the MySQL dump file
>dump_file=$1
>
># Create a new file to store the CREATE TABLE commands
>create_table_file="create_tables.sql"
>
># Use grep to extract all lines that start with "CREATE TABLE"
>grep -E "CREATE TABLE(.|\n)*;" $dump_file > >$create_table_file
>
># Print a message to the user
>echo "All CREATE TABLE commands have been extracted to >$create_table_file"
>```
>The only difference between this script and the previous one is the use of the -E flag with grep. This flag tells grep to match the pattern "CREATE TABLE" and any characters that follow it, up to the end of the line or the next semicolon. This ensures that the entire CREATE TABLE command is extracted, including the column declarations.
>
>To run this script, you would save it as a file with a .sh extension, and then run it from the command line. For example, if you saved the script as `extract_create_tables.sh`, you would run it like this:
>```
>./extract_create_tables.sh my_dump.sql
>```

Nice. It successfully modified the `grep` command to use a regular expression and capture the entire `CREATE TABLE` commands including the column definitions and table names. It ignored all the other data in the file and grabbed only the table definitions. We can bill  the hours it takes to run the script (which definitely can take awhile) but not have to bill much for developing it. We also learned those few commands we needed very quickly, rather than trawling through encyclopedic documentation on shell scripting and `grep`. 

As in generating any code, be sure to validate the code carefully and ensure it compiles and runs correctly. There may be instances where Bard can hallucinate functions that do not exist, but at worst it can provide a nice starting point to developing your shell functions. You can also use Bard to generate automation scripts for Windows PowerShell, AutoHotKey, and Python. 

Leverage Bard and start making yourself more productive!
