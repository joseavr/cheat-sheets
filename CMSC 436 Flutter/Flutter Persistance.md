# Persitance with Flutter

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2024-04-07

---

# Local Storage - Shared Preference Package

## Initialize Singleton

Create a singleton:

```dart
SharedPreferences.getInstance().then( (value) { save the value })
// -> Future<SharedPreferences>
```

## Read

Sync operations:

```dart
getBool(key) // -> bool?
getInt(key) // -> int?
getDouble(key) // -> double?
getString(key) // -> String?
getStringList(key) // -> List<String>?
```

## Write

Async operations:

```dart
setBool(key, value) 
setInt(key, value) 
setDouble(key, value) 
setString(key, value) 
setStringList(key, value)
remove(key) 
```


# Remote DB - Redis

## Read


## Write


```dart
JSON.ARRAPPEND key value

// example
{ "myArray": [ "apple"] }
JSON.ARRINSERT myArray "orange"
{ "myArray": [ "apple", "orange" ]}
```


```dart
JSON.ARRINSERT key index value

// example
{ "myArray": [ "apple", "banana" ] }
JSON.ARRINSERT myArray 1 "orange"
{ "myArray": [ "apple", "orange", "banana"]}

```

## Delete 

