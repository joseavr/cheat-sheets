# Ruby Arrays
Class: <a href="">Ruby Arrays</a>
Subject: #
Date: 2023-03-14
Topics: #, #, # 

---

# Intro to Array in Ruby

-

# Push (add at end)
Adds the given object(s) on to the end of this array.
```ruby
a = [1, 2, 3]
a.push(4)
a    #=> [1,2,3,4]

a.push(5)
a    #=> [1, 2, 3, 4, 5]
```

# Unshift (add at front)
Adds a new item to the beginning of an array.
```ruby
arr = [1;2;3]
arr.unshift(0) 
arr   #=> [0, 1, 2, 3]
```

# Pop (remove at end)
Removes the last element from `self` and returns it, or `nil` if the array is empty.
```ruby
a = [ "a", "b", "c", "d" ]
a.pop     #=> "d"
a.pop(2)  #=> ["b", "c"]
a         #=> ["a"]
```

# Shift (remove at front)
Removes the first element from `self` and returns it, or `nil` if the array is empty
```ruby
a = [ "a", "b", "c", "d" ]
a.shift     #=> "a"
a.pop(2)  #=> ["b", "c"]
a         #=> ["d"]
```