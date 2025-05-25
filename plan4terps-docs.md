# Project Installation

##  Next.js + Shadcn 

Create next project
```bash
npx create-next-app@latest
```

Add Shadcn
```bash
npx shadcn@latest init
```

## Supabase 

`cs-plan4terps`'s database password

```
UIS2bcWoi1bzdh6d
```

Since we're not going to use Supabase Client (PostgREST) and instead Prisma, turn it off at `.../dashboard/project/[projectId]/settings/api`

## Prisma + Supabase 

Install Prisma package as dev dependency
```bash
npm i prisma -D
```


Initiallize project with Prisma CLI
```bash
npx prisma init
```


Add `schema.prisma`
```bash title:prisma/schema.prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider  = "postgresql"
  url       = env("DATABASE_URL")
  directUrl = env("DIRECT_URL")
}
```

Add database urls (provided by Supabase dashboard) to connect with Prisma, as environment variables
```.env
# needed for queries from Prisma to Supabase DB
DATABASE_URL="postgresql://postgres.hfcbqwhemvmhztnvbper:UIS2bcWoi1bzdh6d@aws-0-us-east-1.pooler.supabase.com:6543/postgres?pgbouncer=true&connection_limit=1"

# needed for migrations with Prisma CLI 
DIRECT_URL="postgresql://postgres.hfcbqwhemvmhztnvbper:UIS2bcWoi1bzdh6d@aws-0-us-east-1.pooler.supabase.com:5432/postgres"
```

Install Prisma Client, the query builder
```bash
npm install @prisma/client
```

(Only for Testing) To check Prisma + Database works correctly run the following, then delete the tables at Supabase dashboard
```bash
npx prisma migrate dev --name first_prisma_migration
```

Export the Prisma Client
```ts title:
import { PrismaClient } from '@prisma/client'

// globalThis - a constant that persists across multipe server restarts
const globalForPrisma = globalThis as unknown as { prisma: PrismaClient }

export const db =
  globalForPrisma.prisma || new PrismaClient()

// In development or testing mode, we want to reuse the same connection 
// after server restart, so we store it in a global variable (globalForPrisma).
// After server restarts, we will reuse the global connection (line 5).
// In production mode, globalForPrisma will always be `undefined` because 
// in this line it's never set.
if (process.env.NODE_ENV !== 'production') globalForPrisma.prisma = db

// The database url strings can be uploaded dynamically through
// the env variables for production and development environments
```

Specify the `schema.prisma` location in package.json if the location was changed
- https://www.prisma.io/docs/orm/prisma-schema/overview/location#prisma-schema-location
```json title:package.json
{
...
  "prisma": {
    "schema": "src/database/prisma/schema.prisma"
  },
...
}
```


## Prisma + Xata (Postgres)

After some research, I found a database service called Xata, a Postgres DB with 15GB of storage, compared to the 0.5 GB from Supabase.

1. When creating a new database in Xata, turn on `direct access to Postgres`. This allows connection thru the connection string
2. Add the connection string in a env. variable
```.env
DATABASE_URL="postgresql://qmj59q:<YOUR_API_KEY>@us-east-1.sql.xata.sh/plan4terps:main?sslmode=require"
```

3. We will use Prisma Driver Adapters, they support serverless and edge environments. Install dependencies and add it to the prisma file
```bash
npm install @prisma/adapter-pg pg
```

```.prisma
generator client {
	...
  previewFeatures = ["driverAdapters", ...]
}
```

4. Create the Prisma Client
```ts
import { PrismaPg } from "@prisma/adapter-pg"
import { PrismaClient } from "@prisma/client"
import { Pool } from "pg"

// globalThis - a constant that persists across multipe server restarts
const globalForPrisma = globalThis as unknown as { prisma: PrismaClient }

export const db = globalForPrisma.prisma || getNewPrismaClient()

// In development or testing mode, we want to reuse the same connection
// after server restart, so we store it in a global variable (globalForPrisma).
// After server restarts, we will reuse the global connection (line 5).
// In production mode, globalForPrisma will always be `undefined` because
// in this line it's never set.
if (process.env.NODE_ENV !== "production") globalForPrisma.prisma = db

// The database url strings can be uploaded dynamically through
// the env variables for production and development environments

//
function getNewPrismaClient() {
	const connectionString = `${process.env.DATABASE_URL}`
	const pool = new Pool({ connectionString })
	const adapter = new PrismaPg(pool)
	const prismaClient = new PrismaClient({ adapter })
	return prismaClient
}
```

5. We also need the `shadowDatabase` in order to use Prisma Migrations. 
	- Add `shadowDatabaseUrl` and `a` in the schema.prisma file.
```.prisma
datasource db {
  provider          = "postgresql"
  url               = env("DATABASE_URL")
  shadowDatabaseUrl = env("SHADOW_DATABASE_URL")
}
```

- Create a new database with  `direct access to Postgres` enabled and copy and paste into env. variables (generate an API Key)
```bash
SHADOW_DATABASE_URL="postgresql://qmj59q:<YOUR_API_KEY>@us-east-1.sql.xata.sh/plan4terps-migrations:main?sslmode=require"
```
6. Finally run `npx prisma generate` to update the Prisma Client.
## Installing Biome.js

Biome.js is a linter, made in rust, blazingly fast.
```bash
npm i -D @biomejs/biome   
```

Run `biome` 
```bash
npx @biomejs/biome init
```

Then, Install biome.js extension at the marketplace

Add the following rules at the root `biome.json`. 
Biome docs  [here](https://biomejs.dev/reference/configuration/)
```json
{
	"$schema": "https://biomejs.dev/schemas/1.9.4/schema.json",
	"vcs": {
		"enabled": true,
		"clientKind": "git",
		"useIgnoreFile": true
	},
	"files": {
		"ignoreUnknown": false,
		"ignore": []
	},
	"formatter": {
		"enabled": true,
		"indentStyle": "tab"
	},
	"organizeImports": {
		"enabled": true
	},
	"linter": {
		"enabled": true,
		"rules": {
			"recommended": true,
			"correctness": {
				"noUnusedImports": "warn",
				"noUnusedVariables": "warn",
				"noUnsafeOptionalChaining": "error",
				"noUnsafeFinally": "error"
			},
			"nursery": {
				"useSortedClasses": "warn"
			}
		}
	},
	"javascript": {
		"formatter": {
			"arrowParentheses": "always",
			"quoteStyle": "double",
			"jsxQuoteStyle": "double",
			"bracketSameLine": false,
			"bracketSpacing": true,
			"semicolons": "asNeeded",
			"trailingCommas": "none"
		}
	},
	"json": {
		"formatter": {
			"indentStyle": "tab"
		}
	},

	"css": {
		"formatter": {
			"enabled": true
		},
		"parser": {
			"cssModules": true
		}
	}
}
```


## Commit Naming Convention

### For general setup or maintenance:
- `chore(api): initialize project with [libraries/tools]`
- `chore(web): add dependencies for [Shadcn, TailwindCSS, etc.]`
- `chore(docs): configure project tooling (TailwindCSS, etc.)`

### For adding or updating features:
- `feat: add [feature] using [library]`
- `feat: integrate [library] for [feature]`
- `feat: setup initial styles with TailwindCSS`

### For fixes:
- `fix: resolve issue with [specific problem or package]`
- `fix: correct TailwindCSS configuration`

### For configuration changes:
- `config: setup [TailwindCSS/PostCSS] configuration`
- `config: add initial configuration for [package]`
