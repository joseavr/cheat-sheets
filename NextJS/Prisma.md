# Prisma with SQLite in Next.js 13

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-08-23

---

# What is Prisma

Prisma is a serve-side library that helps developers read and write data to the database in an intuitive, efficient and safe way, and convert code into backend languages. It uses Typescript in order to type the models.

# Installation
- Create next app
```
npx create-next-app@latest project-name --typescrypt --tailwind
```

- Install Prisma
```bash
npm install prisma -D
```

- Initialize Prisma
```
npx prisma init
```

An `environment variable` is added and a file `schema.prisma` with:

```js
generator client {
	provider = "prisma-client-js"
}

datasource db {
	provider = "sqlite"
	url = env("DATABASE_URL")
}
```


# Creating a Model

```js
model Note {

	id Int @id @default(autoincrement())
	title String
	content String? // optional
	createdAt DateTime @default (now())
	updatedAt DateTime @updatedAt

}
```

# Execute Prisma
- Convert prisma code to SQL
```js
npx prisma migrate dev --name init
```

The migration file is created with converted code:
```sql
-- CreateTable

CREATE TABLE "Note" (
	"id" INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
	"title" TEXT NOT NULL,
	"content" TEXT,
	"createdAt" DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
	"updatedAt" DATETIME NOT NULL
);
```

# View Tables
- View tables in localhost
```bash
npx prisma studio
```
	