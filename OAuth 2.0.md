
# OAuth2.0 Flow in Google
## Step 1: Sign in

Construct the url to sign-in with:
- scope: email, profile, openid
- client_id
- redirect_uri: url to where google sends the code

```uri
https://accounts.google.com/o/oauth2/v2/auth?redirect_uri=https%3A%2F%2Fdevelopers.google.com%2Foauthplayground&prompt=consent&response_type=code&client_id=407408718192.apps.googleusercontent.com&scope=https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fuserinfo.email+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fuserinfo.email+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fuserinfo.email&access_type=offline
```

Once logged in, Google sends to the `redirect_uri` as searchParams the `code` to be exchanged

```
/oauthplayground/?code=4%2F0AVMBsJgpTROq0RJVS8hTgW2g7SEm7MdKX9xsBmh8vZlGKWdMCynmAC9iuoFw5LoecgW1Mg&
scope=email+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fuserinfo.email+openid&
authuser=1&
prompt=consent
```
## Step 2: Exchange code for token

To exhange needs to call to:
```
oauth2.googleapis.com
```

With the code, redirect uri, client_id, client_secret as searchParams:
```
code=4%2F0AVMBsJgpTROq0RJVS8hTgW2g7SEm7MdKX9xsBmh8vZlGKWdMCynmAC9iuoFw5LoecgW1Mg&
redirect_uri=https%3A%2F%2Fdevelopers.google.com%2Foauthplayground&
client_id=407408718192.apps.googleusercontent.com&
client_secret=************&scope=&grant_type=authorization_code
```


Google response after exchaning

```json
{
  "access_token": "ya29.a0AS3H6Nx-...", 
  "id_token": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjFiYjc3NGJk...", 
  "expires_in": 3599, 
  "refresh_token_expires_in": 604799, 
  "token_type": "Bearer", 
  "scope": "https://www.googleapis.com/auth/userinfo.email openid", 
  "refresh_token": "1//04HcgqWa2yM6jCgYIARAAGAQSNwF-..."
}
```

To refresh `access_token` using the `refresh_token` needs to call:
```
oauth2.googleapis.com
```

with the following searchParams:
```
client_secret=************&
grant_type=refresh_token&
refresh_token=1%2F%2F04HcgqWa2yM...
client_id=407408718192.apps.googleusercontent.com
```

The response is:
```json
{
  "access_token": "ya29.a0AS3H6Nz...", 
  "refresh_token_expires_in": 602386, 
  "expires_in": 3599, 
  "token_type": "Bearer", 
  "id_token": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjFiYjc3NG...", 
  "scope": "https://www.googleapis.com/auth/userinfo.email openid"
}
```


## Step 3: Send Request

Now, with the access_token, you can send request to google API using access_token via Bearer

Send request:
```
GET /oauth2/v2/userinfo HTTP/1.1
Host: www.googleapis.com
Content-length: 0
Authorization: Bearer ya29.a0AS3H6NxcdWp4S8QIEFALJNG...
```

Response:
```json
{
  "picture": "https://lh3.googleusercontent.com/a-/ALV-UjUkz6PvG1i3x5POA1TsfD-8Q8lljMfrKue7xUauqC4Sco_eNQ=s96-c", 
  "verified_email": true, 
  "id": "116839351050984111627", 
  "email": "pjose.u1999@gmail.com"
}
```


Playground: 

```
https://developers.google.com/oauthplayground/
```



# What is refresh token rotation?

Refresh token rotation is the practice of updating an access_token on behalf of the user, without requiring interaction (ie.: re-authenticating). access_tokens are usually issued for a limited time. After they expire, the service verifying them will ignore the value, rendering the access_token useless. Instead of asking the user to sign in again to obtain a new access_token, many providers also issue a refresh_token during initial signin, that has a longer expiry date. Auth.js libraries can be configured to use this refresh_token to obtain a new access_token without requiring the user to sign in again.


# Session Strategies

When a user visits your application, you want them to not have to log in every single time. After logging in once, your application should save some data about the user and allow them to pick up where they left off the next time they visit. This is called a session. 

There are **two** main session strategies, the JWT-based session and Database session.

## 1. JWT Session
Auth.js can create sessions using JSON Web Tokens (JWT). This is the default session strategy for Auth.js unless a database provider is configured. When a user signs in, a JWT is created in a HttpOnly cookie. Making the cookie HttpOnly prevents JavaScript from accessing it client-side (via document.cookie, for example), which makes it harder for attackers to steal the value. In addition, the JWT is encrypted with a secret key only known to the server. So, even if an attacker were to steal the JWT from the cookie, they could not decrypt it. Combined with a short expiration time, this makes JWTs a secure way to create sessions.

