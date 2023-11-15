# Tanstack / React Query

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-08-30

---

# Intro

Manage asynchronous states

- API request 

## Set up

Wrap the App with the Context Provider
```jsx
...
import { QueryClientProvider, QueryClient } from '@tanstack/react-query'

// config cient
const queryClient = new QueryClient()

ReactDOM.createRoot(document.getElementById('root')!).render(
	<QueryClientProvider client={queryClient}>
		<App />
	</QueryClientProvider>
)
```

Client: import the hook `useQuery()`
- At least two parameters: 
	- key: string[] -> identifies the query to retrieve it since queries are cached
	- function: a function that returns the data
```jsx

```