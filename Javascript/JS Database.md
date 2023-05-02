# JS Database

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/Javascript">Javascript</a>

✏️Section: 0101

🗓️Date: 2023-04-22

---
# 🎬 Intro to Database

A database is a structured collection of data that is organized in a way that facilitates efficient retrieval and management of data. Databases are used to store, manage, and retrieve large volumes of data efficiently and accurately.

Databases are useful in a variety of applications, such as:
1. Business: Databases are used to manage customer data, inventory, employee records, financial transactions, and other business-related information.
    
2. Education: Databases are used to manage student records, course schedules, and grading information.
    
3. Healthcare: Databases are used to manage patient records, medical histories, and other healthcare-related information.
    
4. Research: Databases are used to store and manage research data, such as scientific experiments, surveys, and studies.
    
5. Government: Databases are used by governments to manage a wide range of information, such as census data, tax records, and criminal records.

### Usefulness?
- Ability to provide quick and efficient access to information. 
- Allows for the storage and retrieval of large amounts of data


# 🆚 Relational vs NonRelational DB

## Relational Database (ORM)
- Object Relation Mapping
- A Relational Database is a spreadsheet, with columns and rows, called **Table** or **Relation**
- Hard to modify
- Best practice is to come up with the GREATEST database for your application
- Relational databases are MySQL, Postgres, and SQLite. 
- To query a relational database, you'd use SQL.
- Field types: String, Integer, Float, enum, Etc.

<img src = 'https://i.stack.imgur.com/2CwlP.png' width='500px'>

## Non-Relational Database (ODM)
- Also called ODM (Object Document Mapper), which maps objects with a Document Database like MongoDB.
- Data is stored in JSON, instead of in tables, on the cloud.
- Easy to modify
- Non-Relational databases are MongoDB, CassandraDB, CockroachDB, etc.
- To query a non-relational database, you'd use Javascript
- Field types: Objects of key-values


# 🗓️MySQL (Relational)
- Database system included by XAMPP  
- MySQL/MariaDB Console
	- Allow us to execute commands (e.g., queries, createtables, etc.)

- Using MySQL provided by XAMPP (see notes below before continuing)
	- MakesureyouhavestartedMySQLServer » UseXAMPPControlPanelApplication
	- WecanissueSQLcommandsusingtheMySQLconsole  
	- In a PC we start the console by executing `.\mysql.exe –u root -p`
		- You can find my sql exe at `C:\xampp\mysql\bin`
		- You can open a window using cmd or Windows PowerShell  
	- In a Mac you can start the console by executing `./mysql–uroot-p`
		- You can find my sql at `/Applications/XAMPP/xamppfiles/bin`


# 🗓️ SQL (Structured Query Language)
- SQL allow us to create databases, tables, insert/delete data, etc.  
- SQL allow us to perform the four basic operations of data storage:
	- Create, Read, Update, Delete (CRUD)

## 🐧 SQL Commands

### **Database**
- Showing databases available
```sql
show databases;
```

- Creating databases
```sql
create database ourDB;
```

- Changing to a database
```sql
use ourDB;
```

- Removing Database
```sql
drop database <DATABASENAME>;
drop database ourDB;
```

<br/>

### **Tables**
- Create Table
```sql
create table <tableName> (fieldList);
create table movies(name varchar(20), year int);
```

- Showing tables in a database
```sql
show tables;
```

- Insert data
```sql
insert into <TABLENAME> values (<COMMA_SEPARATED_VALUES>);
insert into movies values ("Jaws Jr", 1976);
```

- Looking at table contents
```sql
select * from <TABLENAME>;
select * from movies;
```

- Delete data from table
```sql
delete from <TABLENAME> where <CONDITION>
delete from <TABLENAME>  (DONT, deletes everything from table)
```

- Removing a table
```sql
drop table <TABLENAME>
drop table movies;
```

- Updated data
```sql
update friends set salary=7778, year=8 where name = “Pat”;
```

- Replace data
```sql
replace into friends values (“Mary”, 5000);
```

<br/>

### Special Operators

- The `like` operator
```sql
delete from friends where name like “%Jose%”;
```

- `Order by` - to display elements ordered by a field
```sql
select * from friends order by salary;  #ascending
select * from friends order by salary desc;  #descending
```

- `count` - allows you to determine the number of records satisfying a criteria
	- Output - number of friends satisfying salary restriction
```sql
select count(name) from friends where salary <= 12000;
```

<br/>

### Field Types String/Blob/Enum/Null
- **char(length)**
- **varchar(length)**
- **blob or text** - (Binary Large Objects)
	- Use to store binary data (e.g., images). Maximum size is 65535  
- **tinyblob or tynytext** - blob or text with maximum size of 255 characters  
- **mediumblob or mediumtext** - blob or text with maximum size of 16777215
- **longblob or longtext** - blob or text with maximum size of 4294967295  
- **enum** - enumeration (maximum of 65535 values)

<br/>

### Conditionals
- Selecting data with conditions
```sql
select * from <TABLE> where <CONDITION>;
select * from friends where salary > 5000;
```

- Conditions Operators
	- `=` - equals  
	- `!=` - not equals  
	- `<=` - less than or equal to » <less than  
	- `>=` - greater than or equal to » > greater than

- Logical Operators: `and`, `or`

- Field specification (projection):
```sql
select <FIELDLIST> from <TABLE> where <CONDITION>
select name, met from friends where salary > 5000;
```

<br/>

### Functions
- `lcase` - returns a lowercase string
```sql
select lcase(“TOM”);
```

- `ucase` - returns an uppercase string 
```sql
select ucase(“cat”);
```

- `now()` - returns current date/time » Output: 2006-12-12 12:21:02
```sql
select now();
```

- `curdate()` - returns current date » Output: 2006-12-12
```sql
select curdate();
```

- `curtime()` - returns current time » Output: 12:21:24
```sql
 select curtime();
```

- `password()` - returns a hash for the string  
```sql
select password(“hello”)
```

### **Aggregation Functions**

-   `having` - to deal with aggregate functions (where clause cannot be used against aggregates).
```sql
select name, sum(amount) from expenses  
group by name  
having sum(amount) > 40;
```

- `limit` - controls the number of records returned
```sql
select * from allfriends limit 3;
select * from allfriends limit 3,2; # Skips the first three records and displays the following two
```

### Joins
Operation that allows us to combine information from several tables

- If you want to display the name, salary, and food someone likes, you can execute the following query:
```sql
select name, salary, food  
from friends, foods  
where friends.name = foods.person;
```