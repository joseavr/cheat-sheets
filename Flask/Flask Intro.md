# 🌶️ Flask Intro
Class: [[]]
Subject: #
Date: 2023-03-05
Topics: #, #, # 

---

# 📥 Import Modules in Python

- Import modules or packages with the import keyword
	- import `<package_name>`
- Assign your own name with the as keyword
	- import `<package_name>` as `<new_name>`
- Import specific methods, classes, or packages
	- from `<package_name>` import `<method/class>`
- Gets rid of dot notation: 
	- `package_name.method()` becomes `method()`

# Create Virtual Environment
- Used to download all packages with specific version for a project

Mac
```bash
python3 -m venv venv
```

Windows
```
py -m venv venv
```

# Getting Ready to Projects
- Run `venv` environment before run Flask projects

Mac
```bash
source ./venv/bin/activate
```

Windows
```bash
./venv/Scripts/activate
```