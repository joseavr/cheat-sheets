# 💎 Regular Expression
Class: [[Ruby]]
Subject: #
Date: 2023-02-07
Topics: #, #, # 

---
https://www.rubyguides.com/2015/06/ruby-regex/

# 🎬 Regex Intro
- Regular Expression
	- A pattern that describes a set of Strings
	- are used to describe regular languages
	- tool used to search for text
- Regex is built-in and is a class in Ruby
	- Regexp
	- Syntax: `/pattern/` or `/pat/` 
```ruby
# Find the word 'like'
"Do you like cats?" =~ /like/ # Returns the index of the occurrance or nil
=> 7 
```

- Another way
```ruby
if "Do you like cats?".match(/like/)
	puts "Match found!"
end
```

# 🔡 Character Class
- A _character class_ is delimited with square brackets `[`, `]
- `[ab]` means a or b
- `/ab/` means a followed by b

- Lets define a range or a list of characters to match.
	- `[aeiou]` => matches any vowel
	- Enclosed by `/[a]/` matches for one character.
	- To match two characters, `/[a][b]/`
```ruby
def contains_vowel(str)
	str =~ /[aeiou]/
end

contains_vowel("test") # returns 1
contains_vowel("sky") # returns nil
```


#  🔍 Ranges
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

# ⚓️ Anchors
Anchors are metacharacters that match to a specific position:
-   `^` - Matches beginning of line
-   `$` - Matches end of line
-   `\A` - Matches beginning of string.
-   `\Z` - Matches end of string. If string ends with a newline, it matches just before newline
-   `\z` - Matches end of string
-   `\G` - Matches first matching position:
-   `\b` - Matches word boundaries when outside brackets; backspace (0x08) when inside brackets
-   `\B` - Matches non-word boundaries

# 🔁 Repetition
To match multiple characters we can use pattern modifiers
-  `+`  => Matches 1 or more characters
-  `*` => Matches 0 or more
-  `?` => Matches 0 or 1
-  `{ n }` => Matches exactly 1
-  `{n ,}` => Matches `n` or more
-  `{, m}` => Matches `m` or less
-  `{n,m}` - Matches between `x` and `y

```ruby
# example of '+'
"Hello".match(/[A-Z]+[a-z]+l{2}o/) #=> #<MatchData "Hello">
# [1 or more uppercase], [1 or more lowercase], 2 times 'l' characters, 
# and one 'o' character
```

# 🔘 Parenthesis in Regex
## Capturing
We can backreference to an `n` group of parenthesis with `\n`
- `/(\d) (\w)/`
	- `\1` references the first group parenthesis `(\d)`
	- `\2` references the second group `(\w)`
	- and so on
	- only  1-9 for `n` are supported using `\n`
	- Otherwise we can use Regex Global Variables
- Example
```ruby
"The cat sat in the hat".match(/[csh](..) [csh]\1 in/)
# [csh] = c
# (..) = at
# space
# [csh] = s
# \1 = (..) = at
```

- When using `.match`, it returns the group of parenthesis matched in an index
```ruby
# From previous example, its return value
=> <MatchData "cat sat in" 1:"at">   # at index 1: "at"

"The cat sat in the hat".match(/[csh](..) [csh]\1 in/)[1] # returns 'at'
```

- `\0` represents the whole matched string
- We can use `\0` and `.gsub` to substitute a matched pattern. Very useful
```ruby
"The cat sat in the hat".gsub(/[csh]at/, '\0s') # => "The cats sats in the hats"
# To every occurrence of "[csh]at" = '\0', add an 's' such that '\0s'
# Therefore, we'll have cats, sats, hats
```

## No Capturing
- When we want to group a pattern but not capture it, we use `?:`
- `(?:[0-9])([0-9])`

## Grouping
Parenthesis _group_ terms, allowing the pattern only work for this group.
- `/(pat)/`

# Backreference - Regex Global Variables
We can use these Regex global variables to backreference `group parenthesis`.
-   `$~` is equivalent to [`Regexp.last_match`](https://ruby-doc.org/3.2.0/Regexp.html#method-c-last_match);
-   `$&` contains the complete matched text;
-   ``$` `` contains string before match;
-   `$'` contains string after match;
-   `$1`, `$2` and so on contain text matching first, second, etc capture group;
-   `$+` contains last capture group

```ruby
# examples
m = 'haystack'.match(/s(\w{2}).*(c)/) #=> #<MatchData "stac" 1:"ta" 2:"c">
$~                                    #=> #<MatchData "stac" 1:"ta" 2:"c">
Regexp.last_match                     #=> #<MatchData "stac" 1:"ta" 2:"c">

$&   #=> "stac" # same as m[0]
$`   #=> "hay"  # same as m.pre_match
$'   #=> "k"    # same as m.post_match
$1   #=> "ta"   # same as m[1]
$2   #=> "c"    # same as m[2]
$3   #=> nil    # no third group in pattern
$+   #=> "c"    # same as m[-1]
```

# Alternation
The vertical bar metacharacter `a|b` is like `OR` in programming, either matches `a` or `b`
```ruby
# example 1
"Feliformia".match(/\w(and|or)\w/) #=> #<MatchData "form" 1:"or">
# \w = f
# (and|or) = or
# \w = m
# Match = form
```

``` ruby
# example 2
"furandi".match(/\w(and|or)\w/)    #=> #<MatchData "randi" 1:"and">
# \w = r
# (and|or) = and
# \w = i
# Match = randi
```


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

## Regex with Ruby Methods
- Regular expression can be used with many Ruby methods
	- .split
	- .scan
	- .gsub
