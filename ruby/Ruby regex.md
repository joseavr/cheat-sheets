# Regular Expression
Class: [[Ruby]]
Subject: #
Date: 2023-02-07
Topics: #, #, # 

---
https://www.rubyguides.com/2015/06/ruby-regex/

# Regex Intro

- Regular Expression
	- A pattern that describes a set of Strings
	- are used to describe regular languages
	- tool used to search for text
- Regex is built-in and is a class in Ruby
	- Regexp
	- Syntax: `/patter/
```ruby
# Find the word 'like'
"Do you like cats?" =~ /like/ #return index of the occurrence
=> 7 # Returns the index of the occurrance or nil
```

- Another way
```ruby
if "Do you like cats?".match(/like/)
	puts "Match found!"
end
```

# Character Class
- A _character class_ is delimited with square brackets `[`, `]
- /\[ ab \]/ means a or b
- /ab/ means a followed by b

- Lets define a range or a list of characters to match.
	- \[aeiou\] => matches any vowel
	- Enclosed by \[ X \] matches for one character.
	- To match two characters, \[ X \] \[Y\]
```ruby
def contains_vowel(str)
	str =~ /[aeiou]/
end

contains_vowel("test") # returns 1
contains_vowel("sky") # returns nil
```


# Ranges
- `/./` => Any character except newline
- `/./m` => Any character, `m` enables multiline mode
- `\w` => A word character (`[a-zA-Z0-9_]`)
- `\W` => A non-word character (`[^a-zA-Z0-9_]`)
- `\d` - A digit character (`[0-9]`)
- `\D` - A non-digit character (`[^0-9]`)
- `\h` - A hexdigit character (`[0-9a-fA-F]`)
- `\H` - A non-hexdigit character (`[^0-9a-fA-F]`)
- `\s` - A whitespace character: `/[ \t\r\n\f\v]/`
- `\S` - A non-whitespace character: `/[^ \t\r\n\f\v]/`
- `\R` - A linebreak: `\n`, `\v`, `\f`, `\r` `\u0085` (NEXT LINE), `\u2028` (LINE SEPARATOR), `\u2029` (PARAGRAPH SEPARATOR) or `\r\n`.

# Anchors
-   `^` - Matches beginning of line
-   `$` - Matches end of line
-   `\A` - Matches beginning of string.
-   `\Z` - Matches end of string. If string ends with a newline, it matches just before newline
-   `\z` - Matches end of string
-   `\G` - Matches first matching position:
-   `\b` - Matches word boundaries when outside brackets; backspace (0x08) when inside brackets
-   `\B` - Matches non-word boundaries

# Repetition
- To match multiple characters we can use pattern modifiers
-  `+`  => Matches 1 or more characters
-  `*` => Matches 0 or more
-  `?` => Matches 0 or 1
-  `{ n }` => Matches exactly 1
-  `{n ,}` => Matches `n` or more
-  `{, m}` => Matches `m` or less
-  `{n,m}` - Matches between `x` and `y

```ruby
"Hello".match(/[A-Z]+[a-z]+l{2}o/) #=> #<MatchData "Hello">
# [1 or more uppercase] [1 or more lowercase] 2 'l' characters, one 'o' character
```

# Regex Global Variables
-   `$~` is equivalent to [`Regexp.last_match`](https://ruby-doc.org/3.2.0/Regexp.html#method-c-last_match);
-   `$&` contains the complete matched text;
-   `` $` `` contains string before match;
-   `$'` contains string after match;
-   `$1`, `$2` and so on contain text matching first, second, etc capture group;
-   `$+` contains last capture group

# Options
End delimiter of a regex can be followed by one or more single-letter options:
-   `/pat/i` - Ignore case
-   `/pat/m` - Treat a newline as a character matched by `.`
-   `/pat/x` - Ignore whitespace and comments in the pattern
-   `/pat/o` - Perform `#{}` interpolation only once

# Encoding
-   `/_pat_/u` - UTF-8
-   `/_pat_/e` - EUC-JP
-   `/pat/s` - Windows-31J
-   `/pat/n` - ASCII-8BIT

