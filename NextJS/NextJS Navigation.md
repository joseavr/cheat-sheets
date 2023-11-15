# Untitled

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-08-28

---

# Next.js 13 App Router
## Params

Allows to catch the `req.params` from the URL

Client-side component
```jsx
'use client'
import { useParams } from 'next/navigation'

export default function ProductForm() {
	const params = useParams()
	// params.id, etc
}
```

Server-side component
```jsx
export default function ProductForm({ params }) {
	...
}
```

## Router

Allows to manipulate the router

Client-side component
```jsx
'use client'
import { useRouter } from 'next/navigation'

export default function ProductForm() {
	const router = useRouter()
	router.refresh()
	// router.push('urlHere')
	
}
```

Server-side component
```tsx
import { redirect } from 'next/navigation'
import { revalidatePath } from 'next/cache'

redirect('urlhere')
revalidatePath('urlhere') // re-renders, equivalent to router.refresh() from client
```