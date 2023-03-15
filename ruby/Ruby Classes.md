# 💎 Ruby Classes
Class: [[Ruby]]
Subject: #
Date: 2023-02-10
Topics: #, #, # 

---
https://www.tutorialspoint.com/ruby/ruby_object_oriented.htm
https://www.rubyguides.com/2019/02/ruby-class/

# 💎 Intro
Ruby is a perfect Object Oriented Programming Language. The features of the object-oriented programming language include 
-   Inheritance
-   Polymorphism
-   Data Encapsulation
-   Data Abstraction

# 🗳️ Class
- Describes in general what an `object` is with methods and variables.
- For example: 
	- `Students` is a class
	- `Jose Valdivia`, a particular student, is an object
- A class in ruby always start with `class` keyword followed by a `name`
```ruby
class Students
	variables
	methods
end
```

# 📝 Constructor
- Useful when creating an `object` with specific values
```ruby
class Student
	def initialize(id, name, age)
		@id = id
		@name = name
		@age = age
	end
end
```

# 📃 Objects
- `objects` are instances of the `class`.
- An instance means that objects (`child`) are created based on their class (`parent`).

## Creating Objects
- We can create objects using the method `new`
- Similar to Java
```ruby
student_1 = Student.new
student_2 = Student.new
```

## Creating Objects with Constructor
- We can create objects with specific values 
```ruby
student_1 = Student.new("1", "Jose", "23")
student_2 = Student.new("2", "Kevin", "29")
```

# 📦 Variables in Classes

## Local Variables
- `Local Variables` are the ones defined inside of a method scope. These are not available outside of scope.

## Instance Variables
- `Instance Variables` are available across all objects but unique for each object.
- In other words, an instance variable from one object differs from another object. For instance:
```ruby
student_1.name = "Jose"
student_2.name = "Kevin"
```
- Instance variables are preceded by the at sign `@` followed by the variable name.
```ruby
class Student
	@id
	@name
	@age
end
```

## Class Variables
- `Class Variable` are shared between all objects.
- If the class variable from a object is modified, another object of the same class also updates it.
- Instance variables are preceded by the sign `@@` followed by the variable name.

## Attr_accesor vs Attr_writer vs Atrr_reader
https://www.bootrails.com/blog/ruby-attr-accessor-attr-writer-attr-reader/#:~:text=Summary,scope%20of%20the%20class%20definition.
- In ruby, methods are public, but data are private. 
	- Public: can be accessed outside of class
	- Private: cannot be accessed outside of class
- For example
```ruby
# Student has @id, @name, @age
student_1 = Student.new("01","Jose","23")
student_1.name    # This gives error
```
- To fix this, we do `getters` and `setters` methods. Such as
```ruby
# Setters
def name 
	return @name 
end

def name=(new_name)
	@name = new_name
```

- But it's tedious writing `getters` and `setters` for each instance variables, but there's another way

### attr_reader
- Data are private
- We use this when we want to 
	- keep instance variables private from changing, 
	- but access them publicly (without `getters` methods)

```ruby
Class Students
	attr_reader :id, :name, :age # <-- Getters

	def initialize
		code
	end
end

# student_1.name => allowed
# student_1.name="Dave" => not allowed
```

### attr_writer
- Data are private
- We use this when we want to 
	- keep instance variables private from accessing them, 
	- but changing them publicly (without `setters` methods)

```ruby
Class Students
	attr_writer :id, :name, :age # <-- Getters

def initialize
		code
	end
end
# student_1.name => not allowed
# student_1.name="Dave" => allowed
```

### attr_accessor
- It's the combination of both attr_reader and attr_writer
```ruby
Class Students
	attr_accessor :id, :name, :age # <-- Getters

def initialize
		code
	end
end
# student_1.name => allowed
# student_1.name="Dave" => allowed
```



# Inheritance

# Polymorphism
