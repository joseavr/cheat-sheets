# Next.js 13  App Router

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-12-25

---


# Params

### URL Params

Allows to catch the `req.params` from the URL

**Client-side component**:

```jsx
'use client'
import { useParams } from 'next/navigation'

export default function ProductForm() {
  const params = useParams()
 // params.id, etc
}
```

**Server-side Component:**

```jsx
export default function ProductForm({ params }) {
  ...
}
```

**Route-handler:**
```ts
// URL -> /items/[slug]
export async function GET(
  { params }: { params: { slug: string } }
) {
  const slug = params.slug // 'a', 'b', or 'c'
}
```

### Query Params

**Client-side component:**
```tsx
'use client'
import { useSearchParams } from 'next/navigation' // hook

// URL -> /dashboard?search=my-project
export function SearchBar() {
  const searchParams = useSearchParams()
  const search = searchParams.get('search')
  // search -> "my-project"
}
```

**Server-side component:**

```tsx
export default function Page({
  searchParams,
}: {
  searchParams: { [key: string]: string | string[] | undefined }
}) {
  return <h1>My Page</h1>
}
// searchParams :: { key : params } or { key1 : params1, key2 : params2, ...}
// key :: string
// params :: string | string[] | undefined
```

**Route-handler:**
```ts
import { type NextRequest } from 'next/server'

// URL -> /api/search?query=hello
export function GET(request: NextRequest) {
  const searchParams = request.nextUrl.searchParams
  const query = searchParams.get('query')
  // query -> "hello"
}
```

### Body Params

**Client-side or Server-side component:**
```tsx

```

**Route-handler:**
```ts
export async function POST() {
 const body = await request.json().then((data) => data as DataType)
}
```


# Headers

**Client-side Component:**
```tsx
fetch(url, {

})
```

**Route-handler:**

```ts
import { headers } from 'next/headers'

export async function GET(req: NextRequest) {
  const headers = new Headers(req.headers)
  const token = headers.get("Authorization")
  // OR
  const token = req.headers.get("Authorization") // better
}

// OR
export async function GET(request: Request) {
  const headers = headers()
  const token = headers.get("Authorization")

	// Create a `new Response` if needs to send new headers 
  return new Response('Hello, Next.js!', {
    status: 200,
    headers: { referer: "123" },
  })
}
```



# Cookies

**Client-side Component:**

**Route-handler:**




# Router Navigation

Allows to manipulate the router

### Redirecting

**Client-side component:**
```jsx
'use client'
import { useRouter } from 'next/navigation'

export function ProductForm() {
	const router = useRouter()
	router.refresh() // refreshes the page (new request, refetches data, re-render client-server components)
	router.push('urlHere') // redirects to another page, saves to history stack
	router.back() // redirects previous route in the browser’s history stack.
  router.forward() // redirects next page in the browser’s history stack.
	router.replace(href: string, { scroll: boolean }) // redirects without adding a new entry into the browser’s history stack
 router.prefetch(href: string) // Prefetch the provided route for faster client-side transitions.
}
```

**Server-side component:**
```tsx
import { redirect } from 'next/navigation'
import { revalidatePath } from 'next/cache'

export function Product() {
	
	revalidatePath('urlhere') // revalidates cache-data next time page visited
	redirect('urlhere') // redirects to another page
	// redirect() can be use in:
	// client & server components, route handlers, server actions
}
```

**The redirect() vs router.push():**
Redirect and router.push() are fairly similar, the main differences are:
- `router.push()` can only be used on the client    
- `redirect()` can be used on the client and server
- only `router.push()` pushes a new entry into the history stack so on back navigation the user will return to where they previously were



# Data Caching

Either caching, no catching, revalidate at certain time.

### Caching Data
```tsx
// 'force-cache' is the default, and can be omitted
fetch('https://...', { cache: 'force-cache' })
```

### No Caching Data
```ts
// Request refetched on every request
fetch('https://...', { cache: 'no-store' })
```

### Revalidate Cache-Data

Purges the Data Cache and re-fetching the latest data.

**Time-based revalidation:**
```tsx
// Request cached for 1 minute.
fetch('https://...', { next: { revalidate: 3600 } })
```
Or
```tsx
// page.tsx | layout.tsx | route.ts
export const revalidate = 3600 // revalidate at most every hour
```

**Client-side  component:**
```tsx
"use client"
import { useRouter } from 'next/navigation'

const router = useRouter()
router.push() // clears Router-cache and makes new request for current route
// ?? router.refresh()
```

**Server-side component:**
```tsx
import { redirect } from 'next/navigation'
import { revalidatePath } from 'next/cache'

revalidatePath('urlhere') // revalidates cache-data next time page visited
revalidatePath('/blog/post-1') // revalidates single url
revalidatePath('/(main)/post/[slug]', 'page') 
revalidatePath('/(main)/post/[slug]', 'layout')
revalidatePath('/', 'layout') // revalidates all data
// Note: good combo to refetch data in a page (e.g after submitting a form)
redirect('urlhere')
```


**Route-handler:**
```ts
import { revalidatePath } from 'next/cache'
import { NextRequest } from 'next/server'
 
export async function GET(request: NextRequest) {
  const path = request.nextUrl.searchParams.get('path')
 
  if (path) {
    revalidatePath(path)
    return Response.json({ revalidated: true, now: Date.now() })
  }
 
  return Response.json({
    revalidated: false,
    now: Date.now(),
    message: 'Missing path to revalidate',
  })
}
```


**revalidatePath vs router.refresh:**

`router.refresh` clears Router cache, and re-render without invalidating the Data Cache or  Full Route Cache.

`revalidatePath` purges the Data Cache and Full Route Cache.

### Third-Party Libraries

Fetching a database, CMS, or ORM client without `fetch()`

```ts
// TODO
```