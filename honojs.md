# What is Hono.js

Hono.js is a backend framework with similar API from Express.js

# Why Choose Hono

Hono has so many features that includes:
- OpenAPI (a documentation for your api routes (hono makes it easy to setup)
- RPC (safe typed in the backend and frontend)
- Similar API like Express



## Status error


```json
// success
{
  "status": "success",
  "data": {...}
}

// error
{
  "status": "error",
  "message": "Something went wrong",
  "code": "INTERNAL_ERROR"
}
```