# Tanstack / React Query

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-08-30

---

# What is React Query

Manage asynchronous states

- API request 

# Set up

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

# useQuery

The `useQuery` hook in React Query is used for fetching and caching data from an API endpoint. (GET)

```jsx
import { useQuery } from 'react-query'

const fetchData = async () => {
  const response = await fetch('/api/...');
  const data = await response.json();
  return data;
}

const { data, isLoading } = useQuery(
	{
		queryKey: ['myQueryKey'],
		queryFn: fetchData

		// advanced options
		refetchOnWindowFocus: false, // Disable automatic refetching on window focus
		staleTime: 60000, // Set the time after which the data is considered stale (in ms)
		onError: (error) => { 
			// Handle errors, e.g., display a toast
	}
)
```

The useQuery() can return:
- **data**: The data returned from the query.
- **isLoading**: A boolean indicating whether the query is currently loading.
- **isError**: A boolean indicating whether an error occurred during the query.

# useMutation

React query hook for modifying/mutating data. (POST, PUT, DELETE)

```jsx
import { useMutation} from 'react-query'

const { mutate, isLoading } = useMutation({
	
	mutationFn: async () => {
		// func must have the actual fetch.post and return data (no a response).
		const payload = ...;
		const { data } = await axios.post("/api/...", payload)
		return data
	},
	
	onError: (err) => {
		// handle error with axios (recommended for status code)
		// we can return a toast based on status code
	},

	onSuccess: () => {
		// executes after resolving succesfully the fetch
		// we can call a toast
	},

	onMutate: () => {
		// Optimistic UI - executes while HTTP requesting
		// manually update states logic here
	}
})
```

The `useMutation()` can return:
- **mutate()**: a function that calls this mutation
- **isLoading**: a boolean react state
- **data**: data returned from fetch

# Pagination

React query hook for infinite scrolling, using IntersectionObserver.

```jsx
import { useInfiniteQuery} from 'react-query'
import { INFINITE_SCROLL_PAGINATION_RESULTS } from '@/config'

const fetchPage = async ({ pageParam = 1 }) => {
	const query =
		`/api/...?limit=${INFINITE_SCROLL_PAGINATION_RESULTS}&page=${pageParam}`
	const { data } = await axios.get(query)
	return data
}

const { data, fetchNextPage, isFetchingNextPage } = useInfiniteQuery({
	queryKey: ['infinite-query'],
	
	queryFn: ({ pageParam }) => fetchData(pageParam),

	// fetchNextPage calls this function and trigger queryFn
	getNextPageParam: (_, pages) => {
		return pages.length + 1
	},
	
	// initial data for the query cache
	initialData: { pages: [initialPosts], pageParams: [1] },				
})
```

Initialize the Intersection Observer hook:
```jsx
import { useIntersection } from "@mantine/hooks"
const { ref, entry } = useIntersection({
	root: lastPostRef.current,
	threshold: 1,
})
```

Set the Intersection observer to the last HTML element:
```jsx
return (
	<ul className="flex flex-col col-span-2 space-y-6">
		{posts.map((post, index) => {
	
			if (index === posts.length - 1) {
				// Add a ref to the last post in the list
				return (
					<li key={post.id} ref={ref}>
						<Post .../>
					</li>
				)
			} else {
				return (
					<Post .../>
				)
			}
		})}
	
		{isFetchingNextPage && (
			<Loader2 className="w-6 h-6 text-zinc-500 animate-spin" />
		)}
	</ul>
```

Trigger it when element is intersected:
```jsx
useEffect(() => {
	if (entry?.isIntersecting) {
		fetchNextPage() // Load more posts when the last post comes into view
	}
}, [entry, fetchNextPage])
```