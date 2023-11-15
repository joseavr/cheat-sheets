# Supabase with Next.js

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-08-28

---

# What is Supabase

- A platform with several services suchas databases, authentication, storage, etc. 
- Similar to Firebase from Google

# Main Menu

- Table Editor/SQL Editor: Edit tables either with sql queries or code
- Authentication
- Storage: Allows users to upload files

# Create a new Table
- Add a name for the table e.g 'posts'
- Add description, OPTIONAL
- Enable Row Level Security: restrict the data access such as: delete, write read, etc
## Columns
Create each column values for the table
- Name: `id`, Type: `uuid`, default value: `gen_random_uuid()`, primary: `checked`
- etc
- Name: `content`, Type: `text`, settings: `no nullable` (for columns that cannot be NULL, like user posts in social media)

Press `Save` then new table is created.

# Config Next.js with Supabase Auth
Dependencies to connect app with the database
```bash
npm install @supabase/auth-helpers-nextjs @supabase/supabase-js
```

Create an .env. API keys found in supabase.com.../settings/api
```.env
NEXT_PUBLIC_SUPABASE_URL = ""

# Safe to share. Controls whether user has access or not
NEXT_PUBLIC_SUPABASE_ANON_KEY = ""
```

Pass cookies to Supabase
```tsx
import { createServerComponentClient } from '@supabase/auth-helpers-nextjs'
import { cookies } from 'next/headers' // to access the request, headers, sessions, etc that supabase creates

export default async function HomePage() {
	// pass cookies so supabase has access to cookies
	const supabase = createServerComponentClient({ cookies }) 
	const { data: posts } = await supabase.from('posts').select('*')

	return (
	<main className="flex min-h-screen flex-col items-center justify-between p-24">
		Hello Twitter
		<pre>{JSON.stringify(posts, null, 2)}</pre> -> Renders empty array
	</main>
	)
}
```

## Policies
Adds configuration to a table to enable CRUD operations for certain types of users. e.g By default, the constant `posts` is an empty array since user has no access to this information. To set up, in supabase.com.../auth/policies,  add a `New Policy`. Recommended to choose `For full customization` option.

---
`Policy Name`:  e.g Allow all users to read posts
`Allowed Operation`: Select one operation e.g SELECT
`Target roles`: for now, leave it blank
`USING expression`: evaluates a code that returns either TRUE or FALSE. e.g `post.user_id = auth.uid()`. But for now, `true`

---

This is what postgreSQL under the hood does with the previous config:
```postgresql
CREATE POLICY "Allow all users to read posts" ON "public"."posts"
AS PERMISSIVE FOR SELECT
TO public
USING (true)
```

FInally, if we refresh the page, it should appear on the browser all posts created in the Table `posts`

# Supabase Auth with Github

Set up OAuth on Github on /settings/developers/OAuth Apps then `Register new application`

---
`Application name`: e.g next-twitter-supabase
`Homepage URL`: http://localhost:3000
`Application description`: A Twitter clone with Supabase 
`Authorization callback URL`: A provider URL that connects with Supabase. Found in supabase.com.../auth/providers. For this, we choose Github provider

Once filled up, `register application`. A Client ID and Client Secret is given. These are for supabase.com.../auth/providers/ -> GitHub

---

Note: Fix `Cant't resolve enconding`
```bash
npm i -D encoding
```

## auth-button




# Protected Routes

We can make redirection redirects at page level. We need to obtain session and validate it
```tsx
export default async function HomePage() {
	// pass cookies so supabase has access to cookies
	const supabase = createServerComponentClient({ cookies }) 
	
	// protected route: Redirection a page level
	const { data: { session } } = await supabase.auth.getSession()
	if (session === null) {
		redirect('/login')
	}
	
	...
```

# Public User Table

Even we have auth with session stored with user's username, email, avatar, etc information, it is not public and cannot be accessed in the front-end e.g if we want to retrieve or display username.

Create a new Table: users
`Name`: users
`Enable RLS`: checked

### Colum 1
`Name`: id 
`edit foreign relation`: 
- `select schema`: auth
- `select a table to reference to`: users (one to one)
- `action if referenced row is removed`: Cascade
`Type`: uuid
`Default Value`: gen_random_uudi()
`Primary`: checked

### Column 2
created_at no modified
### Column 3
`Name`: name
`Type`: text
`Settings`: Unchecked Nullable

### Column 4
`Name`: username
`Type`: text
`Settings`: Unchecked Nullable

### Column 5
`Name`: avatar_url
`Type`: text
`Settings`: Unchecked Nullable

Even tho these new table `user` is public, it is not recommended to display user email, it may be private.

# Functions (Procedures)

Procedures are functions that can be executed anytime we want e.g validations, control flow, constraints, etc. We will create Triggers with these functions

In SQL, triggers are function that executes along with SQL queries e.g when user authenticated, run a function to create this user in the public table `users`

---
supabase.com.../databases/functions

Name of function: insert_user_in_public_table_for_new_user
Schema: public
Return Type: trigger
Definition:
```postgresql
begin
	insert into public.users (id, name, user_name, avatar_url)
	values (
		new.id, 
		new.raw_user_meta_data->>'name',
		new.raw_user_meta_data->>'user_name',
		new.raw_user_meta_data->>'avatar_url'
	);
	return new;
end
```

SECURITY DEFINER: selected

---

## Add Triggers

Now we will add the triggers that fires some functions after some operations are perform in the database

e.g insert user in public `user` table when a user is authenticated (signed up) by the  `user auth` table

---
`Name of trigger`: on_auth.insert_users
`Table`: users auth
`Events`: check Insert
`Trigger type`: After the event (important: trigger this after the user is authenticated)
`Orientation`: Row
`Function to trigger`: insert_user_in_public_table_for_new_user

---

# Supabase Types

Supabase provides us the tables types for Typescript
```bash
npx supabase login
```

Token available at: https://supabase.com/dashboard/account/tokens

Generate types:
```bash
npx supabase gen types typescript --project-id [project-id-here]
```

The project id available at: supabase.com.../settings/general

Export to a specific folder:
```bash
npx supabase gen types typescript --project-id [project-id-here] > ./src/types/database.ts
```

Also, make a npm script in package.json:
```json
"scripts": {
 ...
 "gen:types": "npx supabase gen types typescript --project-id [project-id-here] > ./src/types/database.ts
",
 ...
}
```


# Insert Policies

An user can also write some posts, so create a new policy under `posts`

---
`Policy name`: Authenticated users can create their own posts
`Allowed operation`: Insert
`Target roles`: authenticated
`WITH CHECK expression`: 
```postgresql
user_id = auth.uid()
```

Postgresql query under the hood:
```postgresql
CREATE POLICY "Authenticated users can create their own posts" ON "public"."posts"
AS PERMISSIVE FOR INSERT
TO authenticated

WITH CHECK (user_id = auth.id())
```

---