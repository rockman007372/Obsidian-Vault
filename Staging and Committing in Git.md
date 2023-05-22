## Staging and Committing

_Committing_ saves a *snapshot* of the current state of the tracked files in the revision control history. Such a snapshot is also called a _commit_ (i.e. the noun).

**When ready to commit, you first _stage_ the specific changes you want to commit.** This intermediate step allows you to commit only some changes while saving other changes for a later commit.

![[Pasted image 20230118003300.png]]

### See files in Staging Area (intermediate area before commit)

```bash
git status
```

### Add Files to Staging Area

```bash
git add [file name]
git add . # add all files in directory
git add *
```

### Commit (save)

Must come with commit messages in present tense

```bash
git commit -m "Initial Commit"
```

### To see recent commit history

```bash
git log
git log --oneline
```
