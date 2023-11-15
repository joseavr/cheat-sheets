**# MySQL

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-08-24

---

# Connecting to MySQL with Next.js
- Install mysql https://dev.mysql.com/downloads/mysql/ and follow installation steps, add PATH, etc.

- Create a connection
```js
// create connection to MYSQL
import mysql from 'serverless-mysql'

export const connection = mysql({
	config: {
		host: 'localhost',
		user: 'root',
		password: 'Starcraft14.',
		port: 3306,
		database: 'nextmysqlcrud',
	},
})
```

- Connect mysql from terminal
```bash
mysql -u root -pYourPassword
```

```bash
CREATE DATABASE nextmysqlcrud;
```

- Querying test
```sql
show databases;
SELECT NOW();
```

- Necessary query to fix connection, https://stackoverflow.com/a/56509065
```js
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'yourpassword';
```

# Basic SQL CRUD

```js
import { NextResponse } from 'next/server'
import { connection } from '@/libs/mysql.js' 

export async function GET() {
	const result = await connection.query('SELECT NOW()')	
	return NextResponse.json({ message: result[0]['NOW()'] })

}
```


# Create a SQL Table in Next.js

- In sql terminal, use a specific databases created witht the following command
```sql
show databases;

use <databaseName>;
```

- Create a table
```sql
CREATE TABLE product(
	id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
	name VARCHAR(200) NOT NULL,
	description VARCHAR(200),
	price DECIMAL(10,2),
	createdAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP
)
```

- Verify the tables is created
```sql
show tables;

describe <tableName>;
```