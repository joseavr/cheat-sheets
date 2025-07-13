
There are 4 levels of caching in Next.js

- Request Memoization
- Data Cache
- Route Cache
- Full Route Cache


## Request Memoization

Happens in the Server.

It triggers automatically building the React Component Tree, per-request lifecycle.

In a single request cycle, when building the React Component Tree, data (from requests) passed in React props are reused/memoized.

If using an ORM and can't use `fetch()`, use `cache` from`React` 

To invalidate:

- Lasts only for the lifetime of the request
## Data Cache

There are 4 different types of cache in Data Cache

- Static Site Generation
- Incremental Site Generation
- Server Side Rendering

Characteristic:
- stored on the server
- persist across requests
#### Static Site Generation

In next.js 15, cache is not by default. But to opt in cache to have static site generation:

```js
fetch("https://...", { cache: "force-cache" })
```


#### Incremental Site Generation

```js
fetch("https://...", {
	cache: "force-cache",
	next: { revalidate: 3600 } // cache every 1 hour
})
```

In the code, it means have stale data for 1 hour and revalidate to have fresh data after 1 hour.

#### Server Side Rendering

No cache. By default in Next.js 15. Every request will return fresh data.

```js
fetch("https://...", { cache: "no-store-i" })
fetch("https://...") // in next.js 15 by default cache no-store
```


How to invalidate:

If you opt in cache, to invalidate cache (or purge cache) from Data Cache, there are two ways:

- Server Side (Route Handler / Server Action)
	- `revalidatePath()`
	- `revalidateTag()`
- Client Side
	- `router.refresh()`

## Router Cache

Happens in the Client.
It's a browser memory / in-memory cache of RSC payload (either in static and dynamic routes)

Router Cache triggers when navigating between pages using `<Link/>` Component

Used for improving navigation experience by storing
- previosuly visited routes
- prefetching future routes

How to invalidate:

Cannot opt out but can invalidate cache (or purge cache) from Router cache by:

- Server Side (Route Handler / Server Action)
	- `revalidatePath()`
	- `revalidateTag()`
- Client Side
	- `router.refresh()`
Additionally:
- `cookies.set` or `cookies.delete`
- prefetch={false} on `<Link/>` component


## Full Route Cache

Happens in the Server.
It's a server memory cache of HTML and RSC payload from Static Routes. Like  a CDN

Using:
```js
export const revalidate = 3600 // show stale data (cache data) for 1 hour then after 1 hour revalidate to get fresh data (cache purged)
```


How to invalidate:
- Redeploying

To opt out:
- `revalidate = 0` (get always fresh data)
- export const dynamic = 'force-dynamic'
- fetch with no cache options