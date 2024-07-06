# Git Reset


## Reset Soft

Allows to jump to a previous commit without losing any files. Once done, a new commit will be done

```bash
git reset --soft <commit_id | Head^ | Head~# (last # commits)>
```

Use Case:
- To rename a commit


## Reset Hard

Allows to jump to a previous commit but losing all before that commit

```bash
git reset --hard <commit_id | Head^ | Head~#>
```

Example:

```
Commit 4 - Head
Commit 3
Commit 2
Commit 1

Reset hard to Commit 2.
Commit 4 and Commit 3 are deleted.
```

Use Case:
- To back in time to a specific commit

## Reset Ammend

TODO 

## Rebase 

### Squash 

Merge commits into another commit. 

```bash
git rebase <-i | --interative> <commit_id | Head^ | Head~#>
```


Example:

```
pick   Commit 1
squash Commit 2
squash Commit 3

Commit 2 and 3 will be merge into Commit 1
```

Use Case:

- Sometimes we have several commits working on a feature, but we want a single commit feature
- A similar behaviour is `fixup`
