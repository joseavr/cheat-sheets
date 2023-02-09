# Regular Expression
Class: [[Ruby]]
Subject: #
Date: 2023-02-07
Topics: #, #, # 

---
https://www.rubyguides.com/2015/06/ruby-regex/

# Intro 

# Regex Intro

- Regular Expression
	- A pattern that describes a set of Strings
	- are used to describe regular languages
	- tool used to search for text
- Regex is built-in and is a class in Ruby
	- Regexp
	- Syntax: /patter/
```ruby
# Find the word 'like'
"Do you like cats?" =~ /like/ #return index of the occurrence
=> 7
```
- Another way
```ruby
if "Do you like cats?".match(/like/)
	puts "Match found!"
end
```

# Character Class
- Lets  you define a range or a list of characters to math.
	- [aeiou] => matches any vowel
```ruby
def contains_vowel(str)
	str =~ /[aeiou]/
end

contains_vowel("test") # returns 1
contains_vowel("sky") # returns nil
```




# Ranges


