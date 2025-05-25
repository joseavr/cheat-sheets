Python is an interpreted high level programming language — non raw machine code or code close to human language — and it can be used for web dev, data visualization, and most commonly used nowadays for Machine Learning and LLMS.

Python is a multi-paradigm language meaning that supports functional programming, imperative programming, object oriented programming. Easy to adapt to the programmer way to code. 

Fun fact, the name Python does not come from the snake. It comes from the comedian group Monty Python. Python was created by Guido van Rossum in 1989 and launched 1991. Number 1 most used language in 2024, after Javascript.

To check python version
```python
python3 --version
```

If Python not installed, install via Anaconda: https://anaconda.org/anaconda/python or via https://python.org

For case you want to skip installation and use python only for learning purposes, use a sandbox ran in the web: https://pythonsandbox.io/editor

Extensions for Vscode:
- Python
- Pylance
- Python debugger

Python files always ends in its name with `file_name.py`

By convention, every file name in python is in snake case.


# Data Types

```python
4   # integer
1.0   # float    
1e3   # 1000.0 -> float
2j   # complex numbers
"Hello World"   # string
True   # boolean
None   # None type
[1, 2, 3]   # list
(1, 2, 3)   # tuple
{"key": "value", "age": 30}   # dictionary
{1, 2, 3}   # set
```


## Type Casting

Transform one type to another type. For example, float to integer, string to integer.

```python
# Str9ng to integer
int("100")
# -> 100
 
# Integer to float
float(10)
# -> 10.0

# Number to string
str(123)
# -> '123'

# Boolean to integer
int(True)
# -> 1

int(False)
# -> 0

# Integer to boolean
bool(0)
# -> False

bool(42)
# -> True

# List to tuple
tuple([1, 2, 3])
# -> (1, 2, 3)

# Tuple to list
list((1, 2, 3))
# -> [1, 2, 3]

# String to list of characters
list("hello")
# -> ['h', 'e', 'l', 'l', 'o']

# Example of an error
print("100" + 2)  # ❌ this line will trigger an error
# -> TypeError: can only concatenate str (not "int") to str

# Corrected version using type casting
print(int("100") + 2)
# -> 102

# Casting with potential failure
int("abc")  # ❌ will raise ValueError
# -> ValueError: invalid literal for int() with base 10: 'abc'
```


# Variables

Variables allows you to store data. What kind of data? All data types that Python supports. To have a variable, you need to name it and assign it with `=` a data.

```python
age = 25
name = "John"
```

Variables in Python are muteable. That is, once you set them to a specific data, you can change the variable to another data. In other programming language is not allowed but in Python is.

```python
name = "John"
...more code...
name = "Doe"
```

Variables names cannot start with numbers or special characters. In Python is common to use snake case to name variables, files, etc.


# Conditionals (if, elif, else)

Conditionals allows to execute code block if condition is met.

```python
age = 18

if age >= 21:
	print("You can drink")
elif age >= 18:
	print("You can drive")
else:
	print("Go to school")
```

## Logical Operator

Logical operators are used to combine conditional statements. Python has 3 logical operators: `and`, `or`,  `not`

- `and` – Returns `True` if both statements are true
```python
age = 18
has_license = True

if age >= 18 and has_license
	print("You can drive")
else:
	print("Take Uber")
```


- `or` – Returns `True` if at least one statement is true
```python
is_weekend = True
is_holiday = False

if is_weekend or is_holiday:
    print("You can sleep in")
else:
    print("Go to work")
```


- `not` – Reverses the logical state
```python
is_raining = True

if not is_raining:
    print("Go outside")
else:
    print("Stay inside")
# -> Stay inside
```


# Data Structures

Data structures are ways to organizing, storing, and managing data so it can be accessed and modified efficiently. Python provides built-in data structures such as: lists, sets,  dictionaries, tuples and among others.

## Lists

List is a built-in data structure in python that stores a collection of data or elements. Not necessary has to be the same data type. List has handy methods that can be used for accesing and modifying it. 

### Accessing and Modifying a List

