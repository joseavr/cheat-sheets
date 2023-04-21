# Git Clone
Class: 
Subject: #
Date: 2023-02-17
Topics: #, #, # 

---

# Clone Repo

## From self
- FInd a spot to save repo, e.g go to `~/Documents`
- Clone repo from GitHub
```bash
git clone <HTTPSLink>
```
- New git folder is created e.g `~/Documents/git-repo`

### Change Folder Name
- If want to change the `<git-repo>` to another new git folder
- Copy `.git` to the new folder
```zsh
git pull
``` 

## From someone else

- We must know these two terminologies
	- `upstream`: keyword for repo from someone else
	- `origin`: keyword for own repo`

- Clone repo
```bash
git clone <HTTPSLink>
```

- Rename `origin` to `upstream` and add `origin` again so we can have `upstream` linked to **someone else repo** and `origin` linked to **our own repo**
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