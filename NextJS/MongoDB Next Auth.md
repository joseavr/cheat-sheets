# MongoDB + NexthAuth in Next.js

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-08-26

---

# Intro
  
- Configure next.js app with mongoDB thru `mongoose` 
- Create REST APIs in Next.js
- Bcrypt to encrypt password
- Axios
- Set up Next Auth (similar to Passport in Express) that provides sessions and users
- Configure JWT (JSON Web Tokens) for auth
# Installation Dependencies

```bash
npm i next-auth mongoose axios bcryptjs
```

- If project in Typescript
```bash
npm i @types/bcryptjs -D
```

# MongoDB Connection
```ts
import mongoose from 'mongoose'
const { MONGODB_URI } = process.env

// .env.local is ignored, so check if MONGODB_URI exists
if (!MONGODB_URI) {
	throw new Error('MONGODB_URI MUST BE DEFINED')
}

// Use this function in every API route
export const connectDB = async () => {
	const { connection } = await mongoose.connect(MONGODB_URI)
	try {
		// readyState === 0 disconnected
		// readyState === 1 connected
		// readyState === 2 connecting
		// readyState === 3 disconnecting	
		if (connection.readyState === 1) {
			console.log('MongoDB connected')
			return Promise.resolve(true)
		}
	} catch (error) {
		console.log(error)
		return Promise.reject(false)
	}
}
```


# Next Auth (App Router)
- Next Auth similar to Passport, deals with auth, JSON Web Tokens, etc
- [Next Auth](https://next-auth.js.org/) is becoming [Auth.js](https://authjs.dev/), to be used for every framework, not only for Next.

Create a route.ts in /app/api/auth/[...nextauth]/route.ts
```ts
import NextAuth from 'next-auth'
import CredentailsProvider from 'next-auth/providers/credentials'

/****
Login
*****/
const handler = NextAuth({
	// authenticate with providers: Google, Github, Amazon, etc
	providers: [
		CredentailsProvider({	
			name: 'credentials', // auth name
			credentials: {
				// creates a form in /api/auth/signin
				email: { label: 'Email', type: 'email', placeholder: 'jsmith' },
				password: { label: 'Password', type: 'password' }, // values to be authenticated
				},
				
				// credentials
				// req -> additional info (cookies, headers, etc)
			async authorize(crendentials, req) {
				// user from API
				const user = { id: '1', fullname: 'J Smith', email: 'john@gmail.com' }
				return user // return user authenticated available in every page
			},
		}),
	],
})

export { handler as GET, handler as POST }
```

Need to add these environment variables:
```.env.local
# NEXT_AUTH CRENDENTIALS
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=any_hashed_secret_strings_here
```

- When form submitted with valid data, page is redirected to main root page with a session.
- Session is created in console/application/cookies:
	- next-auth.session
	- next-auth.csrf
	- next-auth.callback

In authorize, user authenticated is returned and ready to use in every pages of the app.
```js
// credentials
// req -> additional info (cookies, headers, etc)
async authorize(crendentials, req) {
	const user = { ... } // user from API
	return user // return user authenticated available in every page (how? app wrapped with a Context)
},
```

- How? Wrap the app up with a Context.
- Create a Provider in app/Providers.tsx.
```tsx
'use client'
import { SessionProvider } from 'next-auth/react'

interface Props {
	children: React.ReactNode
} 

export default function Providers({ children }: Props) {
	return <SessionProvider>{children}</SessionProvider>
}
```

- Wrap the App with the Context in app/layout.tsx
```tsx
import ...
import Providers from '@/app/Providers'

export default function RootLayout({...}) 
	return (
		<html lang="en">
			<body className={inter.className}>
				<Providers>{children}</Providers>
			</body>
		</html>
	)
}
```


# Protected Routes

Create a middleware.ts in /app/middleware.ts
```ts
export { default } from 'next-auth/middleware'

export const config = {
	matcher: ['/dashboard'], // add protected routes
	// matcher: ['/dashboard/:path*'] // protect all nested routes
}
```