```python
mylist1 = [1,2,3,4] # integer list
mylist2 = ["a", "b", "c"] # string list
mylist3 = [1, "hi", 3.14, True] # mix data types list
mylist4 = [[1,2], [3,4]] # list of lists

# Accessing elements in a list
mylist1[0] # -> 1
mylist1[1] # -> 2
mylist1[2] # -> 3
mylist1[3] # -> 4

mylist4[-1] # -> [3,4]
mylist4[-1][0] # -> 3

# Modifying elements in a list
mylist2[0] = "A"
mylist1 = mylist1 + mylist2 # -> [1, 2, 3, 4, "A", "b", "c"]

# Getting the size of the list
len(mylist1) # -> 7

# Add one element at the end of the list
mylist3.append(False)
# -> [1, "hi", 3.14, True, False]

# Add one element at beginning of the list
mylist3 = [True] + mylist2 
# -> [True, 1, "hi", 3.14, True, False]

# Add elements at the end of the list
mylist3.extend([1, 2])
# -> [True, 1, "hi", 3.14, True, False, 1, 2]

# Insert one element in the list: list.insert(index,value)
mylist3.insert(0, "Hello")
# -> ["Hello", True, 1, "hi", 3.14, True, False, 1, 2]

```



### Removing an element in the List


```python
mylist = [10, 2, 40, 2, 60]

# Removing an element from the list
mylist.remove(2) # only removes the first occurent element
# mylist -> [10, 40, 2, 60]

# Removing the last element of the list and returns it
last = mylist.pop() # -> 60
# mylist -> [10, 40, 2]
# last -> 60

# Remove at certain index
mylist.pop(0) # remove the first element of the list
mylist.pop(1) # remove the second element of the list

# Another way to delete an element from the list
del mylist[0]

# Remove all elements
mylist.clear()

# Remove a range of elements
mylist = [1, 2, 3, 4, 5]
del mylist[0:3]
# mylist -> [4, 5]
```


### More Methods

```python
mylist = [1, 40, 20, 10]

# Sort the list in-place (modifies mylist)
mylist.sort()
# mylist -> [1, 10, 20, 40]

# Sort the list and return it (does not modify mylist)
mylist = [1, 40, 20, 10]
sorted_list = sorted(mylist)
# sorted_list -> [1, 10, 20, 40]
# mylist -> [1, 40, 20, 10]

# Count occurrences in the list
mylist = ['a', 'b', 'c', 'a']
mylist.count('a')
# -> 2

# Check if element is in the list
'b' in mylist # True
20 in mylist # False

```


# Loops

## While Loop

Executes a block code repeatedly only if the condition is met

```python
count = 0

while count <= 3:
	print(count)
	count += 1

# -> 0
# -> 1
# -> 2
# -> 3
```


## For Loop


```python
for count in range(4):
    print(count)
# -> 0
# -> 1
# -> 2
# -> 3
```

We also can iterate a list

```python
my_list = ['apple', 'banana', 'cherry', 'strawberry']

for item in my_list:
	print(item)

# or
for item, index in enumerate(my_list):
	print(item, index)
```

## List Comprehensions (Shorthand loop)


```python
# A normal for loop to iterate each letter and save it into the list
my_list = []
for letter in 'home':
    my_list.append(letter)

# list comprehension - example 1
list = [letter for letter in 'home']

# example 2
evens = [x for x in range(10) if x % 2 == 0]
# evens -> [0, 2, 4, 6, 8]

# exmaple 3
capitalized = [word.capitalize() for word in ['hello', 'world']]
# capitalized -> ['Hello', 'World']
```


# Functions

Reusable and parameterizable (allow inputs) code blocks to do specific tasks

```python
def function_name(param1, param2, ...):
	# code block
```

A simple function

```python

# definition of the function
def greet():
	print("Hello")

# call the function
greet()
```


A function with parameters

```python
def greet_to(name):
	print(f"Hello, {name}!")

greet("Sergion")
```

A function with parameters and returns a value

```python
def addition(value1, value2):
	result = value1 + value2
	return result

simple_addition = addition(1, 2)
# simple_addition -> 3 
```

