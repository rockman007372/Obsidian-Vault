---
Date: Jul 3, 2022
Course:
---
# Commands

## Create new Git local repository 

 ```
git init
```

## See files in Staging Area (intermediate area before commit)

 ```
git status
```

## Add Files to Staging Area

```
git add [file name]

git add . # add all files in directory
```

## Commit (save)

Must come with commit messages in present tense

```
git commit -m "Initial Commit"
```

## To see recent commit history

```
git log
```

## See the differences between commits

```
git diff
```

## Rollback to most recent commit

-   `git checkout v1.0`: loads the state as at commit tagged `v1.0`
-   `git checkout 0023cdd`: loads the state as at commit with the hash `0023cdd`
-   `git checkout HEAD~2`: loads the state that is 2 commits behind the most recent commit

## Delete Commits

```
git reset --hard HEAD~2 # go back 2 commits ago
```

## Branching and Merging

-   We can create parallel branches with the master (main) branch, develop these branches separately and merge them at some point in the future.
-   We only want to merge when we are sure our branch is bug-free, usually we work on these parallel branches
-   To create a branch:

```
git branch [new branch name]
```

-   To see all the branches and which branch you currently are:

```
git branch
```

-   To switch branch:

```
git checkout [branch name]
```

-   To merge branches, go to the Master branch, then merge with desired branch

```
git merge [desired branch name]
```

## Ignore

Steps to obmit files:
- Make a .gitignore

```
vim .gitignore
```

- Type in the name of the files to be ignored

---

For remote repository commands, see [[GitHub and Remote Repository]].

# Summary

Common Git commands:

-   `git init` → Create a new git repository
-   `git add “newfile”` → Add a new file to your staging area
-   `git status` → Show which files are being tracked v. untracked
-   `git commit` → Adds staged changes to your local repository
-   `git log` → Show recent commit history
-   `git show “commit_id”` → show details of specific commit
-   `git push “remote” “ branch”` → Push local repository changes to your hosting service
-   `git pull “remote” “ branch”` → pull code from your hosting service to your local directory
-   `git branch` → See local branches
-   `git branch “newName”` → Create new local branch
-   `git checkout “branchName”` → Switch branches
-   `git diff` → See the actual difference in code between your working tree and your staging area
-   `git stash` → stash working directory
-   `git help` → manpages for git
-   `git help “gitCommand”` → man pages for specific git command


# Questions

## Why do we need a staging area?

The Staging Area is when git starts tracking and saving changes that occur in files. These saved changes reflect in the .git directory. That is about it when it comes to the Staging Area. You tell git that I want to track these specific files, then git says okay and moves them from you Working Tree to the Staging Area and says “Cool, I know about this file in its entirety.” However, if you make any more additional changes after adding a file to the Staging Area, git will not know about those specific changes until you tell it to see them. You **explicitly** have to tell git to notice the edits in your files.