When a user signs out, Auth.js deletes the JWT from the cookies, destroying the session.

### Advantages 
- JWTs as a session do not require a database to store sessions; this can be faster, cheaper, and easier to scale.
- This strategy requires fewer resources as you don’t need to manage an extra database/service.
- You may then use the created token to pass information between services and APIs on the same domain without having to contact a database to verify the included information.
- You can use JWT to securely store information without exposing it to third-party JavaScript running on your site.
### Disadvantages
- Expiring a JSON Web Token before its encoded expiry is not possible - doing so requires maintaining a server-side blocklist of invalidated tokens (at least until they truly expire) and checking every token against the list every time a token is presented. Auth.js will destroy the cookie, but if the user has the JWT saved elsewhere, it will be valid (the server will accept it) until it expires. (Shorter session expiry times are used when using JSON Web Tokens as session tokens to allow sessions to be invalidated sooner and simplify this problem.)
- Auth.js enables advanced features to mitigate the downsides of using shorter session expiry times on the user experience, including automatic session token rotation, optionally sending keep-alive messages (session polling) to prevent short-lived sessions from expiring if there is a window or tab open, background re-validation, and automatic tab/window syncing that keeps sessions in sync across windows any time session state changes or a window or tab gains or loses focus.
- As with database session tokens, JSON Web Tokens are limited in the amount of data you can store in them. There is typically a limit of around 4096 bytes per cookie, though the exact limit varies between browsers. The more data you try to store in a token and the more other cookies you set, the closer you will come to this limit. Auth.js implements session cookie chunking so that cookies over the 4kb limit will get split and reassembled upon parsing. However, since this data needs to be transmitted on every request, you need to be aware of how much data you want to transfer using this technique.
- Even if appropriately configured, information stored in an encrypted JWT should not be assumed to be impossible to decrypt at some point - e.g., due to the discovery of a defect or advances in technology. Data stored in an encrypted JSON Web Token (JWE) may be compromised at some point. The recommendation is to generate a secret with high entropy.


## 2. Database session
Alternatively to a JWT session strategy, Auth.js also supports database sessions. In this case, instead of saving a JWT with user data after signing in, Auth.js will create a session in your database. A session ID is then saved in a HttpOnly cookie. This is similar to the JWT session strategy, but instead of saving the user data in the cookie, it only stores an obscure value pointing to the session in the database. So whenever you try to access the user session, you will query the database for the data.

When a user signs out, the session is deleted from the database, and the session ID is deleted from the cookies.

### Advantages
- Database sessions can be at any time modified server-side, so you can implement features that might be more difficult - but not impossible - using the JWT strategy, etc.: “sign out everywhere”, or limiting concurrent logins
- Auth.js has no opinion on the type of database you are using; we have a big list of official database adapters, but you can implement your own as well
### Disadvantages
- Database sessions need a roundtrip to your database, so they might be slower at scale unless your connections/databases are accommodated for it
- Many database adapters are not yet compatible with the Edge, which would allow faster and cheaper session retrieval
- Setting up a database takes more effort and requires extra services to manage compared to the stateless JWT strategy





# How the client sends the JWT stored in the http-only cookie to the server?
###  1. Server-Side Cookie Creation:
When a user successfully logs in, the server generates a JWT and sets it as an HTTP-only cookie. This cookie is typically configured with flags like HttpOnly, Secure (if using HTTPS), and SameSite to enhance security. 
### 2. Client-Side Storage:
The browser automatically stores the HTTP-only cookie. The client-side JavaScript (e.g., in a React app) cannot directly access the cookie's value due to the HttpOnly flag. 
### 3. Automatic Cookie Transmission:
When the client makes a request to the server (e.g., to access a protected resource), the browser automatically includes all relevant cookies in the request headers, including the HTTP-only cookie containing the JWT. 
### 4. Server-Side JWT Extraction:
On the server side, the Authorization header is not used to pass the JWT. **Instead, the server extracts the JWT from the Cookie header within the request.**
### 5. Authentication:
The server then verifies the JWT to authenticate the request. 


## What is the difference between Authorization header vs Cookie header

The **difference between using the `Authorization` header and the `Cookie` header** in a JWT strategy mainly lies in how the JWT is sent to the server and how that affects **security**, **convenience**, and **cross-origin behavior**.

