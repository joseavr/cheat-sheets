# Fix Sync Conflicts
Class: [[Git]]
Subject: #
Date: 2023-02-09
Topics: #, #, # 

---

# Local Repository Out of Sync

- When your local repository (computer) is out of sync with remote repository (GitHub).
- If you work on two computers, and let's say you `commit` two times in a day on `Computer 2` 
	- `Computer 1`: commit#1
	- `Computer 2`: commit#1, commit#2, commit#3
	- `Github remote`: commit#1, commit#2, commit#3(newest)
- Then `computer 1` will be behind by 2 commits from `Github remote` repo.
- This will cause out of sync.
- To solve this problem:

## Solution 1
- Simply `git pull` every time switched computers and before making any changes
- Only `git commit` when you done in one computer and gonna switch to another computer
- `git commit` only one time in a day
- This will prevent having commits behind from `Github remote` repo

## Solution 2

- If you have already commits behind `Github remote`, follow these commands:

1.  `git fetch` will load the `commit` that you dont have on your computer, which are on `Github remote`. From example above, now `Computer 1` will have commit#1, commit#2, commit#3
```bash
git fetch origin
```

2. Move to the last commit. You will lose any progress made in this computer. Ex, `Computer 1` will move from commit#1 to commit#3. `Computer 1` is now an exact copy of `Github remote`
```bash
git reset --hard origin/<branch-name>
```

3. `git clean` will remove unwanted files from your working directory
```bash
git clean -f -d
```

## Solution 3
- If both computers are in the same `commit`, but `computer 1` modified one file and `computer 2` modified a different file

1. `commit` first in either one computer, `computer 2`
```bash
git add .
git commit -m "message"
git push
```

2. In `computer 1`, 
```bash
git add .
git commit -m "message"
git pull   // to merge (add) changes from `computer 2` to `computer 1`
git push   // save changes to `github remote` repo
```

3. In `computer 2`,
```bash
git pull // to sync `computer 2` with `github remote` repo 
```

5. Now you can work on `computer 1` and all computers are sync.

# Branch Name
- To view your branch name
```bash
git branch
```
