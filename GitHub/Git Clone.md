# Git Clone
Class: [[]]
Subject: #
Date: 2023-02-17
Topics: #, #, # 

---

# Clone Repo

## From self


## From someone else

- We must know these two terminologies
	- `upstream`: keyword for repo from someone else
	- `origin`: keyword for own repo`

- Clone repo
```bash
git clone <HTTPSLink>
```

- Rename `origin` to `upstream` and add `origin` again so we can have `upstream` for someone else repo and `origin` for our own repo
```bash
git remote rename origin upstream
git remote add origin httt://github.com/YOU/REPO.git
```

- To push to our own repo:
```bash
git push origin
```

- To get changes from someone else repo `upstream`
```bash
git fetch upstream
```