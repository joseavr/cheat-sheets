# Files
Class: [[Ruby]]
Subject: #
Date: 2023-02-09
Topics: #, #, # 

---

# Open Files

```ruby
f = File.open("data.txt")
```

# Read File
```ruby
line = f.gets
```

## Example
```ruby
regex = /^[0-9A-Z\]$/
# [0-4] => 0|1|2|3|4

line = f.gets
while line
	if line =~ regex
		puts line
	end
	line = r.gets
end

f.close
```