### 🔑 **Authorization Header**

* **Format:** `Authorization: Bearer <JWT>`
* **Used in:** APIs, mobile apps, SPAs
* **Manual sending:** The client (e.g., frontend code) must attach this header explicitly.

**Pros:**

* Stateless and RESTful.
* Works well for APIs and mobile apps.
* Easy to invalidate (change token, done).
* Doesn't automatically get sent on every request — you control when it's sent.

**Cons:**

* Vulnerable to **XSS** if the JWT is stored in `localStorage` or `sessionStorage`.
* You must manually handle sending the header on every request.

### 🍪 **Cookie Header**

* **Format:** `Cookie: token=<JWT>`
* **Used in:** Web apps (especially those with sessions)
* **Automatic sending:** The browser sends cookies automatically with every request to the matching domain.

**Pros:**

* **Secure if using httpOnly + Secure flags**: not accessible via JavaScript → protects against XSS.
* Automatically sent with requests, so no need to manually set headers.
* Plays well with traditional server-side authentication workflows.

**Cons:**

* Vulnerable to **CSRF** unless:
	* You use the `SameSite=Strict` or `SameSite=Lax` attribute on the cookie.
	* Or pair it with CSRF tokens in forms.
* Doesn’t work well with APIs accessed cross-origin unless CORS is configured properly.

## When should I use?

| Scenario                                      | Recommendation                                  |
| --------------------------------------------- | ----------------------------------------------- |
| **SPA or mobile app**                         | Use `Authorization: Bearer <JWT>`               |
| **Traditional web app (form login)**          | Use **httpOnly Secure Cookies**                 |
| **Security priority (no XSS token exposure)** | Use Cookies with `httpOnly` + `SameSite=Strict` |
| **API-first or cross-platform app**           | Use Authorization header                        |

# If Google token expires, should I refresh it?, How about my JWT stored in Cookies?

If your app **only uses the basic info** from the JWT (like user ID, email, etc.) and **doesn't rely on the Google `access_token`** for making requests to Google APIs (e.g., calendar, Gmail, profile updates), then:


 ✅ You **can continue using the JWT** until it expires.

Here’s the reasoning:

* The JWT is your **app's session token**, not Google's.
* If the JWT is valid and securely stored (e.g., http-only cookie), you can **trust its claims** (e.g., user ID, email).
* The expiration of the Google `access_token` is only relevant **if you’re interacting with Google APIs** on behalf of the user.


### Example scenarios:

✅ Continue Session (Google token expired, but not used):

* Your app just shows user data stored in your DB (e.g., dashboard, saved URLs).
* No need to refresh Google tokens. Let the user stay logged in.

❌ Refresh Needed (Google token expired and used):

* Your app calls Google APIs (e.g., get contacts, fetch profile image from Google).
* You'll need to refresh the Google token **in the background** (if refresh token is available), or prompt the user to re-auth.

### Summary Decision Logic:

| Google Access Token Expired | Uses Google APIs? | Action                       |
| --------------------------- | ----------------- | ---------------------------- |
| Yes                         | No                | ✅ Continue using JWT session |
| Yes                         | Yes               | 🔄 Try refresh, else re-auth |
| No                          | Irrelevant        | ✅ Continue normally          |

Let me know if you want help implementing token refresh middleware or conditional API access based on token freshness.


### When should you refresh the Google token?

Only when needed. For example:

- On a route where you’re about to call the Google API (e.g. calendar, user profile, etc.)
- In that route handler, check:
	- Is the access token expired?
	- If yes, then call refreshGoogleToken() (this will hit DB + Google).
	- If that fails, ask user to re-auth.


# Good to know about `exp` and `max_age` in Cookies

The browser stores the `max_age` and `expires` in the following format:
- `max_age` in miliseconds
- `expires` in Date type

```ts
// Date.now() returns time in miliseconds since epoch (1970-1-1)
const now = Math.floor(Date.now()) // miliseconds
const expires = now + (60 * 60 * 24 * 7 * 1000) // miliseconds (now since epoch) + miliseconds (7 days)
```

### Tip

`Date` object accepts miliseconds 

`Date.now()` returns time in miliseconds since epoch (1970-1-1)

```ts
new Date(expires)
// -> Sun Jul 06 2025 16:04:29 GMT-0400 (Eastern Daylight Time)
// Today was: Sun Jun 29 2025 16:04:29 GMT-0400 (Eastern Daylight Time)
```

