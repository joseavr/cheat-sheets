# Ruby Classes
Class: [[Ruby]]
Subject: #
Date: 2023-02-10
Topics: #, #, # 

---
https://www.tutorialspoint.com/ruby/ruby_classes.htm
https://www.tutorialspoint.com/ruby/ruby_object_oriented.htm
https://www.rubyguides.com/2019/02/ruby-class/

# Intro
Ruby is a perfect Object Oriented Programming Language. The features of the object-oriented programming language include 
-   Inheritance
-   Polymorphism
-   Data Encapsulation
-   Data Abstraction

# Class
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

# Constructor
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

# Objects
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

# Variables in Classes

## Local Variables
- `Local Variables` are the ones defined inside of a method scope. These are not available outside of scope.
- 
## Instance Variables
- `Instance Variables` are available across all objects (`childs`)
- Meaning that each `object` will have this variable.
- An instance variable from one object differs from another object. For instance:
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

## Global Variables



# Inheritance

# Polymorphism
