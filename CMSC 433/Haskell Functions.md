# Haskell Functions on Lists

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-10-24

---

# 🗺️ Map 

`(a -> b) -> [a] -> [b]`

- map returns a list of same length of `lst`
- The `map` function takes two arguments:
    - a function `f`: `(a -> b)`,
    - a list of type a: `[a]`.
- It applies the function `f` to every element in the input list, and returns a new list of type `[b]` that contains the results.

## Rule

```ocaml
map func lst
```


- At each iteration, it replaces `each` from list with
    - fun x

## Map Function

```ocaml
TODO
```

## Example
```haskell
map (3*) [1,2,3,4]
-- [3,6,9,12]
```


# 📂 Fold

- Iterates over a list -> do something on the list -> return something
- It's like `for of` loop! but returns something

```haskell
-- Both are equivalents
foldl f 0 list

for each in list:
	acc = do_smth(acc,x)
end
```

## ↩ Fold Left

`foldl :: (b -> a -> b) -> b -> [a] -> b`

### Rule
```haskell
foldl func acc lst
```
### Implementation
```haskell
myFoldl :: (b -> a -> b)  -> b -> [a] -> b
myFoldl f acc [] = acc
myFoldl f acc (h:t) = myFoldl (f acc h) t 
```
### Example 
```haskell
-- with function
let lst = [1, 2, 3, 4, 5]
let substract acc x = acc - x
let sum lst = foldl substract 0 lst -- `\` defines anonymoys func

-- with anonymous func
let lst = [1, 2, 3, 4, 5]
let sum lst = foldl (\acc x -> acc - x) 0 lst -- `\` defines anonymoys func

-- Returns
(1 - (2 - (3 - (4 - (5 - 0)))))
```


## ↪ Fold Right

`foldr :: (a -> b -> b) -> b -> [a] -> b`

### Rule
### Implementation
```haskell
myFoldr :: (a -> b -> b) -> b -> [a] -> b
myFoldr f acc [] = acc
myFoldr f acc (h:t) = f h (myFoldr f acc t)
```

### Example 



# ✅ Useful Functions

## Concat
```haskell
concat :: [String] -> String --type
concat [] = "" -- pattern matching
concat (h:t) = h ++ (concat t) -- pattern matching
```