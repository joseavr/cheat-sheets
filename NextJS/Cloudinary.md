# Cloundary with Next.js

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-08-25

---

# Set Up

Install Package
```bash
npm install cloudinary
```

- In the API route, config cloudinary
```js
import { v2 as cloudinary } from 'cloudinary'

cloudinary.config({
	cloud_name: 'yourUsername',
	api_key: 'yourAPIKey',
	api_secret: 'yourAPISecret',
})
```

- Retrieve image from formData
```js
const data = await request.formData()
const image = data.get('image')
```

- Save locally
```js
const bytes = await image.arrayBuffer() // image in bytes
const buffer = Buffer.from(bytes) // convert to a js buffer
// path to save the image: currentWorkingDirectory, /public, -> string path
const filePath = path.join(process.cwd(), 'public', image.name)
await writeFile(filePath, buffer)

```

- Then save to Cloudinary
```js
const res = await cloudinary.uploader.upload(filePath)

-> {
	asset_id : string,
	url : string, // http
	secure_url: string // https
}
```

- Save to Database
```js
const result = await connection.query('INSERT INTO product SET ?', {
	name: data.get('name'),
	price: data.get('price'),
	description: data.get('description'),
})
```
