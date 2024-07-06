# Reddit Features

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-11-24

---

# Auth with [NextAuth](https://next-auth.js.org/)

## Config

Api route to handle authentication. Opinionated set up.

Create: `/api/auth/[...nextauth]/route.js`

```js
import { authOptions } from "@/lib/auth"
import NextAuth from "next-auth"

// authOptions handles user sessions, JWT
const handler = NextAuth(authOptions)
export { handler as GET, handler as POST }
```

## Client-side Sign In with Google provider

```jsx
// login.with.google.button.jsx
import { signIn } from 'next-auth/react'

async function loginWithGoogle() {
	// states	
	try {
		// sign in with google provider
		await signIn('google')
	} catch (error) {
		// ...
	} finally {
		// ...
	}
}

return (
	<Button onClick={loginWithGoogle}
		// ... >
		Google
	</Button>
)
```

## Get User Session

From server components:
```js
import { getServerSession } from 'next-auth'
getServerSession(authOptions)
```
# Database:  PlanetScale + Prisma

Serveless (pay what you use) SQL platform. Uses AWS to store the database. Easy to scale. 29$/month to scale. Downside the concurrency connections if have more than 1,000 active users.

Planetscale free plan provides:
- 1 billion reads per month (33 million per day)
- 10 million writes per month
- 1,000 concurrency connections

Connect -> Connect with -> Prisma

```.env
DATABASE_URL='...'
```

## Prisma

Install the Prisma CLI:
```bash
npm install prisma --save-dev
```

Any changes to `schema.prisma`, push local changes to database (PlanetScale)

```bash
npx prisma db push
```

Generate types from our prisma file:
```bash
npx prisma generate
```

## Reddit: Database Design

![](20231125010655.png)
# Parallel Routes + Modals

Replacing a page with a modal and display the page when reload (f5).

Useful for login pages so users don't leave page.

```bash
app
|-- (auth)
|   |-- sign-in
|       |-- page.jsx
|   |-- sign-up
|       |-- page.jsx

|-- @authModal
|   |-- (.)sign-in
|       |-- page.jsx
|   |-- (.)sign-up
|       |-- page.jsx
|-- layout.jsx
```

`(.)` intercepts a path of the same level.
`(..)` intercepts a path one level higher.

Since `www.website/sign-in` is at the same level of `www.website/(.)sign-in`, then `(.)sign-in` will intercept it to display its modal

The same way, if we have `www.website/somePath/(..)sign-in`, it will intercept `www.website/sign-in`.

In `layout.jsx`:
```jsx
export default function RootLayout({
	children,
	authModal
}: {
	children: React.ReactNode
	authModal: React.ReactNode
}) {
	return (
		<html>
		<body>
			{/* Parallel route */}
			{authModal}

			{/* Main Content */}
			<main>
				{children}
			</main>			
		</body>
		</html>
	)
}
```

# Tanstack Query

Create a provider.

```jsx
'use client'

import { QueryClientProvider, QueryClient } from '@tanstack/react-query'
import { SessionProvider } from 'next-auth/react'
import { ReactNode } from 'react'

interface LayoutProps {
	children: ReactNode
}

const queryClient = new QueryClient()

export default function Providers({ children }: LayoutProps){
	return (
		<QueryClientProvider client={queryClient}>
			<SessionProvider>{children}</SessionProvider>
		</QueryClientProvider>
	)
}
```

Wrap up the `layout.jsx`:
```jsx
<body>
	<Providers>
		{children}
	</Providers>
</body>
```

Fetch on client-side:
- The `mutate` is a function that can be used to start fetching data. (i.e onClick)
- The `isLoading` is a boolean state
- The `data` is whatever the fetch returns
```js
const { mutate, isLoading, data } = useMutation({
	
	// The actual Fetch function
	mutationFn: async () => {
		const { data } = await axios.post("/api/subreddit", payload)
		return data as string
	},

	// Handle error
	onError: (err) => {
		if (err instanceof AxiosError) {
			if (err.response?.status === 409) {
				return ...
			}

			if (err.response?.status === 422) {
				return ...
			}

			if (err.response?.status === 401) {
				return ...
			}
		}
	},

	// Handle success
	onSuccess: (data) => {
		// do()
	},
})
```



# Miscelanous

## Apply buttons styles to a <Link/> component


```jsx
// buttonVariants() applies buttons style to anchor tags
<Link href="/sign-in" className={buttonVariants()}>
	Sign In
</Link>
```


