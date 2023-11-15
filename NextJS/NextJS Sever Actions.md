# Untitled

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-08-29

---

# What is Server Actions

Create server functions (server actions) that can be executed in `client-components`. e.g passing a server function inside of a form that is client component.

First, need to config to allow server action in `next.config.js`
```js
module.exports = {
  experimental: {
    serverActions: true,
  },
}
```

Example 

```tsx
'use client'
import { Avatar } from '@nextui-org/react'
import { createServerActionClient } from '@supabase/auth-helpers-nextjs'
import { cookies } from 'next/headers'
//import { revalidatePath } from 'next/cache'

export default function ComposePost({ ... }) {
	
	// server action/function
	async function addPost() {
		'use server'
		console.log('Hello World')
	}

	return (
		<form
			className="flex flex-row space-x-4 p-4 border-b border-white/20"
			action={() => addPost()} // server action
		>
			...
		</form>
	)
}
```