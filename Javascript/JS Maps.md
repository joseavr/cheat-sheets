# JS Maps

📚Class: CMSC 335 Web Dev with Javascript

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/Javascript">Javascript</a>

✏️Section: 0101

🗓️Date: 2023-04-02

---

# 🗺️ Intro to Maps
- Same as `dictionaries` in Python
- Same as `hashes` in Ruby
- Collection of `key`-`value` pairs
	- `key`'s can be any value (including objects)
	- `value`'s can be any data

```js
const myMap = new Map();
```


# 🔨 Built-in Functions
## `set()`
- Add key-value pairs to a `Map`
```js
myMap.set('key1', 'value1'); 
myMap.set('key2', 'value2');

// myMap => { 'key1':'value1' , 'key2':'value2' }
```


## `get()`
- Get `value` by a given `key`
```js
myMap.get('key1');
// => 'value1'
```


## `has()`
- Checks if a key exists in the map.
```js
myMap.has('key1'); // output: true 
myMap.has('key2'); // output: false
```


## `keys()`
- Returns an iterator over the keys in the map
```javascript
for (const key of myMap.keys()) { 
    console.log(key);
}
// Output:
// key1
// key2
```


## `values()`
```js
for (const value of myMap.values() ) { 
    console.log(value); 
}
// Output
// value1
// value2
```


## `entries()`
- Returns an iterator object (e.g **Array**) with the [key, value] pairs in a Map
```js
for (const [key, value] of myMap.entries() ) { 
   console.log(`${key} = ${value}`);
}
// output:
// key1 = value1 
// key2 = value2
```


## `forEach()`
- Allows iterate over `key`-`value` pairs in the Map
```js
myMap.forEach( (value, key) => { 
    console.log(`${key} = ${value}`);
});
// output:
// key1 = value1 
// key2 = value2
```

## `size`
- Property: Returns the number of key-value pairs in the map.
```js
myMap.size; 
// output: 2
```

## `delete()`
- Removes a pair in the Map
```js
fruits.delete("key1");
```


## `clear()`
- Removes all the elements from the Map
```js
fruits.remove()
``` 


# 👎 Weak Maps
- Another kind of maps
- A collection of key-value pairs
- Primitive data types are not allowed as keys. The keys must be objects
- Primitive data types
	- Number
	- String
	- Boolean
- The values can be arbitrary values
- <mark style="background: #ADCCFFA6;">Cannot iterate over keys, values, or entries</mark>
- If the key is not being used in the map, the key will be **gargabe-collected**.
- If the map points to an object, and the object is dropped. Then the map is dropped too.
- Useful for **private instances** for a Class