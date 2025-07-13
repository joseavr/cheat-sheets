
## <ins>Work in Different Environments</ins>


> Testing Database installation in Docker guide- [here](https://orm.drizzle.team/docs/guides/postgresql-local-setup)

> Prisma only reads from `.env` unless environment variables are injected

There are 2 ways to work with the Prisma CLI
- Development Environment (or local environment)
- Production Environment

To work with different database sources (i.e one for development, one for production), we could:  
1. [Programmatically Override the URL](https://www.prisma.io/docs/orm/reference/prisma-client-reference#datasourceurl) . **This is risky and can lead to unintentional database deletion.** 
2. Instead, we could safely create two `.env` , one for development and one for production, and load the urls from those files.

Create an `.env.development` and `.env.production` with their respective `DATABASE_URL`

Install dotenv cli, needed to inject environment variables
```bash
npm install -g dotenv-cli
```

Run in development or production with their env. variables
```bash
dotenv -e .env.development -- npx prisma generate

dotenv -e .env.production -- npx prisma generate
```

The process guide can be found here [here](https://www.prisma.io/docs/orm/more/development-environment/environment-variables/using-multiple-env-files#setup-multiple-env-files)


For testing, mock prisma client [docs](https://www.prisma.io/docs/orm/prisma-client/testing/unit-testing#mocking-prisma-client)

If `.env.test` was created then create a script that passes the env. variables to jest [docs](https://www.prisma.io/docs/orm/more/development-environment/environment-variables/using-multiple-env-files#running-tests-on-different-environments)
```bash
dotenv -e .env.test -- jest -i
```



## <ins>Team Workflow</ins>

[Prisma Docs](https://www.prisma.io/docs/orm/prisma-migrate/workflows/team-development)

 The recommended workflow is to:

1. Create and test migrations in a development environment using prisma migrate dev.
2. Commit these migrations to your version control system.
3. Apply the tested migrations to your production database using `prisma migrate deploy` as part of your deployment process Prisma ORM workflow.

### Workflow in Depth

1. Development Environment: In your development environment, you'll typically use a local or disposable database for rapid iterations and testing.

Commands:
Push changes directly to the database (creates one if not). 
- Use for prototyping, or early stage and don't know how the end database will look like. 
- **All table data may be erased if table was modified**. 
- This also generates a new Prisma Client, which means all types are updated
- Does not keep track of the database changes (i.e no migration history)
```bash
npx prisma db push
```

Create a migration history in **dev environment** and updates the Prisma Client.
- The migration history keeps track of the database changes.
- Needed for sync current environment and the database
- Data is lost. If **seed.ts** is set, then it will also seed the database
```bash
npx prisma migrate dev
```

Use this to reset your development database if needed Reset the development database.
```bash
npx prisma migrate reset
``` 

3. Testing Environment: For your testing environment, you'll want to use a separate database that mimics your production setup.

Commands:
Use this to apply migrations to your testing database Production and testing environments.
```bash
`npx prisma migrate deploy`
```

If you're using seed scripts for test data, run this after migrations Integration testing.
```bash
npx prisma db seed
``` 


3. Production Environment: For your production environment, you'll want to apply migrations carefully to avoid data loss or downtime.

Commands:
Use this to apply migrations to your production database Production and testing environments.

```bash
npx prisma migrate deploy
```

#### Typical Workflow:
1. Develop and test changes locally:
	- Make changes to your Prisma schema
	- Run `npx prisma migrate dev` to create and apply migrations
	- Test your changes thoroughly
2. Commit and push your changes:
	- Commit your updated Prisma schema and new migration files
	- Push to your version control system
3. CI/CD Pipeline:
	- In your testing environment:
		- Run `npx prisma migrate deploy` to apply migrations
		- Run your test suite
	- If tests pass, proceed to production deployment
4. Production Deployment:
	- As part of your deployment process, run `npx prisma migrate deploy`

Remember, `migrate deploy` should generally be part of an automated CI/CD pipeline, and it's not recommended to run this command locally to deploy changes to a production database. [link](https://www.prisma.io/docs/orm/prisma-migrate/workflows/development-and-production#production-and-testing-environments)




--- 




## <ins>Core Concept</ins>

When you’re working on your application and making changes to your database schema, you’ll need to run the migrate command again every time you make changes to the schema in order for Prisma to:
1. generate a migration file and apply it to the underlying database and 
2. regenerate the Prisma client in your project with the latest types and model methods.

### Prisma Generate

 Creates or updates the Prisma Client in the .prisma/client folder

1. Reads your Prisma schema file.
2. Generates your Prisma Client library based on the schema.
3. Prisma Client and database schema are now in sync. 

```bash
npx prisma generate
```

### Prisma Migrate

Apply migration-history to the database. **Should not be used in production environment**. 

1. read migration.sql files and runs them in the shadow DB for checking errors.
2. create an SQL migration based on changes in your Prisma schema.
3. apply new migration to the development database. **Potentially deletes all data**.
4. generate/updates Prisma Client based on the new schema.
5. If no migration history found in the DB, the table`_prisma_migrations` is populated in the DB

```bash
npx prisma migrate dev [--name commit-message]
```


### Prisma Push

Best approach for rapid prototyping. Sync Prisma schema and Database schema without persisting a migration. Used in **local environment**, to prototype schema design and no care about changes impact data.

1. Pull current datatabase schema
2. Generate alternations based on diff
3. Apply migrations to the database

```bash
npx prisma db push 
```

### Prisma Deploy

Similar to `prisma migrate`, but does not delete data. For production environments. 

1. applies pending migrations to the database without resetting the database.
2. used in automated CI/CD pipeline (not used in locally and testing environments).
3. does not detect schema drift or reset the database

```bash
npx prisma migrate deploy
```


### Prisma Resolve

 In a schema drift, `prisma migrate resolve` command reconciles your migration history after making such changes such as 
 Patching & hotfixing.
 
```bash
npx prisma migrate resolve
```



--- 

Sync Prisma schema with Database schema in **Development Environment**

```bash
## recommended when working in local (dev environment)
npx prisma migrate dev [--name commit-message]
# or 
npx prisma db push
```

Sync Prisma schema and migration history with Database

```bash
npx prisma migrate deploy
```

Conflict or diff between Database Schema, Prisma Schema, and migration history.
This can happen:
1. Updated manually the Database
2. 
Use the `npm prisma migrate diff` to:
- Either revert the Database changes to sync with current Prisma schema
- Or move forward with the Database changes 

```bash
npx prisma migrate diff 

# then apply the changes 
npx prisma db execute
```


Sync Prisma schema and Database schema without persisting a migration
- when to use?
	- in local environment, to prototype schema design
	- no care about changes impact data
- if prompts "drop" or "re-creation" then there's a destructive change
- Destructive change example:
	- Modifying column with field required when there is already a row with this field empty. 

```bash
npx prisma db push 
```


Sync migration history with **production** Database
- Compares migration history locally with the migration history stored in Database and applies the missing migration that the Database migration history needs from local dev
-  
```bash
npx prisma migrate deploy
```


Workflow:
- [CI pipeline](https://www.prisma.io/docs/assets/images/prisma-migrate-lifecycle-225cf148241db936bf0ea6881386bebc.png)


---



## <ins>Questions</ins>

### If url string is from my production database, then how can i use a disposable database if working in a development environment?

To use a disposable database for development while keeping your production database separate, you can set up different database URLs for different environments. Here's how you can achieve this:

1. Use multiple .env files: Create separate .env files for different environments, such as .env.development and .env.production. In your .env.development file, you can specify a connection string for a local or disposable database Using multiple .env files.

2. Set up environment-specific database URLs: In your .env.development file, you can set a DATABASE_URL that points to your local or disposable database. For example:

```
DATABASE_URL="postgresql://username:password@localhost:5432/dev_database"
```
Your .env.production file (which should not be stored locally for security reasons) would contain the production database URL.

3. Use environment variables: You can use environment variables to switch between different database URLs based on the current environment. For example, in your Prisma schema:

```
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}
```
Then, when running Prisma commands, you can specify which .env file to use:

```
dotenv -e .env.development -- npx prisma migrate dev
```
This command uses the dotenv-cli package to load the correct environment variables Development.

4. For local development, you can use a local database or a dedicated development database. This keeps your production data safe while allowing you to freely modify the development database Prisma Migrate in a development environment (local).

5. If you're using a cloud-hosted database service, you might be able to create separate databases for development and production within the same account.

Remember, it's crucial to keep your production database URL secure and never use it directly in your development environment. Always use a separate, disposable database for development to prevent accidental changes to production data Deploy migrations from a local environment.

By following these practices, you can safely use prisma migrate dev in your development environment without risking your production data.